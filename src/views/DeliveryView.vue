<template>
  <div class="delivery-page">
    <div class="container">
      <!-- H1 с основным коммерческим запросом -->
      <header class="page-header">
      <h1 class="page-title">Немного о том как работает наша доставка</h1>
      <p class="subtitle">Привезем на дом или в офис за 2 часа</p>
        <router-link to="/">Перейти в каталог</router-link>
        <router-link to="/product/1">Популярный букет</router-link>
      </header>

      <!-- Основной контент с H2/H3 -->
      <article class="content">
        
        <!-- H2: Коммерческий блок -->
        <section class="section">
          <h2>Как заказать доставку букета</h2>
          <p>
            Мы предлагаем <strong>быструю доставку цветов</strong> по Перми и области. 
            Чтобы <strong>купить букет с доставкой</strong>, выберите понравившуюся композицию 
            в каталоге, добавьте её в корзину и укажите адрес получателя.
          </p>
          
          <h3>Сроки и стоимость доставки</h3>
          <ul class="info-list">
            <li>
              <div>
                <strong>Экспресс-доставка</strong> — от 2 часов
                <span class="detail">Бесплатно при заказе от 5000 ₽</span>
              </div>
            </li>
            <li>
              <div>
                <strong>Доставка к времени</strong> — точно к назначенному часу
                <span class="detail">+300 ₽ к стоимости заказа</span>
              </div>
            </li>
            <li>
              <div>
                <strong>Ночная доставка</strong> — круглосуточно
                <span class="detail">+500 ₽ к стоимости заказа</span>
              </div>
            </li>
          </ul>
        </section>

        <!-- H2: Информационный блок -->
        <section class="section">
          <h2>Зоны доставки цветов</h2>
          <p>
            Мы осуществляем <strong>доставку букетов по всей Перми</strong>
            Курьеры работают во всех округах: Центральный, Северный, Южный, Восточный, Западный.
          </p>

          <div class="zones-grid">
            <div class="zone-card">
              <h4>В пределах Города</h4>
              <p>Бесплатно от 5000 ₽</p>
              <span class="price">от 350 ₽</span>
            </div>
            <div class="zone-card">
              <h4>Пермский край</h4>
              <p>До 30 км от Перми</p>
              <span class="price">от 800 ₽</span>
            </div>
          </div>
        </section>

        <!-- H2: FAQ блок -->
        <section class="section">
          <h2>Частые вопросы о доставке</h2>
          
          <div class="faq-item">
            <h3>Можно ли заказать доставку к точному времени?</h3>
            <p>Да, мы доставляем <strong>цветы к назначенному времени</strong> с точностью до 30 минут. 
            Укажите желаемое время при оформлении заказа.</p>
          </div>

          <div class="faq-item">
            <h3>Как получить скидку на доставку?</h3>
            <p>При заказе от 5000 ₽ <strong>доставка букета бесплатно</strong>. 
            Также мы проводим акции для постоянных клиентов.</p>
          </div>

          <div class="faq-item">
            <h3>Что делать, если получателя нет дома?</h3>
            <p>Курьер свяжется с получателем по телефону. Если не удалось вручить букет, 
            мы согласуем повторную доставку.</p>
          </div>
        </section>

        <!-- Изображение с ALT -->
        <figure class="image-block">
          <img 
            src="../img/img1.webp" 
            alt="Курьер доставляет букет цветов клиенту на дом — быстрая доставка цветов в Перми"
            class="delivery-image"
            loading="lazy"
          >
          <figcaption>Наши курьеры бережно доставят ваш букет в любое время суток</figcaption>
        </figure>

        <!-- CTA блок -->
        <section class="cta-section">
          <h2>Готовы заказать цветы с доставкой?</h2>
          <p>
            <strong>Купить букет с доставкой</strong> можно прямо сейчас в нашем каталоге. 
            Выберите композицию и оформите заказ за 2 минуты!
          </p>
          <router-link to="/" class="btn-primary">
            Перейти в каталог
          </router-link>
        </section>

      </article>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

// Выносим SEO-данные в отдельный объект для чистоты кода
const seo = {
  title: 'Доставка цветов Пермь — купить букет с доставкой недорого | LAVENDER',
  description: 'Быстрая доставка цветов по Перми от 2 часов. Бесплатно при заказе от 5000 ₽. Закажите букет с доставкой на дом или в офис. Скидки постоянным клиентам!',
  subtitle: 'Оформите заказ с доставкой на дом или в офис за 2 часа'
};

