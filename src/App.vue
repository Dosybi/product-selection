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

<script>
import { ref } from 'vue'
import { userItems, selectionItems } from '../data'
import ItemsSection from './components/ItemsSection.vue'
import SelectedSection from './components/SelectedSection.vue'

export default {
  name: 'IndexPage',
  components: { ItemsSection, SelectedSection },

  setup() {
    const userSelected = ref([])
    const previewSelected = ref('')

    const handleUserSelection = (data) => {
      if (userSelected.value.includes(data) || userSelected.value.length === 6)
        return

      userSelected.value.push(data)
      const newUserItems = userItems.filter((item) => item.id !== data.id)
      userItems.value = newUserItems
    }

    const handlePreviewSelection = (data) => {
      if (previewSelected.value.name === data.name) return

      previewSelected.value = data.name
    }

    const deleteItem = (item) => {
      userSelected.value = userSelected.value.filter(
        (selectedItem) => selectedItem.id !== item.id
      )
      userItems.value = [...userItems.value, item]
    }

    return {
      userItems,
      selectionItems,
      userSelected,
      previewSelected,
      handleUserSelection,
      handlePreviewSelection,
      deleteItem,
    }
  },
}
</script>
