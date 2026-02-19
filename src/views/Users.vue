<template>
  <div class="pa-6">
    <div class="d-flex align-center mb-1">
      <v-icon size="32" color="#0078D4" class="mr-2">mdi-account-group-outline</v-icon>
      <div>
        <h2 class="text-h5 font-weight-bold mb-0">Users</h2>
        <p class="text-caption opacity-70">Search and manage users</p>
      </div>
    </div>

    <v-divider class="mb-5"></v-divider>

    <!-- SEARCH CARD -->
    <v-card elevation="2" class="rounded-lg pa-4 mb-4">
      <v-text-field
        v-model="search"
        density="compact"
        variant="outlined"
        rounded="lg"
        placeholder="Search Users"
        prepend-inner-icon="mdi-magnify"
        hide-details
      />
    </v-card>

    <!-- USER LIST -->
    <v-card elevation="2" class="rounded-lg">
      <v-table density="comfortable">
        <thead>
          <tr class="text-caption font-weight-medium">
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Last Login</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="u in filteredUsers"
            :key="u.id"
            class="user-row"
            @click="$router.push(`/user/${u.id}`)"
          >
            <td>{{ u.id }}</td>
            <td>{{ u.name }}</td>
            <td>{{ u.email }}</td>
            <td>{{ u.lastLogin }}</td>
          </tr>
        </tbody>
      </v-table>
    </v-card>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import bus from '../styles/eventBus'

const search = ref('')
const users = ref([
  { id: 1, name: "Clark Kent", email: "clark@dailyplanet.com", lastLogin: "11:02 AM" },
  { id: 2, name: "Bruce Wayne", email: "bruce@wayne.com", lastLogin: "Yesterday" },
  { id: 3, name: "Diana Prince", email: "diana@amazon.com", lastLogin: "09:45 AM" },
  { id: 4, name: "Steve", email: "clark@dailyplanet.com", lastLogin: "11:02 AM" },
  { id: 5, name: "Stark", email: "bruce@wayne.com", lastLogin: "Yesterday" },
  { id: 6, name: "Clint", email: "diana@amazon.com", lastLogin: "09:45 AM" },
  { id: 7, name: "Natasha", email: "clark@dailyplanet.com", lastLogin: "11:02 AM" },
  { id: 8, name: "Banner", email: "bruce@wayne.com", lastLogin: "Yesterday" },
  { id: 9, name: "Wanda", email: "diana@amazon.com", lastLogin: "09:45 AM" },
  { id: 10, name: "Thor", email: "clark@dailyplanet.com", lastLogin: "11:02 AM" },
  { id: 11, name: "Loki", email: "bruce@wayne.com", lastLogin: "Yesterday" },
  { id: 12, name: "T'chala", email: "diana@amazon.com", lastLogin: "09:45 AM" }
])

// ✅ Filter users based on search
const filteredUsers = computed(() => {
  return users.value.filter(u =>
    u.name.toLowerCase().includes(search.value.toLowerCase()) ||
    u.email.toLowerCase().includes(search.value.toLowerCase())
  )
})
</script>

<style scoped>
.user-row {
  cursor: pointer;
}
.user-row:hover {
  background: #f3f7ff;
}
</style>
