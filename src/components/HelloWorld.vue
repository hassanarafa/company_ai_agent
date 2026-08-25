<template>
  <div>
    <!-- LOGIN VIEW -->
    <div v-if="!isAuthenticated" class="min-h-screen bg-black flex items-center justify-center p-6 text-white"
      dir="ltr">
      <div class="max-w-md w-full bg-zinc-950 border border-zinc-800 p-8 rounded-2xl shadow-2xl space-y-6 relative">

        <div class="text-center">
          <h1 class="text-3xl font-black tracking-widest text-white mb-1">PO<span style="color: #38872c;">O</span>L</h1>
          <p class="text-[9px] tracking-widest uppercase font-bold" style="color: #38872c;">Connecting Demand to Local
            Capability</p>
        </div>

        <form @submit.prevent="handleLogin" class="space-y-4">
          <div>
            <label class="block text-xs font-medium text-zinc-400 mb-1">Email Address</label>
            <input type="email" v-model="loginForm.email" placeholder="name@example.com" required
              class="w-full bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition"
              @focus="$event.target.style.borderColor = '#38872c'" @blur="$event.target.style.borderColor = '#27272a'">
          </div>

          <div>
            <label class="block text-xs font-medium text-zinc-400 mb-1">Password</label>
            <input type="password" v-model="loginForm.password" placeholder="••••••••" required
              class="w-full bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition"
              @focus="$event.target.style.borderColor = '#38872c'" @blur="$event.target.style.borderColor = '#27272a'">
          </div>

          <!-- Feature Alert Draft over Login Button -->
          <div class="relative pt-3">
            <span
              class="absolute top-0 right-3 z-10 px-2 py-0.5 text-[8px] font-extrabold uppercase tracking-wider text-black rounded-full shadow-md animate-pulse"
              style="background-color: #38872c;">
              Secure Portal
            </span>
            <button type="submit" :disabled="loginLoading"
              class="w-full text-black font-extrabold py-3 rounded-xl text-xs transition disabled:opacity-50"
              style="background-color: #38872c; box-shadow: 0 4px 20px rgba(56, 135, 44, 0.35);">
              {{ loginLoading ? 'Authenticating...' : 'Sign In' }}
            </button>
          </div>
        </form>

        <p v-if="loginError" class="text-xs text-red-500 text-center">{{ loginError }}</p>
      </div>
    </div>

    <!-- MAIN DASHBOARD VIEW -->
    <div v-else class="min-h-screen bg-black text-white font-sans flex flex-col md:flex-row" dir="ltr">

      <!-- Mobile Top Bar -->
      <div class="md:hidden bg-zinc-950 text-white p-4 flex justify-between items-center border-b border-zinc-900">
        <div>
          <h1 class="font-black tracking-widest">PO<span style="color: #38872c;">O</span>L</h1>
          <p class="text-[8px] tracking-wider uppercase" style="color: #38872c;">Connecting Demand to Local Capability
          </p>
        </div>
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="text-zinc-300 focus:outline-none p-1">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
          </svg>
        </button>
      </div>

      <!-- Sidebar Navigation -->
      <aside :class="[
        'fixed inset-y-0 left-0 z-50 w-64 bg-black text-zinc-300 flex flex-col justify-between border-r border-zinc-900 transition-transform duration-300 ease-in-out md:static md:translate-x-0',
        mobileMenuOpen ? 'translate-x-0' : '-translate-x-full'
      ]">
        <div class="p-6">
          <!-- Logo Header -->
          <div class="mb-10">
            <h1 class="text-2xl font-black tracking-widest text-white">PO<span style="color: #38872c;">O</span>L</h1>
            <p class="text-[8px] tracking-wider font-bold uppercase mt-0.5" style="color: #38872c;">Connecting Demand to
              Local Capability</p>
          </div>

          <!-- Nav Items -->
          <nav class="space-y-2 text-xs">
            <button v-for="(item, index) in navItems" :key="item" @click="activeTab = item" :class="[
              'w-full text-left px-4 py-3 rounded-xl transition flex items-center gap-3 font-medium',
              activeTab === item
                ? 'bg-zinc-900 text-white shadow-inner'
                : 'text-zinc-400 hover:text-white hover:bg-zinc-900/50'
            ]" :style="activeTab === item ? 'border: 1px solid rgba(56, 135, 44, 0.4);' : ''">
              <span class="text-[10px] font-bold" style="color: #38872c;">0{{ index + 1 }}</span>
              <span>{{ item }}</span>
            </button>
          </nav>
        </div>

        <!-- Bottom Footer info / Logout -->
        <div class="p-6 border-t border-zinc-900 text-[10px] text-zinc-500 space-y-3">
          <div>
            <p class="font-bold text-zinc-400 mb-1">Committee demo flow</p>
            <p>Demand → Capability → Pool → Gap → Growth</p>
          </div>
          <div class="pt-2 border-t border-zinc-900 flex items-center justify-between">
            <span>AI understands & explains.</span>
            <button @click="isAuthenticated = false" class="text-red-400 hover:text-red-300 font-bold">Logout</button>
          </div>
        </div>
      </aside>

      <!-- Overlay for mobile drawer -->
      <div v-if="mobileMenuOpen" @click="mobileMenuOpen = false" class="fixed inset-0 bg-black/50 z-40 md:hidden"></div>

      <!-- Main Dashboard Content Area -->
      <main class="flex-1 flex flex-col min-w-0 overflow-y-auto p-4 md:p-8 space-y-6">

        <!-- Top Status Bar -->
        <div class="flex justify-between items-center text-[11px] text-zinc-400 border-b border-zinc-900 pb-3">
          <span class="tracking-widest uppercase font-semibold text-zinc-400">
            PIF MUSAHAMA HACKATHON — Welcome, {{ userName }}
          </span>
          <div class="flex items-center gap-2 bg-zinc-950 border border-zinc-800 px-3 py-1 rounded-full"
            style="color: #38872c;">
            <span class="w-2 h-2 rounded-full animate-pulse" style="background-color: #38872c;"></span>
            <span>Capability data connected</span>
          </div>
        </div>

        <!-- ================= TAB 1: OVERVIEW ================= -->
        <div v-if="activeTab === 'Overview'" class="space-y-6">
          <div class="space-y-4">
            <h2 class="text-2xl font-bold tracking-tight text-white">Overview</h2>

            <!-- Banner Card with Shadow/Glow -->
            <div
              class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl shadow-xl relative overflow-hidden flex flex-col lg:flex-row justify-between items-start lg:items-center gap-8 transition-all hover:border-[#38872c]/40"
              style="box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);">
              <div class="space-y-3 max-w-2xl">
                <span class="text-[10px] font-bold tracking-widest uppercase" style="color: #38872c;">POOL INTELLIGENCE
                  LAYER</span>
                <h3 class="text-3xl md:text-4xl font-extrabold text-white tracking-tight leading-snug">
                  Saudi demand exists.<br>
                  Local capability exists.<br>
                  <span style="color: #38872c;">PO<span class="text-white">O</span>L</span> connects the two.
                </h3>
                <p class="text-xs text-zinc-400 leading-relaxed">
                  POOL transforms fragmented portfolio demand and supplier data into a live view of qualified national
                  capacity — then reveals exactly where local capabilities need to grow.
                </p>
              </div>

              <!-- Right Metrics Indicator -->
              <div class="flex items-center gap-6 bg-black border border-zinc-800 px-6 py-5 rounded-xl shrink-0">
                <div class="text-center">
                  <p class="text-2xl font-black text-white">2.4M</p>
                  <span class="text-[9px] text-zinc-500 tracking-widest uppercase">DEMAND</span>
                </div>
                <span class="text-lg" style="color: #38872c;">→</span>
                <div class="text-center">
                  <p class="text-2xl font-black" style="color: #38872c;">1.7M</p>
                  <span class="text-[9px] text-zinc-500 tracking-widest uppercase">CAPACITY</span>
                </div>
                <span class="text-lg" style="color: #38872c;">→</span>
                <div class="text-center">
                  <p class="text-2xl font-black text-white">700K</p>
                  <span class="text-[9px] text-zinc-500 tracking-widest uppercase">OPPORTUNITY</span>
                </div>
              </div>
            </div>
          </div>

          <!-- 4 Grid Metric Cards with interactive shadow hover -->
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div
              class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2 transition-all duration-300 hover:border-[#38872c]/40 hover:shadow-[0_8px_25px_rgba(56,135,44,0.15)]">
              <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">AGGREGATED DEMAND</span>
              <h4 class="text-3xl font-black text-white">2.4M</h4>
              <p class="text-[11px] text-zinc-400">Across current buyer requests</p>
            </div>

            <div
              class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2 transition-all duration-300 hover:border-[#38872c]/40 hover:shadow-[0_8px_25px_rgba(56,135,44,0.15)]">
              <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">QUALIFIED LOCAL CAPACITY</span>
              <h4 class="text-3xl font-black" style="color: #38872c;">1.7M</h4>
              <p class="text-[11px] text-zinc-400">Verified supplier capacity</p>
            </div>

            <div
              class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2 transition-all duration-300 hover:border-[#38872c]/40 hover:shadow-[0_8px_25px_rgba(56,135,44,0.15)]">
              <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">CAPACITY GAP</span>
              <h4 class="text-3xl font-black text-white">700K</h4>
              <p class="text-[11px] text-zinc-400">Demand not currently covered</p>
            </div>

            <div
              class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2 transition-all duration-300 hover:border-[#38872c]/40 hover:shadow-[0_8px_25px_rgba(56,135,44,0.15)]">
              <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">LOCAL GROWTH OPPORTUNITY
                →</span>
              <h4 class="text-3xl font-black" style="color: #38872c;">700K</h4>
              <p class="text-[11px] text-zinc-400">Click to explore the gap</p>
            </div>
          </div>

          <!-- Ask POOL Interactive Section -->
          <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-3 relative shadow-xl">
            <div class="absolute -top-3 right-6 z-10">
              <span
                class="px-2.5 py-0.5 text-[9px] font-extrabold uppercase tracking-wider text-black rounded-full shadow-md"
                style="background-color: #38872c;">
                ✨ AI Agent Draft
              </span>
            </div>

            <div>
              <h3 class="font-bold text-sm text-white">Ask POOL</h3>
              <p class="text-xs text-zinc-400">Query national supplier capability directly.</p>
            </div>

            <form @submit.prevent="submitQuery" class="flex flex-col sm:flex-row gap-3">
              <input type="text" v-model="userQuery"
                placeholder="Can Saudi suppliers fulfil 650K units of Industrial X within 45 days?"
                class="flex-1 bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition"
                @focus="$event.target.style.borderColor = '#38872c'"
                @blur="$event.target.style.borderColor = '#27272a'">

              <button type="submit" :disabled="loading"
                class="text-black font-bold px-6 py-3 rounded-xl text-xs transition shrink-0 disabled:opacity-50"
                style="background-color: #38872c; box-shadow: 0 4px 20px rgba(56, 135, 44, 0.35);">
                {{ loading ? 'Analyzing...' : 'Ask POOL' }}
              </button>
            </form>

            <div v-if="aiResponse" class="p-4 bg-black rounded-xl text-xs text-zinc-300 mt-2"
              style="border: 1px solid rgba(56, 135, 44, 0.3);">
              <span class="font-bold block mb-1" style="color: #38872c;">POOL Intelligence Output:</span>
              {{ aiResponse }}
            </div>
          </div>
        </div>

        <!-- ================= TAB 2: DEMAND INTELLIGENCE ================= -->
        <div v-if="activeTab === 'Demand Intelligence'" class="space-y-6">
          <h2 class="text-2xl font-bold tracking-tight text-white">Demand Intelligence</h2>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl relative">
              <div class="absolute -top-3 right-6 z-10">
                <span
                  class="px-2.5 py-0.5 text-[9px] font-extrabold uppercase tracking-wider text-black rounded-full shadow-md"
                  style="background-color: #38872c;">
                  ✨ NLP Input Module
                </span>
              </div>
              <div>
                <h3 class="font-bold text-sm text-white mb-1">Buyer demand</h3>
                <p class="text-[11px] text-zinc-400">Enter a procurement requirement in natural language. For the MVP,
                  buyer requests are created by the team.</p>
              </div>

              <textarea v-model="demandText" rows="4"
                class="w-full bg-black border border-zinc-800 rounded-xl p-4 text-xs text-white focus:outline-none transition resize-none"
                @focus="$event.target.style.borderColor = '#38872c'"
                @blur="$event.target.style.borderColor = '#27272a'"></textarea>

              <button @click="analyseDemand"
                class="text-black font-bold px-6 py-2.5 rounded-xl text-xs transition shadow-md"
                style="background-color: #38872c;">
                Analyse Demand
              </button>
            </div>

            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
              <div>
                <h3 class="font-bold text-sm text-white mb-1">AI requirement extraction</h3>
                <p class="text-[11px] text-zinc-400">AI structures the request. Qualification, scoring, capacity and
                  allocation are then calculated by code.</p>
              </div>

              <div class="bg-black border border-zinc-800 p-4 rounded-xl space-y-2 text-xs">
                <span class="text-[9px] font-bold tracking-widest uppercase" style="color: #38872c;">STRUCTURED
                  DEMAND</span>
                <p><span class="text-zinc-500">Category:</span> {{ structuredDemand.category }}</p>
                <p><span class="text-zinc-500">Quantity:</span> {{ structuredDemand.quantity }}</p>
                <p><span class="text-zinc-500">Delivery window:</span> {{ structuredDemand.deliveryWindow }}</p>
                <p><span class="text-zinc-500">Supplier preference:</span> {{ structuredDemand.preference }}</p>
                <p><span class="text-zinc-500">Priority:</span> {{ structuredDemand.priority }}</p>
              </div>
            </div>
          </div>

          <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
            <div>
              <h3 class="font-bold text-sm text-white mb-1">Demand aggregation</h3>
              <p class="text-[11px] text-zinc-400">POOL combines requests instead of treating each buyer in isolation.
              </p>
            </div>

            <div class="overflow-x-auto">
              <table class="w-full text-left text-xs">
                <thead>
                  <tr class="border-b border-zinc-800 text-zinc-500 uppercase text-[10px]">
                    <th class="pb-3 font-semibold">BUYER</th>
                    <th class="pb-3 font-semibold">CATEGORY</th>
                    <th class="pb-3 font-semibold">DEMAND</th>
                    <th class="pb-3 font-semibold">DELIVERY</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-zinc-900 text-zinc-300">
                  <tr v-for="row in aggregatedDemands" :key="row.buyer" class="hover:bg-zinc-900/40 transition">
                    <td class="py-3 font-medium text-white">{{ row.buyer }}</td>
                    <td class="py-3">{{ row.category }}</td>
                    <td class="py-3 font-bold" style="color: #38872c;">{{ row.demand }}</td>
                    <td class="py-3">{{ row.delivery }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- ================= TAB 3: NATIONAL CAPABILITY MAP ================= -->
        <div v-if="activeTab === 'National Capability Map'" class="space-y-6">
          <h2 class="text-2xl font-bold tracking-tight text-white">National Capability Map</h2>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div
              class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl flex flex-col justify-between shadow-xl relative min-h-[420px]">
              <div>
                <h3 class="font-bold text-sm text-white mb-1">Regional Capabilities</h3>
                <p class="text-[11px] text-zinc-400">Geospatial breakdown of active suppliers and verified regional
                  capacity.</p>
              </div>

              <div
                class="relative w-full h-80 my-auto flex items-center justify-center border border-zinc-900/80 bg-black/40 rounded-xl">
                <svg class="absolute inset-0 w-full h-full p-4 opacity-50" viewBox="0 0 500 300" fill="none">
                  <path d="M120,80 Q200,40 320,60 T420,140 Q450,220 350,250 T150,230 Q80,180 120,80 Z" stroke="#38872c"
                    stroke-width="1.5" stroke-dasharray="4 4" fill="rgba(56,135,44,0.03)" />
                </svg>

                <div
                  class="absolute top-12 left-1/2 -translate-x-1/2 bg-zinc-900 border border-zinc-800 px-4 py-2 rounded-xl text-center shadow-lg">
                  <p class="text-xs font-bold text-white">Northern</p>
                  <p class="text-[10px]" style="color: #38872c;">3 suppliers • 95K</p>
                </div>
                <div
                  class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-zinc-900 border border-zinc-800 px-4 py-2 rounded-xl text-center shadow-lg">
                  <p class="text-xs font-bold text-white">Riyadh</p>
                  <p class="text-[10px]" style="color: #38872c;">54 suppliers • 820K</p>
                </div>
                <div
                  class="absolute bottom-12 left-12 bg-zinc-900 border border-zinc-800 px-4 py-2 rounded-xl text-center shadow-lg">
                  <p class="text-xs font-bold text-white">Western</p>
                  <p class="text-[10px]" style="color: #38872c;">19 suppliers • 270K</p>
                </div>
                <div
                  class="absolute bottom-16 right-16 bg-zinc-900 border border-zinc-800 px-4 py-2 rounded-xl text-center shadow-lg">
                  <p class="text-xs font-bold text-white">Eastern</p>
                  <p class="text-[10px]" style="color: #38872c;">28 suppliers • 610K</p>
                </div>
              </div>
            </div>

            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
              <div>
                <h3 class="font-bold text-sm text-white mb-1">Capability explorer</h3>
                <p class="text-[11px] text-zinc-400">Qualified companies • capabilities • row materials • current
                  capacity.</p>
              </div>

              <div class="space-y-3 text-xs">
                <select
                  class="w-full bg-black border border-zinc-800 rounded-xl p-2.5 text-zinc-300 focus:outline-none">
                  <option>Industrial X</option>
                  <option>Industrial Y</option>
                </select>
                <select
                  class="w-full bg-black border border-zinc-800 rounded-xl p-2.5 text-zinc-300 focus:outline-none">
                  <option>All regions</option>
                  <option>Riyadh</option>
                  <option>Eastern</option>
                  <option>Western</option>
                </select>
                <div class="flex gap-2">
                  <select
                    class="flex-1 bg-black border border-zinc-800 rounded-xl p-2.5 text-zinc-300 focus:outline-none">
                    <option>Qualified only</option>
                    <option>All suppliers</option>
                  </select>
                  <input type="text" placeholder="Search supplier"
                    class="flex-1 bg-black border border-zinc-800 rounded-xl p-2.5 text-zinc-300 focus:outline-none">
                </div>
              </div>

              <div class="space-y-3 pt-2">
                <div v-for="supplier in capabilitySuppliers" :key="supplier.name"
                  class="bg-black border border-zinc-800 p-4 rounded-xl space-y-2 text-xs">
                  <div class="flex justify-between items-center">
                    <span class="font-bold text-white">{{ supplier.name }}</span>
                    <span
                      class="text-[10px] font-bold px-2 py-0.5 rounded-full bg-emerald-950 text-emerald-400 border border-emerald-800/50">{{
                      supplier.match }} Match</span>
                  </div>
                  <p class="text-[11px] text-zinc-500">{{ supplier.desc }}</p>
                  <div class="flex justify-between items-baseline pt-1 border-t border-zinc-900">
                    <div>
                      <p class="text-sm font-black text-white">{{ supplier.capacity }}</p>
                      <span class="text-[9px] text-zinc-500 uppercase">Available capacity</span>
                    </div>
                    <div class="text-right">
                      <p class="text-[10px] text-zinc-400">{{ supplier.updated }}</p>
                      <p class="text-[10px] font-bold" style="color: #38872c;">{{ supplier.confidence }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- ================= TAB 4: SMART POOL ================= -->
        <div v-if="activeTab === 'Smart Pool'" class="space-y-6">
          <h2 class="text-2xl font-bold tracking-tight text-white">Smart Pool</h2>

          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Left Side: Fulfillment Requirement Card -->
            <div
              class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl space-y-6 shadow-xl flex flex-col justify-between">
              <div>
                <h3 class="font-bold text-sm text-white mb-1">Can local suppliers fulfil the demand?</h3>
              </div>

              <div class="text-center py-6 space-y-2">
                <span class="text-[10px] font-bold tracking-widest text-zinc-500 uppercase">BUYER REQUIREMENT</span>
                <p class="text-4xl md:text-5xl font-black" style="color: #38872c;">650K</p>
                <p class="text-xs text-zinc-300 font-medium">Industrial X • &le; 45 days</p>
              </div>

              <div class="bg-black border border-zinc-800 p-4 rounded-xl text-center text-xs text-zinc-400">
                No single qualified supplier can fulfil the full requirement. POOL creates the best qualified
                combination.
              </div>
            </div>

            <!-- Right Side: Smart Supplier Pool & Optimization -->
            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-6 shadow-xl">
              <div class="flex justify-between items-start">
                <div>
                  <h3 class="font-bold text-sm text-white mb-1">Smart supplier pool</h3>
                  <p class="text-[11px] text-zinc-400">Choose the optimization objective.</p>
                </div>
                <!-- Objective filter buttons -->
                <div class="flex gap-1 bg-black p-1 rounded-xl border border-zinc-800 text-[10px]">
                  <button class="px-3 py-1.5 rounded-lg font-bold text-black" style="background-color: #38872c;">Best
                    Fit</button>
                  <button class="px-3 py-1.5 rounded-lg text-zinc-400 hover:text-white transition">Lowest Cost</button>
                  <button class="px-3 py-1.5 rounded-lg text-zinc-400 hover:text-white transition">Fastest</button>
                </div>
              </div>

              <!-- Supplier Allocation List with Progress Bars -->
              <div class="space-y-4">
                <div v-for="item in smartPoolSuppliers" :key="item.name" class="space-y-1.5">
                  <div class="flex justify-between text-xs">
                    <div>
                      <span class="font-bold text-white">{{ item.name }}</span>
                      <span class="text-[10px] text-zinc-500 ml-2">{{ item.meta }}</span>
                    </div>
                    <span class="font-bold text-white">{{ item.allocated }}</span>
                  </div>
                  <!-- Progress Bar -->
                  <div class="w-full bg-black h-2.5 rounded-full overflow-hidden border border-zinc-800/80">
                    <div class="h-full rounded-full transition-all duration-500"
                      :style="{ width: item.width, backgroundColor: '#38872c' }"></div>
                  </div>
                </div>
              </div>

              <!-- Fulfillment Summary Box -->
              <div class="bg-black border border-zinc-800 p-4 rounded-xl space-y-3 text-xs">
                <div class="flex justify-between items-baseline">
                  <span class="font-bold text-white">580K fulfilled - 89.2%</span>
                  <span class="text-zinc-400 text-[11px]">Remaining unmet demand: <strong
                      class="text-amber-400">70K</strong></span>
                </div>
                <button @click="convertGap"
                  class="w-full font-bold py-2.5 rounded-xl text-xs transition text-black shadow-md flex items-center justify-center gap-2"
                  style="background-color: #38872c;">
                  <span>Convert 70K to Growth Opportunity</span>
                  <span>→</span>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- ================= OTHER TABS PLACEHOLDER ================= -->
        <div
          v-if="activeTab !== 'Overview' && activeTab !== 'Demand Intelligence' && activeTab !== 'National Capability Map' && activeTab !== 'Smart Pool'"
          class="space-y-6">
          <h2 class="text-2xl font-bold tracking-tight text-white">{{ activeTab }}</h2>
          <div class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl text-zinc-400 text-xs shadow-xl">
            Module for <span class="text-white font-bold">{{ activeTab }}</span> is linked and currently active in the
            presentation flow.
          </div>
        </div>

      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Authentication
const isAuthenticated = ref(false)
const loginLoading = ref(false)
const loginError = ref('')
const loginForm = ref({
  email: '',
  password: ''
})

const userName = computed(() => {
  if (!loginForm.value.email) return 'User'
  const namePart = loginForm.value.email.split('@')[0]
  return namePart
    .split('.')
    .map(word => word.charAt(0).toUpperCase() + word.slice(1))
    .join(' ')
})

const handleLogin = () => {
  loginLoading.value = true
  loginError.value = ''

  setTimeout(() => {
    if (loginForm.value.email && loginForm.value.password) {
      isAuthenticated.value = true
    } else {
      loginError.value = 'Please provide valid login info.'
    }
    loginLoading.value = false
  }, 800)
}

// Dashboard Navigation State
const mobileMenuOpen = ref(false)
const activeTab = ref('Overview')
const navItems = ['Overview', 'Demand Intelligence', 'National Capability Map', 'Smart Pool', 'Growth Opportunities']

// Overview AI Query State
const userQuery = ref('Can Saudi suppliers fulfil 650K units of Industrial X within 45 days?')
const loading = ref(false)
const aiResponse = ref('')

const submitQuery = () => {
  if (!userQuery.value) return
  loading.value = true
  aiResponse.value = ''

  setTimeout(() => {
    aiResponse.value = `Analysis for "${userQuery.value}": Qualified local suppliers across the network can cover 520K units within the timeline, leaving a capacity gap of 130K units recommended for local growth allocation.`
    loading.value = false
  }, 1200)
}

// Demand Intelligence & Aggregation State
const demandText = ref('We need 650,000 units of Industrial X delivered within 45 days from qualified local suppliers.')
const structuredDemand = ref({
  category: 'Industrial X',
  quantity: '650,000 units',
  deliveryWindow: '≤ 45 days',
  preference: 'Qualified local suppliers',
  priority: 'Capacity + qualification + delivery'
})

const aggregatedDemands = ref([
  { buyer: 'Portfolio Co. A', category: 'Industrial X', demand: '500K', delivery: '30 days' },
  { buyer: 'Portfolio Co. B', category: 'Industrial X', demand: '700K', delivery: '45 days' },
  { buyer: 'Portfolio Co. C', category: 'Industrial X', demand: '400K', delivery: '30 days' },
  { buyer: 'Portfolio Co. D', category: 'Industrial X', demand: '800K', delivery: '60 days' },
])

const analyseDemand = () => {
  aggregatedDemands.value.unshift({
    buyer: `${userName.value}'s Portfolio`,
    category: structuredDemand.value.category,
    demand: '650K',
    delivery: '45 days'
  })
  alert('Demand successfully analyzed, structured by AI, and linked to the National Demand Aggregation table!')
}

// National Capability Map Data
const capabilitySuppliers = ref([
  { name: 'Supplier A', match: '94%', desc: 'Fabrication • Steel Grade X • Riyadh', capacity: '400K', updated: 'Updated 2h ago', confidence: 'High confidence' },
  { name: 'Supplier B', match: '91%', desc: 'Manufacturing • Material X • Eastern', capacity: '300K', updated: 'Updated 5h ago', confidence: 'High confidence' },
  { name: 'Supplier C', match: '83%', desc: 'Assembly • Component X • Western', capacity: '250K', updated: 'Updated 1d ago', confidence: 'Medium confidence' }
])

// Smart Pool Data
const smartPoolSuppliers = ref([
  { name: 'Supplier A', meta: '94% match • Qualified', allocated: '250K', width: '75%' },
  { name: 'Supplier B', meta: '91% match • Qualified', allocated: '200K', width: '60%' },
  { name: 'Supplier C', meta: '88% match • Qualified', allocated: '130K', width: '40%' }
])

const convertGap = () => {
  activeTab.value = 'Growth Opportunities'
}
</script>