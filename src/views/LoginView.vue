<template>
    <div class="min-h-screen w-full bg-black flex items-center justify-center p-6 text-white" dir="ltr">
        <div class="max-w-md w-full bg-zinc-950 border border-zinc-800 p-8 rounded-2xl shadow-2xl space-y-6 relative">
            <div class="text-center">
                <h1 class="text-3xl font-black tracking-widest text-white mb-1">PO<span
                        style="color: #38872c;">O</span>L</h1>
                <p class="text-[9px] tracking-widest uppercase font-bold" style="color: #38872c;">Connecting Demand to
                    Local Capability</p>
            </div>

            <form @submit.prevent="handleLogin" class="space-y-4">
                <div>
                    <label class="block text-xs font-medium text-zinc-400 mb-1">Email Address</label>
                    <input type="email" v-model="email" placeholder="name@example.com" required
                        class="w-full bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition"
                        @focus="$event.target.style.borderColor = '#38872c'"
                        @blur="$event.target.style.borderColor = '#27272a'">
                </div>

                <div>
                    <label class="block text-xs font-medium text-zinc-400 mb-1">Password</label>
                    <input type="password" v-model="password" placeholder="••••••••" required
                        class="w-full bg-black border border-zinc-800 rounded-xl px-4 py-3 text-xs text-white focus:outline-none transition"
                        @focus="$event.target.style.borderColor = '#38872c'"
                        @blur="$event.target.style.borderColor = '#27272a'">
                </div>

                <div class="relative pt-3">
                    <span
                        class="absolute top-0 right-3 z-10 px-2 py-0.5 text-[8px] font-extrabold uppercase tracking-wider text-black rounded-full shadow-md animate-pulse"
                        style="background-color: #38872c;">
                        Secure Portal
                    </span>
                    <button type="submit" :disabled="loading"
                        class="w-full text-black font-extrabold py-3 rounded-xl text-xs transition disabled:opacity-50"
                        style="background-color: #38872c; box-shadow: 0 4px 20px rgba(56, 135, 44, 0.35);">
                        {{ loading ? 'Authenticating...' : 'Sign In' }}
                    </button>
                </div>
            </form>

            <p v-if="error" class="text-xs text-red-500 text-center">{{ error }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue'
const emit = defineEmits(['login-success'])

const email = ref('')
const password = ref('')
const loading = ref(false)
const error = ref('')

const handleLogin = () => {
    loading.value = true
    error.value = ''
    setTimeout(() => {
        if (email.value && password.value) {
            emit('login-success')
        } else {
            error.value = 'Please provide valid login info.'
        }
        loading.value = false
    }, 800)
}
</script>