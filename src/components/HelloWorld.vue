<template>
  <div class="min-h-screen bg-slate-950 text-slate-100 font-sans p-6 md:p-10" dir="rtl">
    <div class="max-w-7xl mx-auto space-y-8">

      <header
        class="flex flex-col md:flex-row justify-between items-start md:items-center bg-slate-900 border border-slate-800 p-6 rounded-2xl shadow-xl gap-4">
        <div>
          <h1 class="text-2xl md:text-3xl font-extrabold text-amber-500 tracking-wide">منظومة حوكمة مخازن مواد البناء
          </h1>
          <p class="text-slate-400 text-sm mt-1">التحكم الآلي بالحصص والمخزون مدعوم بالذكاء الاصطناعي</p>
        </div>
        <div class="flex items-center gap-3 bg-slate-950 px-4 py-2 rounded-xl border border-slate-800">
          <span class="w-2.5 h-2.5 rounded-full bg-emerald-500 animate-pulse"></span>
          <span class="text-xs font-medium text-slate-300">النظام متصل وجاهز</span>
        </div>
      </header>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        <div v-for="item in inventory" :key="item.name"
          class="bg-slate-900 border border-slate-800 p-5 rounded-2xl shadow-lg">
          <div class="flex justify-between items-start">
            <div>
              <p class="text-slate-400 text-xs font-semibold">مخزون المادة</p>
              <h3 class="text-base font-bold text-slate-200 mt-1">{{ item.name }}</h3>
            </div>
          </div>
          <div class="mt-4 flex items-baseline justify-between">
            <span class="text-2xl font-black text-amber-400">{{ item.qty.toLocaleString() }}</span>
            <span class="text-xs text-slate-500">{{ item.unit }}</span>
          </div>
          <div class="w-full bg-slate-800 h-1.5 rounded-full mt-3 overflow-hidden">
            <div class="bg-amber-500 h-full rounded-full" :style="{ width: item.percentage + '%' }"></div>
          </div>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">

        <div
          class="lg:col-span-1 bg-slate-900 border border-slate-800 p-6 rounded-2xl shadow-xl flex flex-col justify-between">
          <div>
            <h2 class="text-base font-bold text-emerald-400 mb-4 pb-2 border-b border-slate-800">
              تقديم طلب توريد جديد
            </h2>
            <form @submit.prevent="submitOrder" class="space-y-4">
              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">اسم الشركة الطالبة</label>
                <select v-model="form.company"
                  class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-white text-sm focus:outline-none focus:border-amber-500 transition">
                  <option>شركة النور للمقاولات</option>
                  <option>شركة البناء الحديث</option>
                  <option>شركة الاتحاد الهندسية</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">مادة البناء المطلوبة</label>
                <select v-model="form.material"
                  class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-white text-sm focus:outline-none focus:border-amber-500 transition">
                  <option value="رمل">رمل</option>
                  <option value="زلط">زلط</option>
                  <option value="طوب أسمنتي">طوب أسمنتي</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">الكمية المطلوبة</label>
                <input type="number" v-model="form.qty"
                  class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-white text-sm focus:outline-none focus:border-amber-500 transition"
                  placeholder="مثال: 300">
              </div>

              <button type="submit" :disabled="loading"
                class="w-full bg-amber-600 hover:bg-amber-500 font-bold py-3 rounded-xl transition shadow-lg text-sm disabled:opacity-50">
                {{ loading ? 'جاري التحقق والتدقيق...' : 'فحص واعتماد الطلب' }}
              </button>
            </form>
          </div>
        </div>

        <div
          class="lg:col-span-2 bg-slate-900 border border-slate-800 p-6 rounded-2xl shadow-xl flex flex-col justify-between">
          <div>
            <h2 class="text-base font-bold text-amber-500 mb-4 pb-2 border-b border-slate-800">
              تقرير وتحليل النظام الذكي
            </h2>

            <div v-if="!agentResponse && !loading"
              class="border border-dashed border-slate-800 rounded-xl p-10 text-center text-slate-500 text-sm">
              قم بتقديم طلب توريد من القائمة الجانبية ليقوم النظام بفحص حصص الشركة والمخزون الفعلي وإصدار القرار هنا.
            </div>

            <div v-if="loading" class="border border-slate-800 bg-slate-950 rounded-xl p-8 text-center space-y-3">
              <div
                class="inline-block w-6 h-6 border-2 border-amber-500 border-t-transparent rounded-full animate-spin">
              </div>
              <p class="text-xs text-slate-400">جاري قراءة سجلات المخزون وتقييم حصة الشركة...</p>
            </div>

            <div v-if="agentResponse && !loading" class="bg-slate-950 border border-slate-800 p-5 rounded-xl space-y-4">
              <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                <span class="text-xs text-slate-400">حالة الطلب:</span>
                <span
                  class="px-3 py-1 bg-emerald-500/10 text-emerald-400 text-xs font-bold rounded-full border border-emerald-500/20">معتمد
                  آلياً</span>
              </div>
              <p class="text-slate-200 text-sm leading-relaxed">{{ agentResponse }}</p>
            </div>
          </div>

          <div class="mt-6 pt-6 border-t border-slate-800">
            <h3 class="text-xs font-semibold text-slate-400 mb-3">سجل أحدث الطلبات المفحوصة</h3>
            <div class="space-y-2">
              <div
                class="flex justify-between items-center text-xs bg-slate-950 p-2.5 rounded-lg border border-slate-800/60">
                <span class="text-slate-300 font-medium">شركة النور للمقاولات - رمل (200م³)</span>
                <span class="text-emerald-400">تم الصرف</span>
              </div>
              <div
                class="flex justify-between items-center text-xs bg-slate-950 p-2.5 rounded-lg border border-slate-800/60">
                <span class="text-slate-300 font-medium">شركة البناء الحديث - زلط (150م³)</span>
                <span class="text-amber-400">موافقة جزئية</span>
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

