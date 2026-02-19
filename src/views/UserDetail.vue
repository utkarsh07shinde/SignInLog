<template>
  <div class="pa-6">
    <div class="d-flex align-center mb-2">
      <v-icon size="32" color="#0078D4" class="mr-3">mdi-account-circle-outline</v-icon>
      <div>
        <h1 class="text-h5 font-weight-bold mb-0">User Details</h1>
        <p class="text-caption opacity-70">Manage user ID: {{ user.id }}</p>
      </div>
    </div>

    <v-divider class="my-4" />

    <v-card elevation="2" class="rounded-xl pa-5">
      <v-text-field v-model="user.name" label="Name" variant="outlined" class="mb-4" />
      <v-text-field v-model="user.email" label="Email" variant="outlined" class="mb-4" />

      <v-btn
        :loading="saving"
        color="#0078D4"
        variant="flat"
        class="rounded-lg px-4"
        @click="onSave"
      >
        Save Changes
      </v-btn>
    </v-card>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import bus from '../styles/eventBus'

const route = useRoute()
const saving = ref(false)

// Fake selected user data
const user = ref({
  id: route.params.id,
  name: "Clark Kent",
  email: "clark@dailyplanet.com",
  lastLogin: "11:02 AM"
})

// ✅ Save should trigger notification
const onSave = () => {
  saving.value = true
  const time = new Date().toLocaleTimeString()

  // Emit notification
  bus.emit('user-action', {
    title: `User Updated`,
    message: `${user.value.name} was updated`,
    time
  })

  saving.value = false
  saving.value = false
  // Toast handled in layout/topbar
  saving.value = false
}
</script>
