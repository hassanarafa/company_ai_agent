<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">National Capability Map</h2>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Left Side: Regional Map Graphic Box -->
            <div
                class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl flex flex-col justify-between shadow-xl relative min-h-[460px]">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Regional Capabilities</h3>
                    <p class="text-[11px] text-zinc-400">Geospatial breakdown of active suppliers and verified regional
                        capacity.</p>
                </div>

                <!-- Map Visual Container -->
                <div
                    class="relative w-full h-96 my-auto flex items-center justify-center border border-zinc-900/80 bg-black/40 rounded-xl overflow-hidden">

                    <!-- Custom Refined Network Boundary SVG -->
                    <svg class="absolute inset-0 w-full h-full p-6 opacity-60 pointer-events-none" viewBox="0 0 600 350"
                        fill="none">
                        <!-- Outer Connected Network Polygon Shape -->
                        <path
                            d="M300,45 C420,45 520,110 520,175 C520,240 420,305 300,305 C180,305 80,240 80,175 C80,110 180,45 300,45 Z"
                            stroke="#38872c" stroke-width="1.5" stroke-dasharray="6 6" fill="rgba(56,135,44,0.04)" />

                        <!-- Connection Lines from Riyadh Center to each Node -->
                        <line x1="300" y1="175" x2="300" y2="75" stroke="#38872c" stroke-width="1.5"
                            stroke-opacity="0.5" />
                        <line x1="300" y1="175" x2="140" y2="235" stroke="#38872c" stroke-width="1.5"
                            stroke-opacity="0.5" />
                        <line x1="300" y1="175" x2="460" y2="235" stroke="#38872c" stroke-width="1.5"
                            stroke-opacity="0.5" />
                    </svg>

                    <!-- Northern Region Node -->
                    <div
                        class="absolute top-10 left-1/2 -translate-x-1/2 bg-zinc-900/95 border border-zinc-800 px-5 py-2.5 rounded-xl text-center shadow-2xl transition hover:border-[#38872c]">
                        <p class="text-xs font-bold text-white">Northern</p>
                        <p class="text-[10px]" style="color: #38872c;">3 suppliers • 95K</p>
                    </div>

                    <!-- Riyadh Central Node -->
                    <div
                        class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-zinc-900/95 border border-zinc-800 px-5 py-3 rounded-xl text-center shadow-2xl transition hover:border-[#38872c]">
                        <p class="text-xs font-bold text-white">Riyadh</p>
                        <p class="text-[10px]" style="color: #38872c;">54 suppliers • 820K</p>
                    </div>

                    <!-- Western Region Node -->
                    <div
                        class="absolute bottom-10 left-12 bg-zinc-900/95 border border-zinc-800 px-5 py-2.5 rounded-xl text-center shadow-2xl transition hover:border-[#38872c]">
                        <p class="text-xs font-bold text-white">Western</p>
                        <p class="text-[10px]" style="color: #38872c;">19 suppliers • 270K</p>
                    </div>

                    <!-- Eastern Region Node -->
                    <div
                        class="absolute bottom-10 right-12 bg-zinc-900/95 border border-zinc-800 px-5 py-2.5 rounded-xl text-center shadow-2xl transition hover:border-[#38872c]">
                        <p class="text-xs font-bold text-white">Eastern</p>
                        <p class="text-[10px]" style="color: #38872c;">28 suppliers • 610K</p>
                    </div>

                </div>
            </div>

            <!-- Right Side: Capability Explorer & Supplier Cards -->
            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Capability explorer</h3>
                    <p class="text-[11px] text-zinc-400">Qualified companies • capabilities • row materials • current
                        capacity.</p>
                </div>

                <!-- Filters -->
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

                <!-- Supplier Match Cards -->
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
</template>

<script setup>
import { ref } from 'vue'

const capabilitySuppliers = ref([
    { name: 'Supplier A', match: '94%', desc: 'Fabrication • Steel Grade X • Riyadh', capacity: '400K', updated: 'Updated 2h ago', confidence: 'High confidence' },
    { name: 'Supplier B', match: '91%', desc: 'Manufacturing • Material X • Eastern', capacity: '300K', updated: 'Updated 5h ago', confidence: 'High confidence' },
    { name: 'Supplier C', match: '83%', desc: 'Assembly • Component X • Western', capacity: '250K', updated: 'Updated 1d ago', confidence: 'Medium confidence' }
])
</script>