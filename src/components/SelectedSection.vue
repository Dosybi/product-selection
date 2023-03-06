<template>
  <div v-if="!preview" class="border w-1/2 lg:w-1/4 flex gap-1 flex-wrap p-4">
    <div
      class="border w-fit p-1 rounded-xl h-fit"
      v-for="item in items"
      :key="item.id"
    >
      <div class="cursor-pointer" @click="() => deleteItem(item)">
        {{ item.name }}
      </div>
    </div>
  </div>
  <div
    v-else
    class="border w-1/2 lg:w-1/4 flex gap-1 flex-wrap p-4 justify-center items-center"
  >
    <div class="p-1 text-2xl uppercase font-bold">
      {{ preview }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'SelectedSection',
  props: {
    items: {
      type: Array,
      required: false,
    },
    preview: {
      type: String,
      required: false,
    },
  },

  methods: {
    deleteItem(item) {
      this.$emit('handle-deletion', item)
    },
  },
}
</script>
