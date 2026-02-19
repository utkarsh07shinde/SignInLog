<template>
  <div class="dashboard">

    <!-- PAGE HEADER -->
    <div class="header">
      <h1 class="title">Admin Center</h1>
      <p class="subtitle">Overview of your system resources & activity</p>
    </div>

    <v-row dense class="mt-4">

      <!-- LEFT COLUMN -->
      <v-col cols="12" md="8">

        <!-- =================== -->
        <!-- RESOURCE OVERVIEW -->
        <!-- =================== -->
        <v-card elevation="1" class="pa-5 azure-card">
          <h3 class="section-title">Resource Overview</h3>

          <v-row dense>
            <v-col cols="12" md="4" v-for="item in resources" :key="item.label">
              <v-card class="metric-card pa-4" elevation="0">
                <v-icon size="28" :color="item.color">{{ item.icon }}</v-icon>
                <div class="metric-value">{{ item.value }}</div>
                <div class="metric-label">{{ item.label }}</div>
              </v-card>
            </v-col>
          </v-row>
        </v-card>

        <!-- =================== -->
        <!-- RECENT CHANGES -->
        <!-- =================== -->
        <v-card elevation="1" class="pa-5 mt-6 azure-card">
          <h3 class="section-title">Recent Changes</h3>

          <v-list density="comfortable">
            <v-list-item v-for="c in changes" :key="c.text">
              <v-list-item-avatar>
                <v-icon color="#0078D4">{{ c.icon }}</v-icon>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>{{ c.text }}</v-list-item-title>
                <v-list-item-subtitle>{{ c.time }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>

      </v-col>


      <!-- RIGHT COLUMN -->
      <v-col cols="12" md="4">

        <!-- =================== -->
        <!-- QUICK ACTIONS -->
        <!-- =================== -->
        <v-card elevation="1" class="pa-5 azure-card">
          <h3 class="section-title">Quick Actions</h3>

          <v-row dense class="mt-2">
            <v-col cols="6" v-for="action in quickActions" :key="action.label">
              <v-card class="quick-card pa-3" elevation="0" link clickable>
                <v-icon size="28" color="#0078D4">{{ action.icon }}</v-icon>
                <div class="quick-label">{{ action.label }}</div>
              </v-card>
            </v-col>
          </v-row>
        </v-card>

        <!-- =================== -->
        <!-- SYSTEM MONITOR -->
        <!-- =================== -->
        <v-card elevation="1" class="pa-5 mt-6 azure-card">
          <h3 class="section-title">System Monitor</h3>

          <v-progress-linear
            v-for="mon in monitor"
            :key="mon.label"
            class="mt-4"
            height="12"
            rounded
            :model-value="mon.value"
            :color="mon.color"
          ></v-progress-linear>

          <div
            v-for="mon in monitor"
            :key="mon.label + '-text'"
            class="monitor-label mt-1"
          >
            {{ mon.label }} – {{ mon.caption }}
          </div>
        </v-card>

      </v-col>

    </v-row>

  </div>
</template>

<script setup>
const resources = [
  { label: "Users", value: "124", icon: "mdi-account-group", color: "#0078D4" },
  { label: "Groups", value: "12", icon: "mdi-account-multiple-outline", color: "#4CAF50" },
  { label: "Roles", value: "8", icon: "mdi-shield-lock-outline", color: "#E53935" },
]

const changes = [
  { text: "Role 'Editor' updated", time: "5 min ago", icon: "mdi-pencil" },
  { text: "Group 'Admins' modified", time: "12 min ago", icon: "mdi-account-group" },
  { text: "User John updated details", time: "1 hour ago", icon: "mdi-account-edit" },
]

const quickActions = [
  { label: "Create User", icon: "mdi-account-plus" },
  { label: "Create Resource", icon: "mdi-plus-circle-outline" },
  { label: "Add Group", icon: "mdi-account-multiple-plus" },
  { label: "Settings", icon: "mdi-cog" },
]

const monitor = [
  { label: "CPU Load", value: 45, color: "#0078D4", caption: "Normal" },
  { label: "Memory Usage", value: 60, color: "#4CAF50", caption: "Stable" },
  { label: "Network Traffic", value: 30, color: "#FF9800", caption: "Light" },
]
</script>

<style scoped>
.dashboard { padding: 20px; }

.title {
  font-size: 26px;
  font-weight: 700;
}

.subtitle {
  color: #555;
  margin-top: 4px;
}

.section-title {
  font-size: 18px;
  font-weight: 600;
}

.azure-card {
  border-radius: 12px;
}

.metric-card {
  border-radius: 10px;
  background: #f4f7fb;
  text-align: center;
}

.metric-value {
  font-size: 24px;
  font-weight: 700;
}

.metric-label {
  font-size: 14px;
  color: #666;
}

.quick-card {
  border-radius: 10px;
  text-align: center;
  cursor: pointer;
  transition: background 0.2s;
}

.quick-card:hover {
  background: #eef4fb;
}

.quick-label {
  margin-top: 8px;
  font-size: 14px;
}

.monitor-label {
  font-size: 13px;
  color: #555;
}
</style>
