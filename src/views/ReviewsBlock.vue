<template>
  <div class="reviews-section">
    <div class="container">
      <h2 class="section-title">Отзывы покупателей</h2>

      <!-- Загрузка -->
      <div v-if="loading && !loaded" class="loading">
        <div class="spinner"></div>
        <p>Загрузка...</p>
      </div>

      <!-- Ошибка -->
      <div v-else-if="apiError" class="error-box">
        <p>❌ {{ apiError }}</p>
        <button @click="loadReviews" class="btn-retry">Повторить</button>
      </div>

      <!-- Список отзывов -->
      <div v-else-if="reviews.length" class="reviews-list">
        <div v-for="item in reviews" :key="item.id" class="review-card">
          <div class="review-top">
            <strong class="name">{{ item.user_name }}</strong>
            <div class="stars">
              <span v-for="s in 5" :key="s" :class="{ on: s <= item.rating }">★</span>
            </div>
            <span class="date">{{ formatDate(item.created_at) }}</span>
          </div>
          <p class="text">{{ item.text }}</p>
        </div>
      </div>

      <!-- Пусто -->
      <div v-else class="empty">
        <p>Пока нет отзывов. Будьте первым!</p>
      </div>

      <!-- Форма -->
      <div class="form-box">
        <h3>Оставить отзыв</h3>
        <form @submit.prevent="sendReview">
          
          <label>Имя *</label>
          <input v-model="form.name" type="text" maxlength="100" placeholder="Ваше имя" :disabled="sending" required>
          
          <label>Оценка *</label>
          <div class="stars-input">
            <span 
              v-for="s in 5" 
              :key="s"
              @click="form.rating = s"
              :class="{ active: s <= form.rating }"
              class="star-btn"
            >★</span>
            <small>Выбрано: {{ form.rating }}/5</small>
          </div>
          
          <label>Отзыв *</label>
          <textarea v-model="form.text" rows="4" maxlength="500" placeholder="Ваш текст..." :disabled="sending" required></textarea>
          <small class="counter">{{ form.text.length }}/500</small>
          
          <div v-if="msg" :class="['msg', msgType]">{{ msg }}</div>
          
          <button type="submit" :disabled="sending" class="btn-send">
            {{ sending ? 'Отправка...' : 'Отправить' }}
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// 🔥 ИСПРАВЛЕНИЕ:
// 1. Убрали двойной /api. 
// 2. Путь должен совпадать с тем, что мы написали в vercel.json (rewrite).
// Если в vercel.json мы писали '/api/:path*', то здесь начинаем сразу с '/api/...'
const API_URL = '/api/ReviewsBlock'

const reviews = ref([])
const loading = ref(false)
const loaded = ref(false)
const apiError = ref(null)
const sending = ref(false)
const msg = ref(null)
const msgType = ref('')

const form = ref({
  name: '',
  text: '',
  rating: 5
})

// Загрузка отзывов
const loadReviews = async () => {
  loading.value = true
  apiError.value = null
  
  try {
    console.log('📡 Запрос к:', API_URL)
    
    const res = await fetch(API_URL, {
      method: 'GET',
      headers: { 'Accept': 'application/json' }
    })
    
    if (!res.ok) throw new Error('Статус: ' + res.status)
    
    const data = await res.json()
    reviews.value = Array.isArray(data) ? data : []
    loaded.value = true
    
  } catch (e) {
    console.error('❌ Ошибка:', e)
    apiError.value = 'Не удалось загрузить отзывы. ' + e.message
  } finally {
    loading.value = false
  }
    // Устанавливаем заголовок вкладки
  document.title = seo.title;
  
  // Находим или создаем мета-тег description
  let metaDescription = document.querySelector('meta[name="description"]');
  
  if (!metaDescription) {
    metaDescription = document.createElement('meta');
    metaDescription.name = 'description';
    document.head.appendChild(metaDescription);
  }
  
  // Обновляем контент
  metaDescription.content = seo.description;
}

// Отправка формы
const sendReview = async () => {
  // Простая валидация
  if (form.value.name.trim().length < 2) return alert('Имя — минимум 2 символа')
  if (form.value.text.trim().length < 10) return alert('Отзыв — минимум 10 символов')
  
  sending.value = true
  msg.value = null
  
  try {
    const res = await fetch(API_URL, {
      method: 'POST',
      headers: { 
        'Content-Type': 'application/json',
        'Accept': 'application/json'
      },
      body: JSON.stringify({
        user_name: form.value.name.trim(),
        rating: form.value.rating,
        text: form.value.text.trim()
      })
    })
    
    const result = await res.json()
    
    if (!res.ok) throw new Error(result.error || result.message || 'Ошибка ' + res.status)
    
    // Успех
    msgType.value = 'success'
    msg.value = '✅ Спасибо! Отзыв отправлен.'
    form.value = { name: '', text: '', rating: 5 }
    
    // Обновляем список
    setTimeout(loadReviews, 1000)
    
  } catch (e) {
    console.error('❌ Ошибка отправки:', e)
    msgType.value = 'error'
    msg.value = '❌ ' + e.message
  } finally {
    sending.value = false
  }
}

