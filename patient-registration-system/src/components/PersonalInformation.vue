<template>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
    <!-- Full Name -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Nama Lengkap *</label>
      <input 
        type="text" 
        :value="modelValue.fullName"
        @input="updateField('fullName', ($event.target as HTMLInputElement).value)"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      >
    </div>

    <!-- Phone Numbers -->
    <div class="grid grid-cols-2 gap-4">
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Nomor Telepon Seluler *</label>
        <div class="flex">
          <select 
            :value="modelValue.mobilePrefix"
            @change="updateField('mobilePrefix', ($event.target as HTMLSelectElement).value)"
            class="w-20 px-2 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          >
            <option value="+62">+62</option>
          </select>
          <input 
            type="tel"
            :value="modelValue.mobile"
            @input="updateField('mobile', ($event.target as HTMLInputElement).value)"
            class="flex-1 px-3 py-2 border border-l-0 border-gray-300 rounded-r-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          >
        </div>
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Nomor Telepon Rumah</label>
        <input 
          type="tel"
          :value="modelValue.homePhone"
          @input="updateField('homePhone', ($event.target as HTMLInputElement).value)"
          class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
      </div>
    </div>

    <!-- Email -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
      <input 
        type="email"
        :value="modelValue.email"
        @input="updateField('email', ($event.target as HTMLInputElement).value)"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      >
    </div>

    <!-- Gender -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Jenis Kelamin *</label>
      <select 
        :value="modelValue.gender"
        @change="updateField('gender', ($event.target as HTMLSelectElement).value)"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      >
        <option value="">Pilih</option>
        <option value="male">Laki-laki</option>
        <option value="female">Perempuan</option>
      </select>
    </div>

    <!-- Birth Place -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Tempat Lahir</label>
      <input 
        type="text"
        :value="modelValue.birthPlace"
        @input="updateField('birthPlace', ($event.target as HTMLInputElement).value)"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      >
    </div>

    <!-- Birth Date -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">Tanggal Lahir *</label>
      <input 
        type="date"
        :value="modelValue.birthDate"
        @input="updateField('birthDate', ($event.target as HTMLInputElement).value)"
        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      >
    </div>
  </div>
</template>

<script setup lang="ts">
interface PersonalInfo {
  fullName: string
  mobilePrefix: string
  mobile: string
  homePhone: string
  email: string
  gender: string
  birthPlace: string
  birthDate: string
}

const props = defineProps<{
  modelValue: PersonalInfo
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: PersonalInfo): void
}>()

const updateField = (field: keyof PersonalInfo, value: string) => {
  emit('update:modelValue', {
    ...props.modelValue,
    [field]: value
  })
}
</script>