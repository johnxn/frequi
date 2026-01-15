<script setup lang="ts">
const props = withDefaults(
  defineProps<{
    availablePairs: string[];
    selectedPair?: string;
  }>(),
  {
    selectedPair: '',
  },
);

const emit = defineEmits<{
  selectionChange: [value: string];
}>();

const filterText = ref('');

const filteredPairs = computed(() => {
  if (!filterText.value) {
    return props.availablePairs;
  }
  const filter = filterText.value.toLowerCase();
  return props.availablePairs.filter((pair) => pair.toLowerCase().includes(filter));
});

const selectPair = (pair: string) => {
  emit('selectionChange', pair);
};
</script>

<template>
  <div class="flex flex-col items-stretch h-full overflow-hidden">
    <h3 class="font-bold text-2xl">Available pairs:</h3>
    <div class="mb-2">
      <InputText
        v-model="filterText"
        placeholder="Filter pairs..."
        class="w-full"
        autofocus
      />
    </div>
    <ul
      class="divide-y border-x border-surface-500 rounded-sm border-y divide-solid divide-surface-500 overflow-y-auto overflow-x-hidden"
      style="max-height: calc(100vh - 200px)"
    >
      <li
        v-for="pair in filteredPairs"
        :key="pair"
        button
        :class="{
          'bg-primary dark:border-primary text-primary-contrast': pair === selectedPair,
        }"
        class="flex justify-between items-center py-1 px-1"
        @click="selectPair(pair)"
      >
        <span>{{ pair }}</span>
      </li>
    </ul>
  </div>
</template>
