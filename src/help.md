## Стилизация скроллбара

::-webkit-scrollbar — сама полоса прокрутки  
::-webkit-scrollbar-thumb — ползунок  
::-webkit-scrollbar-track — трек (фон за ползунком)

```css
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-thumb {
  background-color: #888;
  border-radius: 4px;
}
::-webkit-scrollbar-thumb:hover {
  background-color: #555;
}

/* глобальные стили то что я уже юзала, будет как база для всех черно-серое стильно*/
::-webkit-scrollbar {
  width: 12px;
  height: 14px;
}
::-webkit-scrollbar-track {
  background: rgb(42, 42, 42);
  border-radius: 6px;
}
::-webkit-scrollbar-thumb {
  background-color: #929292;
  border-radius: 6px;

}
::-webkit-scrollbar-thumb:hover {
  background-color: #c5c5c5;
}

какая то библиотека для ползунков установить 
npm install vue-slider-component
Run `npm audit` for details.


Переход между страницами без Vue Router (через App.vue и v-if)
В App.vue используется переменная local.page для отображения нужного компонента.

Компоненты (например, Account.vue) отправляют событие @change-page, чтобы изменить текущую страницу.

<!-- App.vue -->
<script setup>
import { reactive } from 'vue'
import Gallery from './components/Gallery.vue'
import Basket from './components/Basket.vue'
import Shop from './components/Shop.vue'
import Account from './components/Account.vue'

// Управление текущей страницей (1 = галерея, 6 = корзина, 7 = заказы, 8 = аккаунт)
const local = reactive({
  page: 1 // начальная страница
})

// Функция смены страницы по событию
function changePage(newPage) {
  local.page = newPage
}
</script>

<template>
  <!-- Показываем компонент в зависимости от local.page -->
  <Gallery v-if="local.page === 1" @change-page="changePage" />
  <Basket v-else-if="local.page === 6" @change-page="changePage" />
  <Shop v-else-if="local.page === 7" />
  <Account v-else-if="local.page === 8" @change-page="changePage" />
</template>


<!-- Пример внутри Account.vue -->
<template>
  <div>
    <!-- Если пользователь зарегистрирован -->
    <div v-if="user">
      <p>Привет, {{ user.name }}!</p>
      <!-- Кнопка перехода к заказам -->
      <button @click="$emit('changePage', 7)">Мои заказы</button>
    </div>
  </div>
</template>


Вариант 1: Очистить localStorage руками
Открой DevTools → вкладка Application

В левой колонке выбери → Local Storage → твой сайт

Найди ключ users

Удали его (ПКМ → Delete)

Перезагрузи страницу

Теперь твой новый код добавит админа заново, с нужным паролем


Удаление привязки к старому Git-репозиторию:
Remove-Item -Recurse -Force .git


git add .
git commit -m "финалочка. здача завтра"
git push
Затем пересобери проект и заново запушь в ветку gh-pages:

bash
Копировать
Редактировать
npm run build
npx gh-pages -d dist