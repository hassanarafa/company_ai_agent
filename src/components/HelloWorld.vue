<template>
  <div class="min-h-screen bg-slate-100 text-slate-800 font-sans flex flex-col md:flex-row" dir="ltr">

    <div class="md:hidden bg-slate-950 text-white p-4 flex justify-between items-center border-b border-slate-800">
      <div class="flex items-center gap-2">
        <span class="text-xl font-black tracking-wider">P<span class="text-emerald-500">OOL</span></span>
        <span class="text-[10px] text-slate-400 border border-slate-700 px-1.5 py-0.5 rounded">Supply Network</span>
      </div>
      <button @click="mobileMenuOpen = !mobileMenuOpen" class="text-slate-300 focus:outline-none p-1">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
      </button>
    </div>

    <aside :class="[
      'fixed inset-y-0 left-0 z-50 w-64 bg-slate-950 text-slate-300 flex flex-col justify-between border-r border-slate-800 transition-transform duration-300 ease-in-out md:static md:translate-x-0',
      mobileMenuOpen ? 'translate-x-0' : '-translate-x-full'
    ]">
      <div>
        <div class="p-6 hidden md:flex items-center gap-2">
          <span class="text-xl font-black text-white tracking-wider">P<span class="text-emerald-500">OOL</span></span>
          <span class="text-[10px] text-slate-400 border border-slate-700 px-1.5 py-0.5 rounded">Supply Network</span>
        </div>

        <div class="p-4 flex justify-between items-center md:hidden border-b border-slate-900">
          <span class="font-bold text-white">Menu</span>
          <button @click="mobileMenuOpen = false" class="text-slate-400 hover:text-white">✕</button>
        </div>

        <nav class="mt-4 px-3 space-y-1">
          <a href="#"
            class="flex items-center gap-3 px-4 py-3 bg-emerald-500/10 text-emerald-400 font-medium rounded-xl border border-emerald-500/20">
            <span>📊</span> Dashboard
          </a>
          <a href="#"
            class="flex items-center gap-3 px-4 py-3 hover:bg-slate-900 text-slate-400 hover:text-white rounded-xl transition">
            <span>➕</span> New Demand
          </a>
          <a href="#"
            class="flex items-center gap-3 px-4 py-3 hover:bg-slate-900 text-slate-400 hover:text-white rounded-xl transition">
            <span>🏢</span> Suppliers
          </a>
          <a href="#"
            class="flex items-center gap-3 px-4 py-3 hover:bg-slate-900 text-slate-400 hover:text-white rounded-xl transition">
            <span>📦</span> Orders
          </a>
          <a href="#"
            class="flex items-center gap-3 px-4 py-3 hover:bg-slate-900 text-slate-400 hover:text-white rounded-xl transition">
            <span>⚡</span> POOL Score
          </a>
          <a href="#"
            class="flex items-center justify-between px-4 py-3 hover:bg-slate-900 text-slate-400 hover:text-white rounded-xl transition">
            <span class="flex items-center gap-3">🤖 Ask POOL</span>
            <span class="bg-indigo-600 text-white text-[10px] px-1.5 py-0.5 rounded-full font-bold">Beta</span>
          </a>
        </nav>
      </div>

      <div class="p-4 border-t border-slate-900 flex items-center justify-between">
        <div class="flex items-center gap-3">
          <div
            class="w-10 h-10 rounded-full bg-slate-800 flex items-center justify-center font-bold text-white shrink-0">
            AH</div>
          <div class="overflow-hidden">
            <h4 class="text-xs font-bold text-white truncate">Ahmed Al-Harthi</h4>
            <p class="text-[10px] text-slate-400 truncate">Procurement Manager</p>
          </div>
        </div>
      </div>
    </aside>

    <div v-if="mobileMenuOpen" @click="mobileMenuOpen = false" class="fixed inset-0 bg-black/50 z-40 md:hidden"></div>

    <main class="flex-1 flex flex-col min-w-0 overflow-y-auto">

      <header
        class="bg-white border-b border-slate-200 p-4 md:px-8 md:py-4 flex flex-col md:flex-row justify-between items-start md:items-center gap-4 shadow-xs">
        <div>
          <h1 class="text-lg md:text-xl font-bold text-slate-900">Welcome back, Ahmed 👋</h1>
          <p class="text-xs text-slate-500">Here's what's happening with your supply network today.</p>
        </div>
        <div class="flex items-center gap-3 w-full md:w-auto">
          <input type="text" placeholder="Search suppliers, orders, products..."
            class="bg-slate-50 border border-slate-200 rounded-xl px-4 py-2 text-xs w-full md:w-64 focus:outline-none focus:border-emerald-500">
          <div class="bg-slate-50 border border-slate-200 px-3 py-2 rounded-xl text-xs font-semibold shrink-0">
            <span>PIF Company</span>
          </div>
        </div>
      </header>

      <div class="p-4 md:p-8 space-y-6">

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
          <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-xs">
            <p class="text-xs text-slate-500 font-medium">Active Orders</p>
            <div class="flex justify-between items-baseline mt-2">
              <h3 class="text-2xl font-bold text-slate-900">24</h3>
              <span class="text-xs text-emerald-600 font-bold bg-emerald-50 px-2 py-0.5 rounded">+15% vs last
                month</span>
            </div>
          </div>
          <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-xs">
            <p class="text-xs text-slate-500 font-medium">Demand Fulfilled</p>
            <div class="flex justify-between items-baseline mt-2">
              <h3 class="text-2xl font-bold text-slate-900">91%</h3>
              <span class="text-xs text-emerald-600 font-bold bg-emerald-50 px-2 py-0.5 rounded">+7% vs last
                month</span>
            </div>
          </div>
          <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-xs">
            <p class="text-xs text-slate-500 font-medium">Active Suppliers</p>
            <div class="flex justify-between items-baseline mt-2">
              <h3 class="text-2xl font-bold text-slate-900">68</h3>
              <span class="text-xs text-emerald-600 font-bold bg-emerald-50 px-2 py-0.5 rounded">+8 vs last month</span>
            </div>
          </div>
          <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-xs">
            <p class="text-xs text-slate-500 font-medium">At Risk</p>
            <div class="flex justify-between items-baseline mt-2">
              <h3 class="text-2xl font-bold text-rose-600">3</h3>
              <span class="text-xs text-rose-600 font-bold bg-rose-50 px-2 py-0.5 rounded">-2 vs last month</span>
            </div>
          </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">

          <div class="lg:col-span-2 bg-white p-5 md:p-6 rounded-2xl border border-slate-200 shadow-xs space-y-6">
            <div
              class="flex flex-col sm:flex-row justify-between items-start sm:items-center border-b border-slate-100 pb-4 gap-3">
              <div>
                <div class="flex flex-wrap items-center gap-2">
                  <h2 class="font-bold text-slate-900">Active Order</h2>
                  <span
                    class="text-xs font-bold text-emerald-700 bg-emerald-100 px-2.5 py-0.5 rounded-full">POOL-124</span>
                  <span class="text-xs text-emerald-600 bg-emerald-50 px-2 py-0.5 rounded font-medium">On Track</span>
                </div>
                <p class="text-xs text-slate-500 mt-1">Building Materials Inventory • Created on 12 May 2024</p>
              </div>
              <button
                class="bg-slate-900 text-white text-xs px-4 py-2 rounded-xl font-medium hover:bg-slate-800 transition">View
                Details →</button>
            </div>

            <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 text-xs">
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-100">
                <span class="text-slate-500">Required</span>
                <p class="text-sm md:text-base font-bold text-slate-900 mt-1">100,000 units</p>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-100">
                <span class="text-slate-500">Allocated</span>
                <p class="text-sm md:text-base font-bold text-emerald-600 mt-1">100,000 ✓</p>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-100">
                <span class="text-slate-500">Delivered</span>
                <p class="text-sm md:text-base font-bold text-slate-900 mt-1">42%</p>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-100">
                <span class="text-slate-500">Total Cost</span>
                <p class="text-sm md:text-base font-bold text-slate-900 mt-1">SAR 8.24M</p>
              </div>
            </div>

            <div class="bg-slate-50 p-4 md:p-5 rounded-xl border border-slate-200 mt-4 space-y-3">
              <h3 class="font-bold text-xs text-slate-800">AI Inventory & Quota Verification Agent</h3>
              <form @submit.prevent="submitOrder" class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                <select v-model="form.company"
                  class="bg-white border border-slate-200 rounded-lg p-2.5 text-xs text-slate-800">
                  <option>Al-Noor Contracting Co.</option>
                  <option>Modern Building Co.</option>
                </select>
                <select v-model="form.material"
                  class="bg-white border border-slate-200 rounded-lg p-2.5 text-xs text-slate-800">
                  <option value="Sand">Sand (Cubic Meters)</option>
                  <option value="Gravel">Gravel (Cubic Meters)</option>
                </select>
                <input type="number" v-model="form.qty" placeholder="Requested Qty"
                  class="bg-white border border-slate-200 rounded-lg p-2.5 text-xs text-slate-800">
                <button type="submit" :disabled="loading"
                  class="sm:col-span-3 bg-emerald-600 hover:bg-emerald-500 text-white font-bold py-3 rounded-lg text-xs transition shadow-sm">
                  {{ loading ? 'Verifying with AI Agent...' : 'Inspect and Approve Order' }}
                </button>
              </form>

              <div v-if="agentResponse"
                class="mt-3 p-3 bg-white border border-emerald-200 rounded-lg text-xs text-slate-700">
                <strong class="text-emerald-700">AI Decision:</strong> {{ agentResponse }}
              </div>
            </div>

          </div>

          <div class="space-y-6">
            <div class="bg-rose-50 border border-rose-200 p-5 rounded-2xl shadow-xs">
              <div class="flex items-center gap-2 text-rose-700 font-bold text-xs mb-1">
                <span>⚠️</span> Supply Risk Detected
              </div>
              <p class="text-xs text-slate-600">Supplier C is projected to be 6 days late.</p>

              <div class="mt-4 bg-white p-4 rounded-xl border border-rose-100 space-y-3">
                <h4 class="text-xs font-bold text-slate-900">POOL Recommendation</h4>
                <p class="text-[11px] text-slate-500">Move 10,000 units from Supplier C to Supplier B to protect the
                  required delivery date.</p>
                <button
                  class="w-full bg-slate-900 text-white text-xs py-2.5 rounded-lg font-medium hover:bg-slate-800 transition">Review
                  Reallocation →</button>
              </div>
            </div>

            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-xs space-y-3">
              <div class="flex justify-between items-center">
                <h3 class="font-bold text-xs text-slate-900">Ask POOL</h3>
                <span class="text-[10px] bg-indigo-100 text-indigo-700 font-bold px-2 py-0.5 rounded">Beta</span>
              </div>
              <div class="bg-slate-50 p-2.5 rounded-xl text-xs text-slate-600 border border-slate-100">
                How can I help you today?
              </div>
              <div class="space-y-1 text-[11px] text-slate-500">
                <p class="bg-slate-50 p-2 rounded-lg border border-slate-100 hover:bg-slate-100 cursor-pointer">Find a
                  lower-risk option...</p>
                <p class="bg-slate-50 p-2 rounded-lg border border-slate-100 hover:bg-slate-100 cursor-pointer">Can we
                  fulfill 150,000 units instead?</p>
              </div>
              <div class="relative mt-2">
                <input type="text" placeholder="Type your question..."
                  class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:border-emerald-500">
                <span class="absolute right-3 top-2 text-emerald-600 font-bold cursor-pointer">➔</span>
              </div>
            </div>

          </div>

        </div>

      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const mobileMenuOpen = ref(false)
const form = ref({
  company: 'Al-Noor Contracting Co.',
  material: 'Sand',
  qty: ''
})

const loading = ref(false)
const agentResponse = ref('')

const submitOrder = async () => {
  if (!form.value.qty) return
  loading.value = true
  agentResponse.value = ''

  setTimeout(() => {
    agentResponse.value = `Order reviewed successfully for [${form.value.company}]. The requested quantity (${form.value.qty} m³ of ${form.value.material}) is within quota limits and available in stock. Approved automatically.`
    loading.value = false
  }, 1500)
}
</script>