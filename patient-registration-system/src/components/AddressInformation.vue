<template>
  <div class="space-y-4">
    <!-- Village -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Desa/Kelurahan</label>
      <input 
        type="text" 
        v-model="form.village"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" 
        placeholder="Cari desa atau kelurahan..."
      >
    </div>

    <!-- Full Address -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Alamat Lengkap *</label>
      <textarea 
        v-model="form.address"
        rows="3"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      ></textarea>
    </div>

    <!-- RT/RW/Postal Code -->
    <div class="grid grid-cols-3 gap-4">
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">RT</label>
        <input 
          type="text"
          v-model="form.rt"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">RW</label>
        <input 
          type="text"
          v-model="form.rw"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Kode Pos</label>
        <input 
          type="text"
          v-model="form.postalCode"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface AddressInfo {
  village: string
  address: string
  rt: string
  rw: string
  postalCode: string
}

const props = defineProps<{
  modelValue: AddressInfo
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: AddressInfo): void
}>()

const form = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value)
})
</script>