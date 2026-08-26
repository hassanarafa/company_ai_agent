<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">National Capability Map</h2>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Left Side: Map Box -->
            <div
                class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl flex flex-col justify-between shadow-xl relative min-h-[520px]">

                <!-- Header Info inside map box -->
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h3 class="font-bold text-sm text-white mb-1">Saudi supply intelligence</h3>
                        <p class="text-[11px] text-zinc-400">Click a capacity node to inspect regional supplier
                            strength.</p>
                    </div>
                    <div class="flex items-center gap-2">
                        <span
                            class="bg-black border border-zinc-800 text-zinc-300 px-3 py-1 rounded-full text-[10px] font-semibold">104
                            suppliers</span>
                        <span
                            class="bg-black border border-zinc-800 text-zinc-300 px-3 py-1 rounded-full text-[10px] font-semibold"
                            style="color: #38872c;">1.795M verified capacity</span>
                    </div>
                </div>

                <!-- Map Container with Perfect Coordinates Adjustment -->
                <div
                    class="relative w-full h-[420px] my-auto flex items-center justify-center border border-zinc-900 bg-black rounded-xl overflow-hidden mt-4">

                    <!-- Map Image Background -->
                    <img src="@/assets/map.jpg" alt="Saudi Arabia Map"
                        class="absolute inset-0 w-full h-full object-cover opacity-85" />

                    <!-- Kingdom Label -->
                    <span
                        class="absolute top-4 left-6 text-[10px] font-bold uppercase tracking-widest text-white bg-black/80 px-2.5 py-1 rounded border border-zinc-800 z-20">Kingdom
                        of Saudi Arabia</span>

                    <!-- Northern Node (Purple) -> Adjusted North/Hail position -->
                    <div
                        class="absolute top-[36%] left-[41%] -translate-x-1/2 -translate-y-1/2 flex flex-col items-center cursor-pointer group z-10">
                        <div
                            class="w-10 h-10 rounded-full bg-purple-950 border-2 border-purple-500 flex items-center justify-center text-white font-bold text-xs shadow-lg group-hover:scale-110 transition">
                            3
                        </div>
                        <div
                            class="bg-black/90 border border-zinc-800 px-2.5 py-1 rounded-lg mt-1 text-center shadow-md backdrop-blur-sm">
                            <p class="text-[11px] font-bold text-white">Northern</p>
                            <p class="text-[9px] text-purple-400 font-medium">95K capacity</p>
                        </div>
                    </div>

                    <!-- Riyadh Node (Green - Center) -> Adjusted exact Riyadh position -->
                    <div
                        class="absolute top-[58%] left-[54%] -translate-x-1/2 -translate-y-1/2 flex flex-col items-center cursor-pointer group z-10">
                        <div class="w-14 h-14 rounded-full bg-emerald-950 border-2 border-emerald-500 flex items-center justify-center text-white font-extrabold text-sm shadow-xl group-hover:scale-110 transition"
                            style="box-shadow: 0 0 25px rgba(56,135,44,0.8);">
                            54
                        </div>
                        <div
                            class="bg-black/90 border border-zinc-800 px-3 py-1 rounded-lg mt-1 text-center shadow-md backdrop-blur-sm">
                            <p class="text-[11px] font-bold text-white">Riyadh</p>
                            <p class="text-[9px] text-emerald-400 font-medium">820K capacity</p>
                        </div>
                    </div>

                    <!-- Eastern Node (Orange) -> Adjusted Eastern Province position -->
                    <div
                        class="absolute top-[57%] right-[24%] -translate-x-1/2 -translate-y-1/2 flex flex-col items-center cursor-pointer group z-10">
                        <div
                            class="w-12 h-12 rounded-full bg-amber-950 border-2 border-amber-500 flex items-center justify-center text-white font-bold text-xs shadow-lg group-hover:scale-110 transition">
                            28
                        </div>
                        <div
                            class="bg-black/90 border border-zinc-800 px-2.5 py-1 rounded-lg mt-1 text-center shadow-md backdrop-blur-sm">
                            <p class="text-[11px] font-bold text-white">Eastern</p>
                            <p class="text-[9px] text-amber-400 font-medium">610K capacity</p>
                        </div>
                    </div>

                    <!-- Western Node (Yellow) -> Adjusted Makkah/Madinah Western position -->
                    <div
                        class="absolute top-[67%] left-[42%] -translate-x-1/2 -translate-y-1/2 flex flex-col items-center cursor-pointer group z-10">
                        <div
                            class="w-11 h-11 rounded-full bg-yellow-950 border-2 border-yellow-500 flex items-center justify-center text-white font-bold text-xs shadow-lg group-hover:scale-110 transition">
                            19
                        </div>
                        <div
                            class="bg-black/90 border border-zinc-800 px-2.5 py-1 rounded-lg mt-1 text-center shadow-md backdrop-blur-sm">
                            <p class="text-[11px] font-bold text-white">Western</p>
                            <p class="text-[9px] text-yellow-400 font-medium">270K capacity</p>
                        </div>
                    </div>

                </div>

                <!-- Footer Legend -->
                <div
                    class="flex flex-wrap items-center justify-between text-[10px] text-zinc-500 pt-3 border-t border-zinc-900 mt-2">
                    <div class="flex items-center gap-1.5">
                        <span class="w-2 h-2 rounded-full bg-zinc-400"></span>
                        <span>Node size = verified capacity</span>
                    </div>
                    <div class="flex items-center gap-1.5">
                        <span class="w-2 h-2 rounded-full" style="background-color: #38872c;"></span>
                        <span>Click = region drill-down</span>
                    </div>
                    <div class="flex items-center gap-1.5">
                        <span class="w-2 h-2 rounded-full bg-zinc-600"></span>
                        <span>Data shown = prototype values</span>
                    </div>
                </div>

            </div>

            <!-- Right Side: Capability Explorer -->
            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Capability explorer</h3>
                    <p class="text-[11px] text-zinc-400">Qualified companies • capabilities • raw materials • current
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
</template>

<script setup>
import { ref } from 'vue'

const capabilitySuppliers = ref([
    { name: 'Supplier A', match: '94%', desc: 'Fabrication • Steel Grade X • Riyadh', capacity: '400K', updated: 'Updated 2h ago', confidence: 'High confidence' },
    { name: 'Supplier B', match: '91%', desc: 'Manufacturing • Material X • Eastern', capacity: '300K', updated: 'Updated 5h ago', confidence: 'High confidence' },
    { name: 'Supplier C', match: '83%', desc: 'Assembly • Component X • Western', capacity: '250K', updated: 'Updated 1d ago', confidence: 'Medium confidence' }
])
</script>