<script setup>
</script>

<template>
  <header class="showcase">
    <div class="container">
      <div class="text-content">
        <p class="problem-category">Проблема мусора</p>
        <h1>Решении проблем мусора</h1>
        <p>
          Из ежегодных жалоб из разных районов Санкт-Петербурга по загрязнению мусором
          центрального и спального районов поставило вопрос о наибольшем финансировании
          мэрией Санкт-Петербурга на финансирование городских служб по устранению загрязнения на улицах.
          Пожалуйста, сообщайте о проблемах мусора вашего района в наш городской портал.
        </p>
        <a href="src\???">Посмотреть</a>
      </div>
    </div>
  </header>

  <section>
    <div class="container">
      <h1 class="editor-h1">Актуальные Новости</h1>
      <div class="articles">
        <a href="src\???" class="card">
          <img src="/img/articles/ent1.jpg" alt="" />
          <article>
            <p class="road-category">Ремонт дорог</p>
            <h1>На 15 октября планируется перекрытие улицы</h1>
            <p>
              В связи с ухудшением состояния асфальтового покрытия на улице Ленина,
              начнется ремонт с 15 октября. Пожалуйста, сообщайте о проблемах.
            </p>
          </article>
        </a>

        <a href="src\???" class="card">
          <article>
            <p class="problem-category">Безопасность</p>
            <h1>Криминал на улицах</h1>
            <p>
              В связи с увеличением числа краж в районе Центрального рынка,
              мы призываем жителей сообщать о подозрительных лицах.
            </p>
          </article>
        </a>

        <a href="src\???" class="card">
          <img src="/img/articles/greenery1.jpg" alt="" />
          <article>
            <p class="green-category">Парки и скверы:</p>
            <h1>Благоустройства парка</h1>
            <p>
              В парке Победы начнется благоустройство. Если вы заметили поврежденные скамейки или дорожки,
              сообщите нам.
            </p>
          </article>
        </a>

        <a href="src\???" class="card">
          <article>
            <p class="problem-category">Водоснабжение</p>
            <h1>Проблема с перебоями воды</h1>
            <p>
              В некоторых районах города наблюдаются перебои с водоснабжением.
              Пожалуйста, сообщайте о проблемах для оперативного реагирования.
            </p>
          </article>
          <img src="/img/articles/water.jpg" alt="" />
        </a>

        <a href="src\???" class="card">
          <img src="/img/articles/greenery2.jpg" alt="" />
          <article>
            <p class="green-category">Зеленые насаждения</p>
            <h1>Нехватка живой природы</h1>
            <p>
              В рамках программы по озеленению города мы планируем высадку деревьев.
              Сообщайте о местах, где не хватает зелени.
            </p>
          </article>
        </a>

        <a href="src\???" class="card">
          <article>
            <p class="problem-category">Освещение</p>
            <h1>Проблема с электричеством</h1>
            <p>
              В нескольких районах города зафиксированы проблемы с уличным освещением.
              Мы призываем жителей сообщать о неработающих фонарях.
            </p>
          </article>
        </a>

        <a href="src\???" class="card">
          <article>
            <p class="road-category">Транспорт</p>
            <h1>Ухудшение общественного транспорта</h1>
            <p>
              В связи с увеличением числа жалоб на общественный транспорт,
              мы запускаем опрос для улучшения качества обслуживания. Ваше мнение важно!
            </p>
          </article>
          <img src="/img/articles/ent2.jpg" alt="" />
        </a>
      </div>
    </div>
  </section>
  <div style="height: 100px;"></div>
</template>