// Формат даты
const formatDate = (d) => {
  if (!d) return ''
  return new Date(d).toLocaleDateString('ru-RU', {
    day: 'numeric', month: 'long', year: 'numeric'
  })
}

onMounted(loadReviews)

// Выносим SEO-данные в отдельный объект для чистоты кода
const seo = {
  title: 'Отзывы покупателей о цветах | LAVENDER',
  description: 'Читайте отзывы реальных покупателей о наших букетах и доставке цветов.'
};
</script>
<style scoped> .reviews-section{padding:50px 20px;width:100%;max-width:1200px;margin:0 auto;font-family:'Inter',sans-serif}.container{max-width:100%}.section-title{text-align:center;font-size:1.8rem;margin:0 0 30px;color:#1f2937}.loading,.error-box,.empty{text-align:center;padding:40px 20px;color:#6b7280}.error-box{background:#fee2e2;color:#b91c1c;border-radius:10px}.btn-retry{margin-top:10px;padding:8px 20px;background:#481C69;color:white;border:none;border-radius:6px;cursor:pointer}.spinner{width:35px;height:35px;border:3px solid #e5e7eb;border-top-color:#481C69;border-radius:50%;animation:spin 1s linear infinite;margin:0 auto 15px}@keyframes spin{to{transform:rotate(360deg)}}.reviews-list{display:flex;flex-wrap:wrap;gap:20px;margin-bottom:40px}.review-card{flex:1 1 280px;max-width:350px;background:#fff;padding:20px;border-radius:12px;border:1px solid #e5e7eb}.review-top{display:flex;align-items:center;gap:10px;margin-bottom:12px;flex-wrap:wrap}.name{font-weight:600;color:#1f2937}.stars{color:#e5e7eb;font-size:1.1rem;letter-spacing:2px}.stars .on{color:#f59e0b}.date{margin-left:auto;font-size:0.8rem;color:#9ca3af;white-space:nowrap}.text{margin:0;color:#374151;line-height:1.5;font-size:0.95rem}.form-box{background:#f3f0f7;padding:25px;border-radius:14px;max-width:550px;margin:0 auto}.form-box h3{margin:0 0 20px;text-align:center;color:#481C69}form{display:flex;flex-direction:column;gap:15px}label{font-weight:600;font-size:0.9rem;color:#1f2937}input,textarea{width:100%;padding:10px 12px;border:1px solid #e5e7eb;border-radius:8px;font-size:1rem;font-family:inherit;box-sizing:border-box}input:focus,textarea:focus{outline:none;border-color:#481C69;box-shadow:0 0 0 3px rgba(72,28,105,0.1)}input:disabled,textarea:disabled{background:#f3f4f6;cursor:not-allowed}.counter{text-align:right;font-size:0.75rem;color:#9ca3af;margin-top:-8px}.stars-input{display:flex;align-items:center;gap:8px;flex-wrap:wrap}.star-btn{font-size:1.8rem;color:#e5e7eb;cursor:pointer;transition:transform 0.1s,color 0.1s;line-height:1}.star-btn:hover,.star-btn.active{color:#f59e0b;transform:scale(1.1)}.stars-input small{color:#6b7280;font-size:0.8rem}.msg{padding:10px 14px;border-radius:8px;font-size:0.9rem;font-weight:500}.msg.error{background:#fee2e2;color:#b91c1c}.msg.success{background:#d1fae5;color:#065f46}.btn-send{width:100%;padding:12px;background:#481C69;color:white;border:none;border-radius:8px;font-weight:600;font-size:1rem;cursor:pointer;transition:background 0.2s}.btn-send:hover:not(:disabled){background:#361550}.btn-send:disabled{opacity:0.7;cursor:not-allowed}@media (max-width:768px){.review-card{flex:1 1 100%;max-width:100%}.review-top{flex-direction:column;align-items:flex-start;gap:5px}.date{margin-left:0}.stars-input{gap:4px}.star-btn{font-size:1.5rem}}@media (max-width:480px){.reviews-section{padding:30px 15px}.section-title{font-size:1.4rem}.form-box{padding:20px 15px}input,textarea{padding:9px 10px;font-size:0.95rem}.btn-send{padding:11px;font-size:0.95rem}}</style>
