<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">Smart Pool</h2>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Left Box: Buyer Requirement -->
            <div
                class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl space-y-6 shadow-xl flex flex-col justify-between">
                <h3 class="font-bold text-sm text-white mb-1">Can local suppliers fulfil the demand?</h3>

                <div class="text-center py-6 space-y-2">
                    <span class="text-[10px] font-bold tracking-widest text-zinc-500 uppercase">BUYER REQUIREMENT</span>
                    <p class="text-4xl md:text-5xl font-black" style="color: #38872c;">650K</p>
                    <p class="text-xs text-zinc-400 font-medium">Industrial X • ≤45 days</p>
                </div>

                <div class="bg-black border border-zinc-900 p-4 rounded-xl text-center">
                    <p class="text-xs text-zinc-400">
                        No single qualified supplier can fulfil the full requirement. POOL creates the best qualified
                        combination.
                    </p>
                </div>
            </div>

            <!-- Right Box: Smart Supplier Pool -->
            <div
                class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-6 shadow-xl flex flex-col justify-between">
                <div class="space-y-4">
                    <div class="flex justify-between items-center">
                        <h3 class="font-bold text-sm text-white mb-1">Smart supplier pool</h3>
                        <span class="text-[10px] text-zinc-400">Choose the optimization objective.</span>
                    </div>

                    <!-- Optimization Objective Buttons -->
                    <div class="flex gap-2">
                        <button
                            class="px-3 py-1.5 rounded-lg text-xs font-bold bg-zinc-900 text-white border border-zinc-800">Best
                            Fit</button>
                        <button
                            class="px-3 py-1.5 rounded-lg text-xs font-medium text-zinc-400 hover:bg-zinc-900/50">Lowest
                            Cost</button>
                        <button
                            class="px-3 py-1.5 rounded-lg text-xs font-medium text-zinc-400 hover:bg-zinc-900/50">Fastest</button>
                    </div>

                    <!-- Suppliers List -->
                    <div class="space-y-4 pt-2">
                        <div v-for="item in smartPoolSuppliers" :key="item.name" class="space-y-1.5">
                            <div class="flex justify-between text-xs items-center">
                                <div>
                                    <span class="font-bold text-white">{{ item.name }}</span>
                                    <span class="text-[10px] text-zinc-500 ml-2">{{ item.match }}</span>
                                </div>
                                <span class="font-bold text-white">{{ item.allocated }}</span>
                            </div>
                            <div class="w-full bg-black h-2.5 rounded-full overflow-hidden border border-zinc-800">
                                <div class="h-full rounded-full transition-all duration-500"
                                    :style="{ width: item.width, backgroundColor: '#38872c' }"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Fulfilled Status & Gap Conversion Box -->
                <div class="bg-black border border-zinc-800 p-4 rounded-xl space-y-3 mt-4">
                    <div class="flex justify-between items-center text-xs">
                        <span class="font-bold" style="color: #38872c;">580K fulfilled · 89.2%</span>
                        <span class="text-zinc-400">Remaining unmet demand: <strong
                                class="text-white">70K</strong></span>
                    </div>
                    <button @click="$emit('navigate', 'Growth Opportunities')"
                        class="w-full py-2.5 px-4 rounded-xl text-xs font-bold text-black bg-white hover:bg-zinc-200 transition">
                        Convert 70K to Growth Opportunity →
                    </button>
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
defineEmits(['navigate'])

const smartPoolSuppliers = ref([
    { name: 'Supplier A', match: '94% match • Qualified', allocated: '250K', width: '75%' },
    { name: 'Supplier B', match: '91% match • Qualified', allocated: '200K', width: '60%' },
    { name: 'Supplier C', match: '88% match • Qualified', allocated: '130K', width: '40%' }
])
</script>