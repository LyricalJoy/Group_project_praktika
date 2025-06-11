<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const isMenuOpen = ref(false)
const currentUser = ref(null)

// Добавление админа при первом запуске
const users = JSON.parse(localStorage.getItem('users') || '[]')
if (!users.find(u => u.login === 'admin')) {
  users.push({
    login: 'admin',
    password: 'adminWSR',
    firstName: 'Димка',
    lastName: 'Админ',
    middleName: 'Администраторович',
    email: 'admin@example.com',
    role: 'admin',
  })
  localStorage.setItem('users', JSON.stringify(users))
}

// Получение текущего пользователя при загрузке приложения
onMounted(() => {
  const storedUser = localStorage.getItem('currentUser')
  if (storedUser) {
    currentUser.value = JSON.parse(storedUser)
  }
})

// Обработка успешного входа из Account.vue
function handleLoginSuccess(user) {
  currentUser.value = user
  localStorage.setItem('currentUser', JSON.stringify(user))
}

// Обработка выхода из аккаунта — очистка currentUser и localStorage
function handleLogout() {
  currentUser.value = null
  localStorage.removeItem('currentUser')
  router.push('/account') // после выхода редирект на страницу аккаунта
}

function goToSubmitApplication() {
  router.push('/submit')
}
function goToMyRequests() {
  router.push('/my-requests')
}

function goToAdminPanel() {
  router.push('/panel')
}

// Переключение меню
function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}

// Переход по маршруту и закрытие меню
function goTo(path) {
  router.push(path)
  isMenuOpen.value = false
}

// Навигационные охранники — базовая проверка доступа к страницам
router.beforeEach((to, from, next) => {
  const publicPages = ['/', '/news', '/about', '/account', '/login', '/register']
  const authRequired = !publicPages.includes(to.path)
  const user = JSON.parse(localStorage.getItem('currentUser'))

  if (authRequired && !user) {
    // Если страница требует авторизации, но пользователь не залогинен — редирект на аккаунт
    next('/account')
  } else if (to.path === '/panel' && user?.role !== 'admin') {
    // Если пользователь не админ пытается зайти на панель админа — редирект на главную
    next('/')
  } else {
    next()
  }
})
</script>

<template>
  <div class="app-wrapper">
    <nav class="navbar">
      <div class="navbar-top">
        <!-- Гамбургер -->
        <button class="hamburger" @click="toggleMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>

        <!-- Логотип -->
        <img
          src="/img/logo.png"
          alt="Логотип"
          class="logo"
          @click="goTo('/')"
        />

        <!-- Десктопное меню -->
        <div class="menu-buttons">
          <button @click="goTo('/')">Главная</button>
          <button @click="goTo('/news')">Новости</button>
          <button @click="goTo('/about')">О портале</button>

          <template v-if="currentUser?.role === 'admin'">
            <button @click="goTo('/panel')">Панель управления</button>
          </template>
          <template v-else-if="currentUser">
            <button @click="goTo('/submit')">Подать заявку</button>
            <button @click="goTo('/my-requests')">Мои заявки</button>
          </template>
        </div>


        <template v-if="currentUser && currentUser.role !== 'admin'">
          <div class="welcome-message">
            Добро пожаловать, {{ currentUser.firstName }}!
          </div>
        </template>

        <template v-if="currentUser?.role === 'admin'">
          <div class="welcome-message">
            С возвращением, Администратор!
          </div>
        </template>


        <!-- Иконка аккаунта -->
        <img
          src="/img/icon_1.png"
          alt="Аккаунт"
          class="account-icon"
          @click="goTo('/account')"
        />
      </div>

      <!-- Мобильное меню -->
      <div v-if="isMenuOpen" class="mobile-menu">
        <button @click="goTo('/')">Главная</button>
        <button @click="goTo('/news')">Новости</button>
        <button @click="goTo('/about')">О портале</button>

        <template v-if="currentUser?.role === 'admin'">
          <button @click="goTo('/panel')">Панель управления</button>
        </template>
        <template v-else-if="currentUser">
          <button @click="goTo('/submit')">Подать заявку</button>
          <button @click="goTo('/my-requests')">Мои заявки</button>
        </template>

        <button @click="goTo('/account')">Аккаунт</button>
      </div>
    </nav>

    <div class="main">
      <router-view
        @login-success="handleLoginSuccess"
        @logout="handleLogout"
        @submit-application="goToSubmitApplication"
        @open-admin-panel="goToAdminPanel"
        @open-my-requests="goToMyRequests"
      />
    </div>

  <footer>
    <div class="footer-content">
    <div>
      <h4>Мы в соцсетях</h4>
