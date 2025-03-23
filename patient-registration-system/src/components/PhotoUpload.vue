<template>
  <div class="flex items-center space-x-4">
    <div 
      class="w-32 h-32 bg-gray-100 rounded-lg flex items-center justify-center border-2 border-dashed border-gray-300 cursor-pointer overflow-hidden"
      @click="triggerFileInput"
    >
      <div v-if="!preview" class="text-center">
        <i class="fas fa-camera text-gray-400 text-2xl mb-2"></i>
        <p class="text-sm text-gray-500">Upload Foto</p>
      </div>
      <img v-else :src="preview" class="w-full h-full object-cover rounded-lg" alt="Preview" />
    </div>
    <input
      type="file"
      ref="fileInput"
      class="hidden"
      accept="image/*"
      @change="handleFileChange"
    >
    <div class="flex items-center">
      <input 
        type="checkbox" 
        id="newborn" 
        :value="modelValue"
        @input="$emit('update:modelValue', ($event.target as HTMLInputElement).checked)"
        class="mr-2"
      >
      <label for="newborn" class="text-gray-600">Bayi baru lahir</label>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

defineProps<{
  modelValue: boolean
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: boolean): void
  (e: 'photo-selected', file: File): void
}>()

const fileInput = ref<HTMLInputElement | null>(null)
const preview = ref<string | null>(null)

const triggerFileInput = () => {
  fileInput.value?.click()
}

const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement
  if (target.files && target.files[0]) {
    const file = target.files[0]
    
    // Create preview URL
    preview.value = URL.createObjectURL(file)
    
    // Emit the file
    emit('photo-selected', file)
  }
}
</script>