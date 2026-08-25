<template>
  <div class="min-h-screen w-full bg-black text-white font-sans flex flex-col md:flex-row" dir="ltr">
    <LoginView v-if="!isAuthenticated" @login-success="isAuthenticated = true" />

    <template v-else>
      <AppSidebar :navItems="navItems" :activeTab="activeTab" @update:activeTab="activeTab = $event"
        @logout="isAuthenticated = false" />

      <main class="flex-1 flex flex-col min-w-0 overflow-y-auto p-4 md:p-8 space-y-6 bg-black">
        <AppHeader :userName="userName" />

        <OverviewView v-if="activeTab === 'Overview'" @navigate="activeTab = $event" />
        <DemandView v-else-if="activeTab === 'Demand Intelligence'" />
        <CapabilityMapView v-else-if="activeTab === 'National Capability Map'" />
        <SmartPoolView v-else-if="activeTab === 'Smart Pool'" @navigate="activeTab = $event" />
        <GrowthOpportunitiesView v-else-if="activeTab === 'Growth Opportunities'" />
      </main>
    </template>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import LoginView from './views/LoginView.vue'
import AppSidebar from './components/Sidebar.vue'
import AppHeader from './components/Header.vue'
import OverviewView from './views/OverviewView.vue'
import DemandView from './views/DemandView.vue'
import CapabilityMapView from './views/CapabilityMapView.vue'
import SmartPoolView from './views/SmartPoolView.vue'
import GrowthOpportunitiesView from './views/GrowthOpportunitiesView.vue'

const isAuthenticated = ref(false)
const activeTab = ref('Overview')
const userEmail = ref('hassan.emara@example.com')

const userName = computed(() => {
  if (!userEmail.value) return 'User'
  const namePart = userEmail.value.split('@')[0]
  return namePart.split('.').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ')
})

const navItems = ['Overview', 'Demand Intelligence', 'National Capability Map', 'Smart Pool', 'Growth Opportunities']
</script>

<style>
body {
  margin: 0;
  background-color: #000000;
}
</style>