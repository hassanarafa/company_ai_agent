<template>
    <div class="space-y-6">
        <div class="space-y-4">
            <h2 class="text-2xl font-bold tracking-tight text-white">Overview</h2>

            <div class="bg-zinc-950 border border-zinc-900 p-8 rounded-2xl shadow-xl relative overflow-hidden flex flex-col lg:flex-row justify-between items-start lg:items-center gap-8 transition-all hover:border-[#38872c]/40"
                style="box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);">
                <div class="space-y-3 max-w-2xl">
                    <span class="text-[10px] font-bold tracking-widest uppercase" style="color: #38872c;">POOL
                        INTELLIGENCE LAYER</span>
                    <h3 class="text-3xl md:text-4xl font-extrabold text-white tracking-tight leading-snug">
                        Saudi demand exists.<br>
                        Local capability exists.<br>
                        <span style="color: #38872c;">PO<span class="text-white">O</span>L</span> connects the two.
                    </h3>
                    <p class="text-xs text-zinc-400 leading-relaxed">
                        POOL transforms fragmented portfolio demand and supplier data into a live view of qualified
                        national capacity — then reveals exactly where local capabilities need to grow.
                    </p>
                </div>

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

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2">
                <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">AGGREGATED DEMAND</span>
                <h4 class="text-3xl font-black text-white">2.4M</h4>
                <p class="text-[11px] text-zinc-400">Across current buyer requests</p>
            </div>
            <div class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2">
                <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">QUALIFIED LOCAL
                    CAPACITY</span>
                <h4 class="text-3xl font-black" style="color: #38872c;">1.7M</h4>
                <p class="text-[11px] text-zinc-400">Verified supplier capacity</p>
            </div>
            <div class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2">
                <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">CAPACITY GAP</span>
                <h4 class="text-3xl font-black text-white">700K</h4>
                <p class="text-[11px] text-zinc-400">Demand not currently covered</p>
            </div>
            <div class="bg-zinc-950 border border-zinc-900 p-5 rounded-2xl space-y-2">
                <span class="text-[10px] font-bold text-zinc-500 tracking-wider uppercase">LOCAL GROWTH OPPORTUNITY
                    →</span>
                <h4 class="text-3xl font-black" style="color: #38872c;">700K</h4>
                <p class="text-[11px] text-zinc-400">Click to explore the gap</p>
            </div>
        </div>

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
                    class="flex-1 bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition">
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
</template>

<script setup>
import { ref } from 'vue'
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
</script>