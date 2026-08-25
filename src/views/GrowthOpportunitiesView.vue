<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">Growth Opportunities</h2>

        <!-- Top Banner Card -->
        <div class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl shadow-xl relative overflow-hidden flex flex-col lg:flex-row justify-between items-start lg:items-center gap-8 transition-all hover:border-[#38872c]/40"
            style="box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);">
            <div class="space-y-3 max-w-2xl">
                <span class="text-[10px] font-bold tracking-widest uppercase" style="color: #38872c;">FROM SHORTAGE TO
                    STRATEGY</span>
                <h3 class="text-3xl md:text-4xl font-extrabold text-white tracking-tight leading-snug">
                    The gap is not the end.<br>
                    It is the <span style="color: #38872c;">opportunity.</span>
                </h3>
                <p class="text-xs text-zinc-400 leading-relaxed">
                    POOL aggregates recurring unmet demand and shows where Saudi supplier capacity can be developed or
                    expanded.
                </p>
            </div>

            <div class="bg-black border border-zinc-800 px-8 py-6 rounded-xl text-center shrink-0">
                <span class="text-[9px] text-zinc-500 tracking-widest uppercase block mb-1">NATIONAL LOCAL GROWTH
                    OPPORTUNITY</span>
                <p class="text-4xl font-black" style="color: #38872c;">700K</p>
            </div>
        </div>

        <!-- Bottom Grid: Where is the gap & Data confidence -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Left Side: Where is the gap Table -->
            <div class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Where is the gap?</h3>
                    <p class="text-[11px] text-zinc-400">Click Industrial X to understand what is driving the
                        opportunity.</p>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead>
                            <tr class="border-b border-zinc-800 text-zinc-500 uppercase text-[10px]">
                                <th class="pb-3 font-semibold">CAPABILITY</th>
                                <th class="pb-3 font-semibold">DEMAND</th>
                                <th class="pb-3 font-semibold">CAPACITY</th>
                                <th class="pb-3 font-semibold">GAP</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-zinc-900 text-zinc-300">
                            <tr v-for="gap in growthGaps" :key="gap.capability"
                                class="hover:bg-zinc-900/40 transition cursor-pointer">
                                <td class="py-3 font-bold" style="color: #38872c;">{{ gap.capability }}</td>
                                <td class="py-3">{{ gap.demand }}</td>
                                <td class="py-3">{{ gap.capacity }}</td>
                                <td class="py-3 font-black text-white" style="color: #38872c;">{{ gap.gap }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Right Side: Data Confidence Panel -->
            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Data confidence</h3>
                    <p class="text-[11px] text-zinc-400">"Live" means the user can see whether the capacity signal is
                        current enough to trust.</p>
                </div>

                <div class="space-y-3 pt-2 text-xs">
                    <div v-for="conf in dataConfidences" :key="conf.label"
                        class="flex justify-between items-center bg-black border border-zinc-800 p-3 rounded-xl">
                        <span class="text-zinc-300 font-medium">{{ conf.label }}</span>
                        <span class="text-[10px] font-bold px-2.5 py-1 rounded-full border" :style="conf.style">{{
                            conf.status }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const growthGaps = ref([
    { capability: 'Industrial X →', demand: '2.4M', capacity: '1.7M', gap: '700K' },
    { capability: 'Raw Material Y', demand: '1.2M', capacity: '1.05M', gap: '150K' },
    { capability: 'Component Z', demand: '900K', capacity: '880K', gap: '20K' }
])

const dataConfidences = ref([
    { label: 'Supplier A capacity', status: 'High • 2h ago', style: 'background-color: rgba(56,135,44,0.15); color: #4ade80; border-color: rgba(74,222,128,0.3);' },
    { label: 'Supplier B qualification', status: 'Verified • 5h ago', style: 'background-color: rgba(56,135,44,0.15); color: #4ade80; border-color: rgba(74,222,128,0.3);' },
    { label: 'Supplier C capacity', status: 'Medium • 1d ago', style: 'background-color: rgba(234,179,8,0.15); color: #facc15; border-color: rgba(250,204,21,0.3);' },
    { label: 'Supplier F capacity', status: 'Refresh • 3d ago', style: 'background-color: rgba(239,68,68,0.15); color: #f87171; border-color: rgba(248,113,113,0.3);' }
])
</script>