<div class="social-links">
  <a href="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Bbno%24_Twitchcon_2024.jpg/500px-Bbno%24_Twitchcon_2024.jpg" target="_blank" aria-label="VK">
    <i class="fab fa-vk"></i>
  </a>
  <a href="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Bbno%24_Twitchcon_2024.jpg/500px-Bbno%24_Twitchcon_2024.jpg" target="_blank" aria-label="Telegram">
    <i class="fab fa-telegram"></i>
  </a>
  <a href="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Bbno%24_Twitchcon_2024.jpg/500px-Bbno%24_Twitchcon_2024.jpg" target="_blank" aria-label="YouTube">
    <i class="fab fa-youtube"></i>
  </a>
</div>
    </div>
      <div class="footer_text">
        <p>Спасибо что помогаете сделать наш город лучше!</p>
      <p>&copy; 2025 Городской портал. Все права защищены.</p>
      </div>
      <div>
      <h4>Контакты</h4>
        <p>г. Санкт-Петербург, ул. Ординарная, 10</p>
        <p>Тел. +7 (968) 298-23-56</p>
        <p>Email: info@cityportal.ru</p>
      </div>
    </div>
  </footer>

  
</div>

</template>


<style scoped>

.welcome-message {
  font-size: 16px;
  font-family: Arial, Helvetica, sans-serif;
  margin-right: -100px;
  color: #444;
}

.navbar,
.main,
footer {
  max-width: 1500px;
  width: 100%;    
  margin: 0 auto;    
  padding: 0 16px;
}



.navbar {
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.navbar-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 70px;
}

/* Гамбургер */
.hamburger {
  display: none;
  flex-direction: column;
  gap: 4px;
  cursor: pointer;
  margin-right: 12px;
  background-color: white;
  border-color: #61adff;
}
.hamburger span {
  width: 24px;
  height: 3px;
  background: #333;
}

/* Логотип */
.logo {
  height: 80px;
  cursor: pointer;
}
.logo:hover {
  transform: scale(1.3);
  transition: transform 0.8s;
}

/* Меню для десктопа */
.menu-buttons {
  display: flex;
  gap: 16px;
}
.menu-buttons button {
  background: none;
  border: none;
  font-size: 16px;
  color: #444;
  cursor: pointer;
  transition: color 0.5s;
}
.menu-buttons button:hover {
  color: #007bff;
}

/* Иконка аккаунта */
.account-icon {
  height: 32px;
  cursor: pointer;
}
.account-icon:hover {
  transform: scale(1.3);
  transition: transform 0.8s;
}

/* Мобильное меню */
.mobile-menu {
  display: none;
  flex-direction: column;
  background: #f9f9f9;
  padding: 16px;
}
.mobile-menu button {
  background: none;
  border: none;
  font-size: 16px;
  padding: 8px 0;
  text-align: left;
  cursor: pointer;
  color: #333;
}

/* Адаптация */
@media (max-width: 720px) {

  .navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
.main {
  padding-top: 140px; /* чтобы контент не прятался под navbar */
}
    /* Отступ слева для иконки аккаунта */
    .account-icon {
    margin-left: 10px;
  }
  .navbar-top {
    padding: 10px 10px; /* убрать большие отступы */
  }
  .welcome-message {
    display: none; /* убрать приветствие */
  }
  .menu-buttons {
    display: none;
  }
  footer .footer_text {
    padding-top: 15px; /* уменьшить большой отступ */
  }
  .hamburger {
    display: flex;
  }
  .footer-content {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  footer h4,
  footer p {
    width: 100%;
    text-align: center;
  }
  
  footer {
  color: white;
  margin-top: auto; /* этот отступ толкает футер вниз */
  background-color: rgb(108, 165, 222);
  width: 100%;
  text-align: center; /* по центру текст внутри футера */
}

  .mobile-menu {
    display: flex;
  }
}
.main {
  background-color: rgba(165, 214, 255, 0.786);
  padding-top: 50px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.footer-content {
  padding: 25px;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}
.social-links {
  display: flex;
  gap: 16px;
  margin-top: 8px;
  align-items: center;
}

.social-links a {
  font-size: 36px;
  color: #ffffff;
  transition: color 0.3s;
}

.social-links a:hover {
  color: #ffb458;
}

.app-wrapper {
  min-height: 100vh;       /* высота окна браузера */
  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* контент сверху */
}

footer {
  color: white;
  margin-top: auto; /* этот отступ толкает футер вниз */
  background-color: rgb(108, 165, 222);
  width: 100%;
  text-align: center; /* по центру текст внутри футера */
}

.footer_text {
  padding-top: 50px;

}

</style>