<style scoped>
/* =====
SHOWCASE
===== */
:root {
  --headings-font: "Handlee", cursive;
  --primary-color: rgb(240, 37, 37);
  --light-grey-color: rgb(243, 243, 243);
  --dark-color: rgb(46, 46, 46);
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

p {
  line-height: 1.5rem;
  padding: 0.5rem 0rem;
}

h1,
h2,
h3 {
  font-family: "Quicksand", sans-serif;
}

.container {
  max-width: 1100px;
  padding: 0px 20px;
  margin: auto;
}

body {
  background-color: var(--light-grey-color);
}

img {
  width: 100%;
}

.problem-category,
.road-category,
.green-category {
  display: inline-block;
  text-transform: uppercase;
  font-size: 0.7rem;
  padding: 2px 20px;
  border-radius: 50px;
  color: white;
  margin: 0.5rem 0rem;
}

.problem-category {
  background-color: orange;
}

.road-category {
  background-color: rgb(186, 98, 197);
}

.green-category {
  background-color: rgb(0, 151, 245);
}

.showcase {
  position: relative;
  color: white;
  height: 60vh;
  background: url(images/background.jpg) center center/cover;
}

.showcase::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
}

.showcase .container {
  height: inherit;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-content: center;
}

.showcase .text-content {
  position: relative;
  padding: 0px 30px;
}

.showcase .text-content h1 {
  text-transform: uppercase;
  font-size: 1.6rem;
  margin: 10px 0px;
  letter-spacing: 1px;
  font-family: var(--headings-font);
}

.showcase .text-content p:nth-child(3) {
  text-align: justify;
}

.showcase .text-content a {
  text-decoration: none;
  padding: 10px 15px;
  font-size: 1.05rem;
  font-weight: 400;
  display: inline-block;
  color: white;
  letter-spacing: 1px;
  background-color: var(--primary-color);
  margin-top: 10px;
}

.showcase .text-content a:hover {
  background-color: var(--light-grey-color);
  color: black !important;
}





/* =====
ARTICLES
===== */

.editor-h1 {
  font-size: 1.6rem;
  margin: 1rem 0rem;
  letter-spacing: 1px;
}

.articles {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 1rem;
}

.articles>a:nth-child(1),
.articles>a:last-child {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1rem;
  grid-column: 1 / span 2;
  align-items: center;
}

.articles>a:last-child {
  grid-column: 2 / span 2;
}

.articles>a:nth-child(2) {
  background-color: var(--dark-color);
  color: white;
}

.articles>a:nth-child(6) {
  background-color: var(--primary-color);
  color: white;
}

.card {
  background-color: white;
  padding: 1rem;
  text-decoration: none;
  color: black;
}

.card:hover {
  box-shadow: 3px 5px 10px rgb(199, 199, 199);
}


/* Общие стили для мобильных устройств */
@media (max-width: 768px) {

  /* Универсальные настройки */
  body {
    font-size: 14px;
  }

  /* Контейнеры */
  .container {
    padding: 0 10px;
  }

  /* Showcase */
  .showcase {
    height: auto;
    padding: 20px 0;
  }

  .showcase .container {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .showcase .text-content {
    padding: 0 10px;
  }

  .showcase .text-content h1 {
    font-size: 1.2rem;
  }

  .showcase .text-content p:nth-child(3) {
    text-align: justify;
  }

  .showcase .text-content a {
    padding: 8px 12px;
    font-size: 1rem;
    margin-top: 10px;
  }

  /* Категории */
  .problem-category,
  .road-category,
  .green-category {
    display: inline-block;
    font-size: 0.6rem;
    padding: 2px 12px;
    margin: 0.3rem 0;
  }

  /* Articles grid */
  .articles {
    display: block;
  }

  .articles>a {
    display: block;
    margin-bottom: 1rem;
  }

  .articles>a:nth-child(1),
  .articles>a:last-child {
    grid-column: auto;
  }

  /* Убираем двухколоночность у карточек внутри */
  .articles>a:nth-child(1),
  .articles>a:last-child {
    grid-template-columns: 1fr;
  }

  /* Для карточек внутри */
  .card {
    padding: 0.8rem;
  }
}
</style>
