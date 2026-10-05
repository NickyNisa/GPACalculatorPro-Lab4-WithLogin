<template>
  <q-page class="q-pa-md" style="max-width: 900px; margin: 0 auto">
    <div class="row justify-end q-pt-sm">
      <q-btn color="negative" icon="logout" label="LOGOUT" @click="handleLogout" />
    </div>
    <div class="text-center q-mb-lg q-mt-md">
      <q-icon name="calculate" size="50px" color="primary" />
      <div class="text-h4 text-weight-bold q-mt-sm">GPA Calculator Pro</div>
      <div class="text-subtitle1 text-grey-6">ระบบคำนวณและบันทึกเกรดเฉลี่ยรายภาคเรียน</div>
    </div>
    <GpaForm @add-subject="addSubject" />
    <SubjectList
      :subjects="subjects"
      @delete-subject="deleteSubject"
      @clear-all="clearAllSubjects"
    />
    <SummaryCard :subjects="subjects" />
  </q-page>
</template>
<script setup>
import { ref } from 'vue'
import GpaForm from './GpaForm.vue'
import { useRouter } from 'vue-router'
import { useAuthStore } from '@/stores/authStore.js'
import SubjectList from '@/components/SubjectList.vue'
import SummaryCard from '@/components/SummaryCard.vue'

const router = useRouter()
const authStore = useAuthStore()
const subjects = ref([])

const handleLogout = () => {
  authStore.logout()
  router.push('/login')
}

const addSubject = (newSubject) => {
  subjects.value.push(newSubject)
}

const deleteSubject = (index) => {
  subjects.value.splice(index, 1)
}

const clearAllSubjects = () => {
  subjects.value = []
}
</script>
