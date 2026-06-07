
<template>
  <div class="team-page">
    <div class="container">
      <header class="team-header">
        <h1 class="page-title">Наша команда</h1>
        <p class="subtitle">Профессионалы, которые создают красоту для вас</p>
      </header>

      <div class="team-grid">
        <div v-for="member in teamMembers" :key="member.id" class="team-card">
          <div class="member-photo">
            <img :src="member.photo" :alt="`${member.name} ${member.surname}`" loading="lazy">
          </div>
          <div class="member-info">
            <h3 class="member-name">{{ member.name }} {{ member.surname }}</h3>
            <p class="member-position">{{ member.position }}</p>
            <div class="member-contacts">
                {{ member.phone }}
                {{ member.email }}
            </div>
            <div class="member-quote">
              
              <p>"{{ member.quote }}"</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { onMounted } from 'vue';
const teamMembers = ref([
  {
    id: 1,
    name: 'Анна',
    surname: 'Цветкова',
    position: 'Главный флорист',
    phone: '+7 (999) 123-45-67',
    email: 'anna@lavender.ru',
    photo: "https://img.freepik.com/premium-photo/portrait-young-woman-standing-against-plants_1048944-21369490.jpg?semt=ais_hybrid&w=740&q=80",
    quote: 'Каждый букет — это история любви, которую я помогаю рассказать.'
  },
  {
    id: 2,
    name: 'Михаил',
    surname: 'Садовников',
    position: 'Менеджер по закупкам',
    phone: '+7 (999) 234-56-78',
    email: 'mikhail@lavender.ru',
    photo: 'https://pikaso.cdnpk.net/private/production/3774947885/render.jpg?token=exp=1775001600~hmac=95c58f6cbfac185b2e123c9a1ad8481adc585f87ee64739d24077eefade6eadd&preview=true',
    quote: 'Только свежие цветы от проверенных поставщиков.'
  },
  {
    id: 3,
    name: 'Елена',
    surname: 'Доставкина',
    position: 'Руководитель службы доставки',
    phone: '+7 (999) 345-67-89',
    email: 'elena@lavender.ru',
    photo: 'https://pikaso.cdnpk.net/private/production/3774932460/render.png?token=exp=1775001600~hmac=e64738526ea01e9db953f82c54305454923bb1795ab692c3446ab04657dd5a17&preview=1',
    quote: 'Доставим вовремя, в любую погоду, с улыбкой!'
  }
]);


// Выносим SEO-данные в отдельный объект для чистоты кода
const seo = {
  title: 'Наша команда флористов | LAVENDER',
  description: 'Познакомьтесь с командой профессиональных флористов LAVENDER. Создаем красоту для вас.'
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

<style scoped>:root{--primary:#481C69;--primary-light:#f3f0f7;--text-main:#1f2937;--text-muted:#6b7280;--bg-page:#f9fafb;--bg-card:#fff;--border:#e5e7eb}.team-page{background-color:var(--bg-page);min-height:100vh;padding:60px 20px;font-family:'Inter',system-ui,sans-serif;width:100%;max-width:1920px;margin:0 auto;box-sizing:border-box}.container{max-width:1400px;margin:0 auto;width:100%}.team-header{text-align:center;margin-bottom:60px}.page-title{font-size:2.5rem;color:var(--primary);margin:0 0 15px;font-weight:800;line-height:1.2}.subtitle{font-size:1.1rem;color:var(--text-muted);margin:0;max-width:600px;margin-left:auto;margin-right:auto}.team-grid{display:flex;flex-wrap:wrap;gap:30px;justify-content:center}.team-card{flex:1 1 280px;max-width:350px;background:var(--bg-card);border-radius:16px;overflow:hidden;box-shadow:0 4px 6px -1px rgba(0,0,0,0.05);border:1px solid var(--border);transition:transform 0.3s,box-shadow 0.3s;display:flex;flex-direction:column}.team-card:hover{transform:translateY(-8px);box-shadow:0 20px 25px -5px rgba(0,0,0,0.1)}.member-photo{width:100%;height:280px;overflow:hidden;flex-shrink:0}.member-photo img{width:100%;height:100%;object-fit:cover;transition:transform 0.5s ease}.team-card:hover .member-photo img{transform:scale(1.05)}.member-info{padding:24px;display:flex;flex-direction:column;flex-grow:1}.member-name{font-size:1.25rem;color:var(--text-main);margin:0 0 8px;font-weight:700}.member-position{color:var(--primary);font-weight:600;font-size:0.95rem;margin:0 0 16px}.member-contacts{display:flex;flex-direction:column;gap:10px;margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid var(--border)}.contact-link{display:flex;align-items:center;gap:8px;color:var(--text-muted);text-decoration:none;font-size:0.9rem;transition:color 0.2s}.contact-link:hover{color:var(--primary)}.member-quote{background:var(--primary-light);padding:16px;border-radius:12px;position:relative;margin-top:auto}.quote-icon{color:var(--primary);opacity:0.3;margin-bottom:8px;font-size:1.5rem}.member-quote p{margin:0;font-size:0.9rem;color:var(--text-main);font-style:italic;line-height:1.5}@media (max-width:991px){.team-page{padding:50px 20px}.page-title{font-size:2.2rem}.subtitle{font-size:1rem}.team-header{margin-bottom:50px}.team-card{flex:1 1 45%;max-width:45%}.member-photo{height:260px}.member-info{padding:20px}}@media (max-width:767px){.team-page{padding:40px 15px}.page-title{font-size:1.8rem}.subtitle{font-size:0.95rem}.team-header{margin-bottom:40px}.team-grid{gap:25px}.team-card{flex:1 1 48%;max-width:48%}.member-photo{height:240px}.member-name{font-size:1.1rem}.member-position{font-size:0.9rem}.member-info{padding:18px}.member-quote p{font-size:0.85rem}}@media (max-width:479px){.team-page{padding:30px 12px}.page-title{font-size:1.5rem;margin-bottom:10px}.subtitle{font-size:0.9rem}.team-header{margin-bottom:30px}.team-grid{gap:20px}.team-card{flex:1 1 100%;max-width:100%}.member-photo{height:220px}.member-info{padding:16px}.member-name{font-size:1.1rem}.member-position{font-size:0.85rem;margin-bottom:12px}.member-contacts{gap:8px;margin-bottom:16px;padding-bottom:16px}.contact-link{font-size:0.85rem;gap:6px}.member-quote{padding:14px;border-radius:10px}.quote-icon{font-size:1.2rem;margin-bottom:6px}.member-quote p{font-size:0.85rem;line-height:1.4}}</style>
