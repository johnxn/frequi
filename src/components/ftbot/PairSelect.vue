<script setup lang="ts">
withDefaults(
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

const selectPair = (pair: string) => {
  emit('selectionChange', pair);
};
</script>

<template>
  <div class="flex flex-col items-stretch h-full overflow-hidden">
    <h3 class="font-bold text-2xl">Available pairs:</h3>
    <ul
      class="divide-y border-x border-surface-500 rounded-sm border-y divide-solid divide-surface-500 overflow-y-auto overflow-x-hidden"
      style="max-height: calc(100vh - 150px)"
    >
      <li
        v-for="pair in availablePairs"
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