const inventory = ref([
  { name: 'رمل ناعم', qty: 1500, unit: 'متر مكعب', percentage: 75 },
  { name: 'زلط مسلح', qty: 1200, unit: 'متر مكعب', percentage: 60 },
  { name: 'طوب أسمنتي', qty: 5000, unit: 'قطعة', percentage: 50 },
  { name: 'أسمنت فاخر', qty: 850, unit: 'طن', percentage: 40 }
])

const form = ref({
  company: 'شركة النور للمقاولات',
  material: 'رمل',
  qty: ''
})

const loading = ref(false)
const agentResponse = ref('')

const submitOrder = async () => {
  if (!form.value.qty) return
  loading.value = true
  agentResponse.value = ''

  const apiKey = "AIzaSyDbVr6iyB-PJi1r505mbQASZ87pYCtjGsY"
  const promptText = `أنت مسؤول حوكمة مخازن مواد بناء. المخزون الحالي: رمل 1500م3، زلط 1200م3. الشركة "${form.value.company}" طلبت شراء ${form.value.qty} متر من الـ "${form.value.material}". هل توافق على الطلب أم ترفضه أو تعطيه موافقة جزئية بناءً على المخزون؟ اكتب رداً احترافياً ومباشراً.`

  try {
    const response = await fetch("https://generativelanguage.googleapis.com/v1beta/openai/chat/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${apiKey}`
      },
      body: JSON.stringify({
        model: "gemini-2.5-flash",
        messages: [
          { role: "user", content: promptText }
        ],
        temperature: 0.3
      })
    })

    const data = await response.json()

    if (data.choices && data.choices.length > 0) {
      agentResponse.value = data.choices[0].message.content
    } else {
      agentResponse.value = "حدث خطأ في استجابة النموذج."
    }

  } catch (error) {
    agentResponse.value = "فشل الاتصال بخادم الذكاء الاصطناعي. تأكد من اتصال الإنترنت ومفتاح الـ API."
    console.error(error)
  } finally {
    loading.value = false
  }
}
</script>