onMounted(() => {
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
});
</script>
<style scoped>:root{--primary:#481C69;--primary-dark:#361550;--primary-light:#f3f0f7;--text-main:#1f2937;--text-muted:#6b7280;--bg-page:#f9fafb;--bg-card:#fff;--border:#e5e7eb;--success:#10b981}.delivery-page{background-color:var(--bg-page);min-height:100vh;padding:60px 20px;font-family:'Inter',system-ui,sans-serif;width:100%;max-width:1920px;margin:0 auto;box-sizing:border-box}.container{max-width:900px;margin:0 auto;width:100%}.page-header{text-align:center;margin-bottom:50px}.page-title{font-size:2.5rem;color:var(--primary);margin:0 0 15px;font-weight:800;line-height:1.2}.subtitle{font-size:1.2rem;color:var(--text-muted);margin:0}.content{background:var(--bg-card);border-radius:16px;padding:50px;box-shadow:0 4px 6px -1px rgba(0,0,0,0.05);border:1px solid var(--border)}.section{margin-bottom:50px;padding-bottom:50px;border-bottom:1px solid var(--border)}.section:last-child{border-bottom:none;margin-bottom:0;padding-bottom:0}h2{font-size:1.8rem;color:var(--text-main);margin:0 0 25px;font-weight:700}h3{font-size:1.3rem;color:var(--text-main);margin:30px 0 15px;font-weight:600}h4{font-size:1.1rem;color:var(--text-main);margin:0 0 8px;font-weight:600}p{color:var(--text-muted);line-height:1.7;font-size:1.05rem;margin:0 0 15px}strong{color:var(--text-main);font-weight:600}.info-list{list-style:none;padding:0;margin:20px 0;display:flex;flex-direction:column;gap:15px}.info-list li{display:flex;align-items:flex-start;gap:15px;padding:20px;background:var(--primary-light);border-radius:12px;transition:transform 0.2s}.info-list li:hover{transform:translateY(-2px)}.info-list .icon{font-size:1.5rem;flex-shrink:0;display:flex;align-items:center;justify-content:center;width:40px;height:40px;background:var(--primary);color:white;border-radius:50%}.info-list .detail{display:block;font-size:0.9rem;color:var(--text-muted);margin-top:5px}.zones-grid{display:flex;flex-wrap:wrap;gap:20px;margin:20px 0}.zone-card{flex:1 1 200px;background:var(--primary-light);padding:25px 20px;border-radius:12px;text-align:center;border:1px solid var(--border);display:flex;flex-direction:column;justify-content:center;align-items:center;transition:transform 0.2s,box-shadow 0.2s}.zone-card:hover{transform:translateY(-4px);box-shadow:0 4px 12px rgba(0,0,0,0.05)}.zone-card .price{display:block;font-size:1.4rem;font-weight:700;color:var(--primary);margin-top:10px}.faq-item{background:var(--bg-page);padding:25px;border-radius:12px;margin-bottom:15px;border:1px solid var(--border);transition:border-color 0.2s}.faq-item:hover{border-color:var(--primary)}.faq-item:last-child{margin-bottom:0}.faq-item h3{margin-top:0;font-size:1.1rem;color:var(--primary)}.faq-item p{margin:0;font-size:0.95rem}.image-block{margin:30px 0;text-align:center}.delivery-image{max-width:100%;height:auto;border-radius:12px;box-shadow:0 10px 15px -3px rgba(0,0,0,0.1);display:block;margin:0 auto}.image-block figcaption{font-size:0.9rem;color:var(--text-muted);margin-top:10px;font-style:italic}.cta-section{text-align:center;background:linear-gradient(135deg,var(--primary),var(--primary-dark));padding:50px 40px;border-radius:16px;color:#000;margin-top:30px}.cta-section h2{color:#000;margin-bottom:15px}.cta-section p{color:rgba(0,0,0,0.9);margin-bottom:25px;font-size:1.1rem}.cta-section strong{color:#4e095c}.btn-primary{display:inline-block;background:white;color:var(--primary);padding:16px 36px;border-radius:10px;font-weight:600;text-decoration:none;transition:all 0.2s;font-size:1rem}.btn-primary:hover{transform:translateY(-2px);box-shadow:0 10px 20px rgba(0,0,0,0.2);background:var(--primary-light)}@media (max-width:991px){.delivery-page{padding:50px 20px}.page-title{font-size:2.2rem}.content{padding:40px}h2{font-size:1.6rem}.zone-card{flex:1 1 45%}}@media (max-width:767px){.delivery-page{padding:40px 20px}.page-header{margin-bottom:30px}.page-title{font-size:1.8rem}.subtitle{font-size:1rem}.content{padding:30px;border-radius:12px}h2{font-size:1.4rem;margin-bottom:20px}h3{font-size:1.2rem;margin-top:25px}p{font-size:1rem}.info-list li{padding:15px;gap:12px}.info-list .icon{width:35px;height:35px;font-size:1.2rem}.zones-grid{flex-direction:column}.zone-card{flex:1 1 100%;padding:20px}.cta-section{padding:30px 20px}}@media (max-width:479px){.delivery-page{padding:30px 15px}.page-title{font-size:1.5rem;margin-bottom:10px}.subtitle{font-size:0.95rem}.content{padding:20px;border-radius:10px}.section{margin-bottom:30px;padding-bottom:30px}h2{font-size:1.3rem}h3{font-size:1.1rem;margin-top:20px}p{font-size:0.95rem;line-height:1.6}.info-list li{flex-direction:column;align-items:center;text-align:center;padding:20px 15px}.info-list .icon{margin-bottom:10px}.zone-card .price{font-size:1.2rem}.faq-item{padding:20px 15px}.faq-item h3{font-size:1rem}.faq-item p{font-size:0.9rem}.cta-section h2{font-size:1.3rem}.cta-section p{font-size:0.95rem}.btn-primary{width:100%;padding:14px 20px;font-size:0.95rem}}</style>
