<script setup>
/* eslint-disable vue/multi-word-component-names, no-undef */
defineProps({
    userName: String
})
</script>

<template>
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
</template>