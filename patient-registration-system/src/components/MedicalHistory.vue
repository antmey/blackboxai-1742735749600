<template>
  <div class="space-y-8">
    <!-- Disease History -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Riwayat Penyakit</h2>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Riwayat Penyakit</label>
          <select 
            :value="modelValue.diseaseHistory"
            @change="updateDiseaseHistory($event.target.value)"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            multiple
          >
            <option value="diabetes">Diabetes</option>
            <option value="hypertension">Hipertensi</option>
            <option value="heart_disease">Penyakit Jantung</option>
            <option value="asthma">Asma</option>
            <option value="tuberculosis">Tuberculosis</option>
            <option value="other">Lainnya</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Riwayat Penyakit Keluarga</label>
          <div class="flex items-center space-x-2">
            <select 
              :value="modelValue.familyDiseaseHistory"
              @change="updateFamilyDiseaseHistory($event.target.value)"
              class="flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              multiple
            >
              <option value="diabetes">Diabetes</option>
              <option value="hypertension">Hipertensi</option>
              <option value="heart_disease">Penyakit Jantung</option>
              <option value="cancer">Kanker</option>
              <option value="other">Lainnya</option>
            </select>
            <button 
              type="button"
              class="p-2 text-blue-600 hover:bg-blue-50 rounded-md"
              @click="addFamilyHistory"
            >
              <i class="fas fa-plus"></i>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Allergies -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Riwayat Alergi</h2>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Riwayat Alergi Obat</label>
          <div class="flex space-x-2">
            <input 
              type="text"
              v-model="newDrugAllergy"
              class="flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              placeholder="Masukkan nama obat"
            >
            <button 
              type="button"
              class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700"
              @click="addDrugAllergy"
            >
              Tambah
            </button>
          </div>
          <div class="mt-2 flex flex-wrap gap-2">
            <span 
              v-for="(allergy, index) in modelValue.drugAllergies" 
              :key="index"
              class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full flex items-center space-x-2"
            >
              <span>{{ allergy }}</span>
              <button 
                type="button"
                class="text-blue-600 hover:text-blue-800"
                @click="removeDrugAllergy(index)"
              >
                <i class="fas fa-times"></i>
              </button>
            </span>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Riwayat Alergi Lainnya</label>
          <textarea 
            :value="modelValue.otherAllergies"
            @input="updateOtherAllergies($event.target.value)"
            rows="3"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
            placeholder="Masukkan riwayat alergi lainnya..."
          ></textarea>
        </div>
      </div>
    </div>

    <!-- Current Medications -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Obat yang Sedang Dikonsumsi</h2>
      <div class="space-y-4">
        <div>
          <div class="flex space-x-2">
            <input 
              type="text"
              v-model="newMedication"
              class="flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              placeholder="Masukkan nama obat"
            >
            <button 
              type="button"
              class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700"
              @click="addMedication"
            >
              Tambah
            </button>
          </div>
          <div class="mt-2 flex flex-wrap gap-2">
            <span 
              v-for="(medication, index) in modelValue.currentMedications" 
              :key="index"
              class="px-3 py-1 bg-green-100 text-green-800 rounded-full flex items-center space-x-2"
            >
              <span>{{ medication }}</span>
              <button 
                type="button"
                class="text-green-600 hover:text-green-800"
                @click="removeMedication(index)"
              >
                <i class="fas fa-times"></i>
              </button>
            </span>
          </div>
        </div>
      </div>
    </div>

    <!-- Fall Risk Assessment -->
    <div>
      <h2 class="text-xl font-semibold text-gray-700 mb-4">Skala Risiko Jatuh (Opsional)</h2>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Cara berjalan pasien:</label>
          <div class="space-y-2">
            <label class="flex items-center space-x-2">
              <input 
                type="radio" 
                :checked="modelValue.walkingAbility === 'normal'"
                @change="updateWalkingAbility('normal')"
                class="text-blue-600"
              >
              <span>Normal - tidak sempoyongan, seimbang</span>
            </label>
            <label class="flex items-center space-x-2">
              <input 
                type="radio" 
                :checked="modelValue.walkingAbility === 'impaired'"
                @change="updateWalkingAbility('impaired')"
                class="text-blue-600"
              >
              <span>Tidak seimbang / sempoyongan / pusing</span>
            </label>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Menopang saat akan duduk:</label>
          <div class="space-y-2">
            <label class="flex items-center space-x-2">
              <input 
                type="radio" 
                :checked="modelValue.sittingSupport === 'no'"
                @change="updateSittingSupport('no')"
                class="text-blue-600"
              >
              <span>Tidak</span>
            </label>
            <label class="flex items-center space-x-2">
              <input 
                type="radio" 
                :checked="modelValue.sittingSupport === 'yes'"
                @change="updateSittingSupport('yes')"
                class="text-blue-600"
              >
              <span>Ya, tampak memegang pinggiran kursi atau meja/benda lain sebagai penopang</span>
            </label>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface MedicalHistoryData {
  diseaseHistory: string[]
  familyDiseaseHistory: string[]
  drugAllergies: string[]
  otherAllergies: string
  currentMedications: string[]
  walkingAbility: 'normal' | 'impaired' | ''
  sittingSupport: 'yes' | 'no' | ''
}

const props = defineProps<{
  modelValue: MedicalHistoryData
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: MedicalHistoryData): void
}>()

const newDrugAllergy = ref('')
const newMedication = ref('')

const updateField = <K extends keyof MedicalHistoryData>(
  field: K,
  value: MedicalHistoryData[K]
) => {
  emit('update:modelValue', {
    ...props.modelValue,
    [field]: value
  })
}

const updateDiseaseHistory = (value: string[]) => {
  updateField('diseaseHistory', value)
}

const updateFamilyDiseaseHistory = (value: string[]) => {
  updateField('familyDiseaseHistory', value)
}

const updateOtherAllergies = (value: string) => {
  updateField('otherAllergies', value)
}

const updateWalkingAbility = (value: 'normal' | 'impaired') => {
  updateField('walkingAbility', value)
}

const updateSittingSupport = (value: 'yes' | 'no') => {
  updateField('sittingSupport', value)
}

const addDrugAllergy = () => {
  if (newDrugAllergy.value.trim()) {
    updateField('drugAllergies', [...props.modelValue.drugAllergies, newDrugAllergy.value.trim()])
    newDrugAllergy.value = ''
  }
}

const removeDrugAllergy = (index: number) => {
  const newAllergies = [...props.modelValue.drugAllergies]
  newAllergies.splice(index, 1)
  updateField('drugAllergies', newAllergies)
}

const addMedication = () => {
  if (newMedication.value.trim()) {
    updateField('currentMedications', [...props.modelValue.currentMedications, newMedication.value.trim()])
    newMedication.value = ''
  }
}

const removeMedication = (index: number) => {
  const newMedications = [...props.modelValue.currentMedications]
  newMedications.splice(index, 1)
  updateField('currentMedications', newMedications)
}

const addFamilyHistory = () => {
  // Implementation for adding family history
}
</script>