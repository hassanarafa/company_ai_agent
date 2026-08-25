<script setup>
/* eslint-disable vue/multi-word-component-names */
defineProps({
    navItems: Array,
    activeTab: String,
    mobileMenuOpen: Boolean
})
defineEmits(['update:activeTab', 'logout'])
</script>

<template>
    <aside :class="[
        'fixed inset-y-0 left-0 z-50 w-64 bg-black text-zinc-300 flex flex-col justify-between border-r border-zinc-900 transition-transform duration-300 ease-in-out md:static md:translate-x-0 shrink-0',
        mobileMenuOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
    ]">
        <div class="p-6">
            <div class="mb-10">
                <h1 class="text-2xl font-black tracking-widest text-white">PO<span style="color: #38872c;">O</span>L
                </h1>
                <p class="text-[8px] tracking-wider font-bold uppercase mt-0.5" style="color: #38872c;">Connecting
                    Demand to Local Capability</p>
            </div>

            <nav class="space-y-2 text-xs">
                <button v-for="(item, index) in navItems" :key="item" @click="$emit('update:activeTab', item)" :class="[
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

        <div class="p-6 border-t border-zinc-900 text-[10px] text-zinc-500 space-y-3">
            <div>
                <p class="font-bold text-zinc-400 mb-1">Committee demo flow</p>
                <p>Demand → Capability → Pool → Gap → Growth</p>
            </div>
            <div class="pt-2 border-t border-zinc-900 flex items-center justify-between">
                <span>AI understands & explains.</span>
                <button @click="$emit('logout')" class="text-red-400 hover:text-red-300 font-bold">Logout</button>
            </div>
        </div>
    </aside>
</template>