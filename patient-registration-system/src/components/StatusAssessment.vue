<template>
  <div class="space-y-8">
    <!-- Status Assessments -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <!-- Psychological Status -->
      <div>
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Status Psikologis</h2>
        <select 
          :value="modelValue.psychologicalStatus"
          @change="updateField('psychologicalStatus', $event.target.value)"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
          <option value="">Pilih Status Psikologis</option>
          <option value="cooperative">Kooperatif</option>
          <option value="anxious">Cemas</option>
          <option value="depressed">Depresi</option>
          <option value="aggressive">Agresif</option>
          <option value="withdrawn">Menarik Diri</option>
        </select>
      </div>

      <!-- Economic Status -->
      <div>
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Status Ekonomi</h2>
        <input 
          type="text"
          :value="modelValue.economicStatus"
          @input="updateField('economicStatus', ($event.target as HTMLInputElement).value)"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="Status ekonomi..."
        >
      </div>

      <!-- Spiritual Status -->
      <div>
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Status Spiritual</h2>
        <input 
          type="text"
          :value="modelValue.spiritualStatus"
          @input="updateField('spiritualStatus', ($event.target as HTMLInputElement).value)"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="Status spiritual..."
        >
      </div>
    </div>

    <!-- Vaccination History -->
    <div>
      <div class="flex items-center justify-between mb-4">
        <h2 class="text-xl font-semibold text-gray-700">Riwayat Vaksinasi</h2>
        <button 
          type="button"
          class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 flex items-center space-x-2"
          @click="addVaccination"
        >
          <i class="fas fa-plus"></i>
          <span>Tambah Riwayat Vaksinasi</span>
        </button>
      </div>

      <!-- Vaccination List -->
      <div class="space-y-4">
        <div 
          v-for="(vaccination, index) in modelValue.vaccinations" 
          :key="index"
          class="p-4 bg-gray-50 rounded-lg border border-gray-200"
        >
          <div class="flex justify-between items-start mb-4">
            <h3 class="font-medium text-gray-900">Vaksinasi #{{ index + 1 }}</h3>
            <button 
              type="button"
              class="text-red-600 hover:text-red-800"
              @click="removeVaccination(index)"
            >
              <i class="fas fa-trash"></i>
            </button>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Jenis Vaksin</label>
              <input 
                type="text"
                :value="vaccination.type"
                @input="updateVaccinationField(index, 'type', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                placeholder="Masukkan jenis vaksin"
              >
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Tanggal Vaksinasi</label>
              <input 
                type="date"
                :value="vaccination.date"
                @input="updateVaccinationField(index, 'date', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              >
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Batch Number</label>
              <input 
                type="text"
                :value="vaccination.batchNumber"
                @input="updateVaccinationField(index, 'batchNumber', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                placeholder="Masukkan nomor batch"
              >
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Lokasi Vaksinasi</label>
              <input 
                type="text"
                :value="vaccination.location"
                @input="updateVaccinationField(index, 'location', ($event.target as HTMLInputElement).value)"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                placeholder="Masukkan lokasi vaksinasi"
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Vaccination {
  type: string
  date: string
  batchNumber: string
  location: string
}

interface StatusData {
  psychologicalStatus: string
  economicStatus: string
  spiritualStatus: string
  vaccinations: Vaccination[]
}

const props = defineProps<{
  modelValue: StatusData
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: StatusData): void
}>()

const updateField = <K extends keyof StatusData>(
  field: K,
  value: StatusData[K]
) => {
  emit('update:modelValue', {
    ...props.modelValue,
    [field]: value
  })
}

const updateVaccinationField = (
  index: number,
  field: keyof Vaccination,
  value: string
) => {
  const newVaccinations = [...props.modelValue.vaccinations]
  newVaccinations[index] = {
    ...newVaccinations[index],
    [field]: value
  }
  updateField('vaccinations', newVaccinations)
}

const addVaccination = () => {
  const newVaccination: Vaccination = {
    type: '',
    date: '',
    batchNumber: '',
    location: ''
  }
  
  updateField('vaccinations', [...props.modelValue.vaccinations, newVaccination])
}

const removeVaccination = (index: number) => {
  const newVaccinations = [...props.modelValue.vaccinations]
  newVaccinations.splice(index, 1)
  updateField('vaccinations', newVaccinations)
}
</script>