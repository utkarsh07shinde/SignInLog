<template>
  <div class="resources-page">

    <h2 class="title">Resources</h2>
    <p class="subtitle">List of all resources</p>

    <v-card class="mt-6 pa-6" elevation="1">

      <!-- FILTER BAR -->
      <div class="filter-bar">
        <v-text-field
          placeholder="Search resources..."
          prepend-inner-icon="mdi-magnify"
          hide-details
          density="compact"
          class="mr-4"
        ></v-text-field>

        <v-select
          label="Type"
          :items="['All', 'VM', 'Storage', 'DB']"
          hide-details
          density="compact"
          class="mr-4"
        ></v-select>

        <v-btn color="#0078D4" variant="flat">
          <v-icon left>mdi-refresh</v-icon>
          Refresh
        </v-btn>
      </div>

      <!-- TABLE -->
      <v-data-table
        :headers="headers"
        :items="items"
        class="mt-6"
        hover
      ></v-data-table>

    </v-card>

  </div>
</template>

<script setup>
const headers = [
  { title: "Name", key: "name" },
  { title: "Type", key: "type" },
  { title: "Region", key: "region" },
  { title: "Status", key: "status" }
]

const items = [
  { name: "VM-01", type: "VM", region: "US", status: "Running" },
  { name: "DB-Production", type: "DB", region: "Europe", status: "Online" },
  { name: "Storage-01", type: "Storage", region: "Canada", status: "Active" },
  { name: "Web-01", type: "VM", region: "US", status: "Running" },
  { name: "LoadBalancer-01", type: "DB", region: "Europe", status: "Online" },
  { name: "Firewall-01", type: "Storage", region: "Canada", status: "Active" },
  { name: "backup", type: "VM", region: "US", status: "Running" },
  { name: "Cdn-01", type: "DB", region: "Europe", status: "Online" },
  { name: "Storage-01", type: "Storage", region: "Canada", status: "Active" },
  { name: "VM-02", type: "VM", region: "US", status: "Running" },
  { name: "DB-Production", type: "DB", region: "Europe", status: "Online" },
  { name: "Storage-02", type: "Storage", region: "Canada", status: "Active" }
]
</script>

<style scoped>
.resources-page {
  padding: 20px;
}

.title {
  font-size: 22px;
  font-weight: 600;
}

.subtitle {
  color: #666;
  font-size: 14px;
}

.filter-bar {
  display: flex;
  align-items: center;
}
</style>
