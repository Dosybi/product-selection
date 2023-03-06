<template>
  <div class="border w-1/2 flex gap-2 flex-wrap p-4">
    <div
      class="border w-fit p-1 rounded-xl cursor-pointer h-fit"
      v-for="item in items"
      :key="item.id"
    >
      <div @click="() => selectItem(item)">{{ item.name }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemsSection',
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  methods: {
    selectItem(item) {
      this.$emit('handle-selection', item)
    },
  },
}
</script>
