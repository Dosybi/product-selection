<script>
import { userItems, selectionItems } from '../data'
import ItemsSection from './components/ItemsSection.vue'
import SelectedSection from './components/SelectedSection.vue'

export default {
  name: 'IndexPage',
  components: { ItemsSection, SelectedSection },

  data() {
    return {
      userItems: userItems,
      selectionItems: selectionItems,
      userSelected: [],
      previewSelected: '',
    }
  },

  methods: {
    handleUserSelection(data) {
      const newUserSelectedItems = [...this.userSelected]

      if (
        newUserSelectedItems.includes(data) ||
        newUserSelectedItems.length === 6
      )
        return

      newUserSelectedItems.push(data)
      const newUserItems = this.userItems.filter((item) => item.id !== data.id)
      this.userSelected = newUserSelectedItems
      this.userItems = newUserItems
    },

    handlePreviewSelection(data) {
      let newPreviewSelected = this.previewSelected

      if (newPreviewSelected.name === data.name) return

      newPreviewSelected = data.name
      this.previewSelected = newPreviewSelected
    },

    deleteItem(item) {
      const newUserSelectedItems = [...this.userSelected].filter(
        (selectedItem) => selectedItem.id !== item.id
      )
      const newUserItems = [...this.userItems, item]

      this.userSelected = newUserSelectedItems
      this.userItems = newUserItems
    },
  },
}
</script>

<template>
  <main class="p-6">
    <div class="flex gap-1 justify-between">
      <SelectedSection :items="userSelected" @handle-deletion="deleteItem" />
      <SelectedSection :preview="previewSelected" />
    </div>
    <div class="flex gap-1">
      <ItemsSection
        :items="userItems"
        @handle-selection="handleUserSelection"
      />
      <ItemsSection
        :items="selectionItems"
        @handle-selection="handlePreviewSelection"
      />
    </div>
  </main>
</template>
