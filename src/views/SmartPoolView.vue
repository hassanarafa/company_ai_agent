<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">Smart Pool</h2>
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <div
                class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl space-y-6 shadow-xl flex flex-col justify-between">
                <h3 class="font-bold text-sm text-white mb-1">Can local suppliers fulfil the demand?</h3>
                <div class="text-center py-6 space-y-2">
                    <span class="text-[10px] font-bold tracking-widest text-zinc-500 uppercase">BUYER REQUIREMENT</span>
                    <p class="text-4xl md:text-5xl font-black" style="color: #38872c;">650K</p>
                </div>
            </div>

            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-6 shadow-xl">
                <h3 class="font-bold text-sm text-white mb-1">Smart supplier pool</h3>
                <div class="space-y-4">
                    <div v-for="item in smartPoolSuppliers" :key="item.name" class="space-y-1.5">
                        <div class="flex justify-between text-xs">
                            <span class="font-bold text-white">{{ item.name }}</span>
                            <span class="font-bold text-white">{{ item.allocated }}</span>
                        </div>
                        <div class="w-full bg-black h-2.5 rounded-full overflow-hidden border border-zinc-800">
                            <div class="h-full rounded-full" :style="{ width: item.width, backgroundColor: '#38872c' }">
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
const smartPoolSuppliers = ref([
    { name: 'Supplier A', allocated: '250K', width: '75%' },
    { name: 'Supplier B', allocated: '200K', width: '60%' }
])
</script>