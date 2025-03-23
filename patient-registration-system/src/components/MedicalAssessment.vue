<template>
  <div class="space-y-8">
    <!-- Vital Signs -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Tanda-tanda Vital</h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Suhu Tubuh</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.temperature"
              @input="updateField('temperature', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              step="0.1"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">Celcius</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Nadi</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.pulse"
              @input="updateField('pulse', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">kali/menit</span>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Sistole</label>
            <div class="flex">
              <input 
                type="number" 
                :value="modelValue.systolic"
                @input="updateField('systolic', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              >
              <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">mmHg</span>
            </div>
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Diastole</label>
            <div class="flex">
              <input 
                type="number" 
                :value="modelValue.diastolic"
                @input="updateField('diastolic', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              >
              <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">mmHg</span>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Frekuensi Pernapasan</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.respiratoryRate"
              @input="updateField('respiratoryRate', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">kali/menit</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Saturasi Oksigen</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.oxygenSaturation"
              @input="updateField('oxygenSaturation', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              max="100"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">%</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Physical Examination -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Pemeriksaan Fisik</h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Lingkar Kepala</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.headCircumference"
              @input="updateField('headCircumference', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              step="0.1"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">cm</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Lingkar Perut</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.waistCircumference"
              @input="updateField('waistCircumference', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              step="0.1"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">cm</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Tinggi Badan</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.height"
              @input="updateField('height', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              step="0.1"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">cm</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Berat Badan</label>
          <div class="flex">
            <input 
              type="number" 
              :value="modelValue.weight"
              @input="updateField('weight', ($event.target as HTMLInputElement).value)"
              class="w-full px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              step="0.1"
            >
            <span class="px-3 py-2 bg-gray-100 border border-l-0 border-gray-300 rounded-r-md text-gray-500">kg</span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">IMT</label>
          <input 
            type="text" 
            :value="calculateBMI"
            disabled
            class="w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md text-gray-500"
          >
        </div>
      </div>
    </div>

    <!-- Health Data -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Data Kesehatan</h2>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Keluhan Utama *</label>
          <textarea 
            :value="modelValue.mainComplaint"
            @input="updateField('mainComplaint', ($event.target as HTMLTextAreaElement).value)"
            rows="3"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            placeholder="Keluhan utama..."
          ></textarea>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Keluhan Tambahan</label>
          <textarea 
            :value="modelValue.additionalComplaints"
            @input="updateField('additionalComplaints', ($event.target as HTMLTextAreaElement).value)"
            rows="3"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            placeholder="Keluhan tambahan..."
          ></textarea>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Status Perawat</label>
          <select 
            :value="modelValue.nursingStatus"
            @change="updateField('nursingStatus', ($event.target as HTMLSelectElement).value)"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          >
            <option value="">Pilih Status Perawat</option>
            <option value="outpatient">Rawat Jalan</option>
            <option value="inpatient">Rawat Inap</option>
            <option value="emergency">Gawat Darurat</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface MedicalData {
  // Vital Signs
  temperature: number
  pulse: number
  systolic: number
  diastolic: number
  respiratoryRate: number
  oxygenSaturation: number
  
  // Physical Examination
  headCircumference: number
  waistCircumference: number
  height: number
  weight: number
  
  // Health Data
  mainComplaint: string
  additionalComplaints: string
  nursingStatus: string
}

const props = defineProps<{
  modelValue: MedicalData
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: MedicalData): void
}>()

const updateField = (field: keyof MedicalData, value: string | number) => {
  emit('update:modelValue', {
    ...props.modelValue,
    [field]: value
  })
}

const calculateBMI = computed(() => {
  if (props.modelValue.height && props.modelValue.weight) {
    const heightInMeters = props.modelValue.height / 100
    const bmi = props.modelValue.weight / (heightInMeters * heightInMeters)
    return bmi.toFixed(1)
  }
  return ''
})
</script>