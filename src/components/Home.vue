<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const goToSubmit = () => {
  const currentUser = JSON.parse(localStorage.getItem('currentUser') || 'null')
  if (currentUser) {
    router.push('/submit')
  } else {
    alert('Подать заявку могут только зарегистрированные пользователи. Пожалуйста, войдите или зарегистрируйтесь.')
    router.push('/account')
  }
}

// Переменные для слайдера
import { ref, onMounted, onBeforeUnmount } from 'vue';

const slidesCount = 3; // число слайдов
const currentSlide = ref(0);
let slideInterval = null;

// Функция для переключения слайда по индексу
function showSlide(index) {
  currentSlide.value = index % slidesCount;
}

// Автоматическое переключение
onMounted(() => {
  slideInterval = setInterval(() => {
    currentSlide.value = (currentSlide.value +1) % slidesCount;
  },5000);
});

onBeforeUnmount(() => {
  clearInterval(slideInterval);
});

</script>
<template>
  <div class="hero">
    <div class="hero-content">
      <h1 class="hero-title">Спаси свой город — начни с одного клика</h1>
      <p class="hero-subtitle">Сообщите о проблемах ЖКХ, благоустройстве, дорогах — мы решим.</p>
      <button class="hero-button" @click="goToSubmit">⚡ Подать заявку</button>
      <p style="color: #FFC48E; font-style: italic; margin-top: 12px;">
  Подать заявку могут только зарегистрированные пользователи.
</p>
    </div>
  </div>

  <div class="main_counter_panel">
    <div class="counter_panel">
      <div class="counter_count">34 287</div>  
      <div class="counter_title">Сообщений поступило</div>
    </div>
    <div class="counter_panel">
      <div class="counter_count">35 665</div>
      <div class="counter_title">Проблем решено</div>
    </div>
    <div class="counter_panel">
      <div class="counter_count">3 453</div>
      <div class="counter_title">В работе</div>
    </div>
  </div>

 <h1 class="section-title">Решенные проблемы</h1>
<div class="slider" id="slider">
  <div class="slides" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
    <div class="slide">
      <img src="/img/one.jpg" height="450px" width="650px" />
      <div class="slide-text">Проблема с освещением решена</div>
    </div>
    <div class="slide">
      <img src="/img/two.jpg" height="450px" width="654px" />
      <div class="slide-text">Обновление асфальта завершено</div>
    </div>
    <div class="slide">
      <img src="/img/three.jpg" height="450px" width="654px" />
      <div class="slide-text">Высадка деревьев выполнена</div>
    </div>
  </div>
  <div class="slider-controls">
    <span
      v-for="(dot, index) in slidesCount"
      :key="index"
      class="slider-dot"
      :class="{ active: index === currentSlide }"
      @click="showSlide(index)"
    ></span>
  </div>
</div>
<!-- Точки управления -->
    
</template>

<style scoped>
/* Эпичный фон */
.hero {
  /*background: linear-gradient(135deg, #028AD2, #006194);*/
  background-color: #E4EFFF;
  padding: 100px 20px;
  color: rgb(0, 0, 0);
  text-align: center;
  animation: fadeIn 1.5s ease-out;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-image: url('/img/fon.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  padding: 50px;
}


.hero-title {
  font-size: 60px;
  font-weight: 900;
  text-shadow: 2px 2px 5px #00000066;
  margin-bottom: 20px;
}

.hero-subtitle {
  font-size: 24px;
  margin-bottom: 40px;
  font-style: italic;
  color: #292e34;
}

.hero-button {
  font-size: 28px;
  background-color: #028AD2;
  color: #000;
  border-color: #000;
  border-radius: 12px;
  padding: 16px 36px;
  cursor: pointer;
  transition: all 0.4s ease;
  box-shadow: 0 8px 24px rgba(0,0,0,0.2);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.hero-button:hover {
  background-color: #006194;
  transform: scale(1.05);
}

.main_counter_panel {
  display: flex;
  justify-content: space-around;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 22px;
  border-radius: 12px;
  gap: 20px;
  flex-wrap: wrap; /* чтобы элементы переносились при необходимости */
  justify-content: space-around; /* равномерное распределение по горизонтали */

}

.counter_panel {
  background: #E4EFFF;
  border: 3px solid #006194;
  border-radius: 16px;
  padding: 30px;
  text-align: center;
  width: 300px;
  transition: transform 0.3s;
  flex: 1 1 auto; /* позволяет элементам расти и сжиматься */
  min-width: 200px; /* минимальная ширина для блока, чтобы не сжимался слишком сильно */
  margin: 10px; /* отступы между блоками */
  text-align: center; /* центрирование текста внутри блока */
}
/* Мобильная версия — вертикальный ряд */
@media (max-width: 768px) {
  .main_counter_panel {
    flex-direction: column; /* все блоки идут вертикально */
    align-items: center; /* по центру по горизонтали */
  }
  
  .counter_panel {
    width: 80%; /* или любой другой размер, подходящий для мобильных */
    margin: 10px 0; /* вертикальные отступы между блоками */
  }
}
.counter_panel:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

.counter_count {
  font-size: 40px;
  font-weight: bold;
  color: #006194;
}

.counter_title {
  margin-top: 12px;
  font-size: 20px;
  color: #333;
}

.section-title {
  text-align: center;
  font-size: 36px;
  
  color: #006194;
  font-weight: 800;
  letter-spacing: 1px;
}

.main_counter_complet {
  display: flex;
  justify-content: space-evenly;
  margin: 40px 60px;
  gap: 30px;
}
h1{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.counet_complet {
  background: #f7faff;
  border: 2px dashed #028AD2;
  border-radius: 14px;
  padding: 24px;
  width: 240px;
  text-align: center;
  transition: all 0.3s ease;
}
.counet_complet:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 15px rgba(0,0,0,0.1);
}

.counet_complet_img {
  font-size: 48px;
  margin-bottom: 12px;
}

.counet_complet_title {
  font-weight: 600;
  font-size: 20px;
  color: #028AD2;
}

/* Анимация появления */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-30px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Стили для слайдера */
.slider {
  position: relative;
  width: 85%;
  height: 450px;
  overflow: hidden;
  background-color:#f0f0f0;
  margin-bottom: 50px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.slides {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.slide {
  min-width:100%;
  display:flex;
  
  justify-content:center;
  font-size:24px;

  position: relative;
  

}

.slide-text {
  position: absolute;
  bottom: 30px; /* Расположение по вертикали */
  left: 50%;
  transform: translateX(-50%);
  color: rgb(0, 0, 0); /* Цвет текста */
  background-color: rgba(167, 188, 196, 0.6); /* Полупрозрачный фон для читаемости */

}

/* Точки навигации */
.slider-controls {
  position:absolute;
  bottom: 0;
  width:100%;
  text-align:center;
}
.slider-dot {
  display:inline-block;
  width:12px;
  height:12px;
  margin:0 5px;
  background-color:#fff;
  border-radius:50%;
 cursor:pointer;
}
.slider-dot.active {
 background-color:#333; 
}

</style>


