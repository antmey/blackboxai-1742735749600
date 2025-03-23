<template>
  <div class="min-h-screen py-8 px-4">
    <div class="max-w-6xl mx-auto bg-white rounded-lg shadow-md p-6">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">Data Pasien</h1>
      
      <!-- Data Diri -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Data Diri</h2>
        <div class="space-y-4">
          <PhotoUpload
            v-model="isNewborn"
            @photo-selected="handlePhotoSelected"
          />
          <PersonalInformation
            v-model="personalInfo"
            :class="{ 'opacity-50 pointer-events-none': isNewborn }"
          />
        </div>
      </div>

      <!-- Alamat -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Alamat Identitas</h2>
        <AddressInformation
          v-model="addressInfo"
        />
      </div>

      <!-- Medical Assessment -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Pemeriksaan Medis</h2>
        <MedicalAssessment
          v-model="medicalInfo"
        />
      </div>

      <!-- Medical History -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Riwayat Medis</h2>
        <MedicalHistory
          v-model="historyInfo"
        />
      </div>

      <!-- Status Assessment -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold text-gray-700 mb-4">Penilaian Status</h2>
        <StatusAssessment
          v-model="statusInfo"
        />
      </div>

      <!-- Submit and Reset Buttons -->
      <div class="flex justify-end space-x-4">
        <FormButton
          type="button"
          @click="handleReset"
          class="bg-gray-500 hover:bg-gray-600"
        >
          Reset
        </FormButton>
        <FormButton
          :loading="isSubmitting"
          @click="submitForm"
        >
          Simpan
        </FormButton>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import PhotoUpload from './PhotoUpload.vue'
import PersonalInformation from './PersonalInformation.vue'
import AddressInformation from './AddressInformation.vue'
import MedicalAssessment from './MedicalAssessment.vue'
import MedicalHistory from './MedicalHistory.vue'
import StatusAssessment from './StatusAssessment.vue'
import FormButton from './FormButton.vue'

// State
const isNewborn = ref(false)
const isSubmitting = ref(false)
const selectedPhoto = ref<File | null>(null)

const personalInfo = reactive({
  fullName: '',
  mobilePrefix: '+62',
  mobile: '',
  homePhone: '',
  email: '',
  gender: '',
  birthPlace: '',
  birthDate: ''
})

const addressInfo = reactive({
  village: '',
  address: '',
  rt: '',
  rw: '',
  postalCode: ''
})

const medicalInfo = reactive({
  // Vital Signs
  temperature: 0,
  pulse: 0,
  systolic: 0,
  diastolic: 0,
  respiratoryRate: 0,
  oxygenSaturation: 0,
  
  // Physical Examination
  headCircumference: 0,
  waistCircumference: 0,
  height: 0,
  weight: 0,
  
  // Health Data
  mainComplaint: '',
  additionalComplaints: '',
  nursingStatus: ''
})

const historyInfo = reactive({
  diseaseHistory: [],
  familyDiseaseHistory: [],
  drugAllergies: [],
  otherAllergies: '',
  currentMedications: [],
  walkingAbility: '',
  sittingSupport: ''
})

const statusInfo = reactive({
  psychologicalStatus: '',
  economicStatus: '',
  spiritualStatus: '',
  vaccinations: []
})

// Methods
const handlePhotoSelected = (file: File) => {
  selectedPhoto.value = file
}

const validateForm = (): boolean => {
  // Required fields validation
  if (!personalInfo.fullName || !personalInfo.mobile || !personalInfo.gender || !personalInfo.birthDate) {
    alert('Mohon lengkapi data diri yang wajib diisi')
    return false
  }

  if (!addressInfo.address) {
    alert('Mohon lengkapi alamat lengkap')
    return false
  }

  if (!medicalInfo.mainComplaint) {
    alert('Mohon lengkapi keluhan utama')
    return false
  }

  return true
}

const handleReset = () => {
  // Reset all form data
  isNewborn.value = false
  selectedPhoto.value = null
  
  Object.assign(personalInfo, {
    fullName: '',
    mobilePrefix: '+62',
    mobile: '',
    homePhone: '',
    email: '',
    gender: '',
    birthPlace: '',
    birthDate: ''
  })

  Object.assign(addressInfo, {
    village: '',
    address: '',
    rt: '',
    rw: '',
    postalCode: ''
  })

  Object.assign(medicalInfo, {
    temperature: 0,
    pulse: 0,
    systolic: 0,
    diastolic: 0,
    respiratoryRate: 0,
    oxygenSaturation: 0,
    headCircumference: 0,
    waistCircumference: 0,
    height: 0,
    weight: 0,
    mainComplaint: '',
    additionalComplaints: '',
    nursingStatus: ''
  })

  Object.assign(historyInfo, {
    diseaseHistory: [],
    familyDiseaseHistory: [],
    drugAllergies: [],
    otherAllergies: '',
    currentMedications: [],
    walkingAbility: '',
    sittingSupport: ''
  })

  Object.assign(statusInfo, {
    psychologicalStatus: '',
    economicStatus: '',
    spiritualStatus: '',
    vaccinations: []
  })
}

const submitForm = async () => {
  try {
    if (!validateForm()) return

    isSubmitting.value = true
    
    // Prepare form data
    const formData = {
      isNewborn: isNewborn.value,
      photo: selectedPhoto.value,
      personalInfo,
      addressInfo,
      medicalInfo,
      historyInfo,
      statusInfo
    }

    // Here you would typically send the data to an API
    console.log('Form submitted:', formData)
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    alert('Data berhasil disimpan!')
    
    // Reset form after successful submission
    handleReset()
  } catch (error) {
    console.error('Error submitting form:', error)
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    isSubmitting.value = false
  }
}
</script>