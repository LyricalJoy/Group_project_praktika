<script setup>
import { useRouter } from 'vue-router'
import { ref } from 'vue'

const router = useRouter()
const isUserLoggedIn = ref(false)

// Проверка авторизации (например, из localStorage)
const checkAuth = () => {
  const currentUser = JSON.parse(localStorage.getItem('currentUser') || 'null')
  isUserLoggedIn.value = !!currentUser
}

checkAuth()

const goToSubmit = () => {
  if (isUserLoggedIn.value) {
    router.push('/submit')
  } else {
    alert('Подать заявку могут только зарегистрированные пользователи. Пожалуйста, войдите или зарегистрируйтесь.')
    router.push('/account')
  }
}

const goToMyRequests = () => {
  if (isUserLoggedIn.value) {
    router.push('/my-requests')
  } else {
    alert('Чтобы просмотреть заявки, пожалуйста, войдите или зарегистрируйтесь.')
    router.push('/account')
  }
}
</script>

<template>
  <div class="container">
    <section class="about">
      <article>
        <h2>Городской портал «Сделаем лучше вместе!»</h2>
        <img src="/img/1.jpg" alt="Портал Сделаем лучше вместе" />
        <p>
          Городской портал «Сделаем лучше вместе!» — платформа для взаимодействия жителей Санкт-Петербурга
          с местными властями и друг с другом. Цель — улучшить качество жизни через участие граждан в инициативах
          по благоустройству.
        </p>

        <h2>Основные функции портала</h2>

        <h3>Обратная связь с жителями</h3>
        <p>
          Жители могут оставлять предложения, замечания и жалобы по вопросам городской инфраструктуры и благоустройства.
          Власти оперативно реагируют на потребности граждан.
        </p>

        <h3>Инициативы и проекты</h3>
        <p>
          Информация о текущих и планируемых инициативах, проекты, за которыми можно следить и предлагать свои идеи.
        </p>

        <h3>Информация о событиях</h3>
        <p>
          Новости о реставрации культурных, спортивных и общественных объектов Санкт-Петербурга.
        </p>

        <h2>Преимущества использования портала</h2>

        <h3>Удобство</h3>
        <p>Доступность 24/7 — оставляйте обращения в любое время.</p>

        <h3>Прозрачность</h3>
        <p>
          Граждане видят, как их предложения учитываются местными органами власти.
        </p>

        <h3>Сообщество</h3>
        <p>
          Формируется активное гражданское общество для совместного решения городских проблем.
        </p>

        <h2>Подать заявку</h2>
        <p>Подать заявку могут только зарегистрированные пользователи.</p>
        <button class="submit-button" @click="goToSubmit">⚡ Подать заявку</button>
      </article>

      <article>
        <h3>Ваш статус</h3>
        <p>
          Хотите посмотреть свои заявки? Вы можете следить за их статусом в личном кабинете.
        </p>
        <button class="status-button" @click="goToMyRequests">Посмотреть заявки</button>
      </article>
    </section>
  </div>
</template>

<style scoped>
.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
}

.about {
  display: grid;
  grid-template-columns: 2.5fr 1fr;
  grid-gap: 2rem;
  margin: 2rem 0;
}

.about article {
  background-color: white;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.1);
}

.about article:first-child {
  grid-row: 1 / span 2;
}

.about article:first-child h2 {
  font-size: 2rem;
  font-weight: 900;
  margin-bottom: 1rem;
  color: #028AD2;
}

.about article:first-child img {
  max-width: 100%;
  border-radius: 8px;
  margin-bottom: 1rem;
  object-fit: cover;
  box-shadow: 0 4px 10px rgba(2, 138, 210, 0.3);
}

.about article h3 {
  margin-top: 1.5rem;
  color: #006194;
  font-weight: 700;
}

.submit-button,
.status-button {
  background-color: #FFC48E;
  color: #000;
  border: none;
  border-radius: 12px;
  padding: 12px 28px;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  margin-top: 12px;
  box-shadow: 0 6px 18px rgba(255, 196, 142, 0.6);
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.submit-button:hover,
.status-button:hover {
  background-color: #ff9a3e;
  transform: scale(1.05);
}

.about article:last-child {
  background-color: #028AD2;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  padding: 2rem 1rem;
  border-radius: 12px;
}

.about article:last-child h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.about article:last-child p {
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

/* Мобильная версия */
@media (max-width: 768px) {
  .about {
    grid-template-columns: 1fr;
    margin: 1rem 0;
  }

  /* Убираем закрепление первого элемента */
  .about article:first-child {
    grid-row: auto;
  }

  /* Добавляем отступы между статьями */
  .about article:last-child {
    margin-top: 2rem;
    padding: 1.5rem;
    /* Можно чуть уменьшить, если нужно */
  }

  /* Уменьшаем размеры шрифтов для улучшенной читаемости */
  .about article:first-child h2 {
    font-size: 1.5rem;
  }

  .about article:last-child h3 {
    font-size: 1.2rem;
  }

  .about article p {
    font-size: 1rem;
  }

  /* Кнопки делаем чуть меньше, чтобы не растягивали блок */
  .submit-button,
  .status-button {
    padding: 10px 20px;
    font-size: 16px;
  }
}
</style>