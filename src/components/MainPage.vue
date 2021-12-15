<template>
  <div class="hello">
    <main class="main">
      <div>
        <div class="board">
          <h1 class="board__title">Конференции Олега Бунина</h1>
          <h2 class="board__alt-title">Онтико</h2>
        </div>

        <div class="login">
          <div class="container">
            <a
              class="login__link"
              href="http://conf.ontico.ru/users/profile.html"
              target="_blank"
            >
              <svg
                class="login__icon"
                xmlns="http://www.w3.org/2000/svg"
                width="27"
                height="27"
                viewbox="0 0 27 27"
              >
                <path
                  d="M13.5 0C6.04297 0 0 6.04297 0 13.5S6.04297 27 13.5 27 27 20.95703 27 13.5 20.95703 0 13.5 0zm.03906 19.86719H7.69141c0-4.21485 3.70312-4.21485 4.52734-5.3164l.09375-.50391c-1.15625-.58594-1.97266-1.9961-1.97266-3.64454 0-2.17578 1.41407-3.9375 3.16016-3.9375 1.74219 0 3.15625 1.76172 3.15625 3.9375 0 1.63282-.80078 3.03516-1.9375 3.63282l.10547.5703c.90234 1.04688 4.48437 1.1172 4.48437 5.26173zm0 0"
                ></path>
              </svg>

              <span class="login__text">Личный кабинет</span>
            </a>
          </div>
        </div>

        <!-- Calendar -->
        <div class="rescheduled">
          <a
            class="rescheduled__link"
            href="https://conf.ontico.ru/new-dates.html"
            target="_blank"
            >Изменения дат проведения конференций 2021-2022</a
          >
        </div>

        <div class="calendar" style="background-color: #ffffff">
          <div class="container">
            <div class="calendar__items">
              <div
                v-for="(item, index) in calendarItemsData.result"
                :key="index"
                class="calendar__item-inner"
              >
                <a :href="item.uri" class="calendar__item-information">
                  <h3 class="calendar__item-date">{{ item.date_range }}</h3>
                  <img
                    class="calendar__item-logo"
                    :src="item.logo"
                    alt="logo"
                  />
                  <h5 class="calendar__item-title">{{ item.name }}</h5>
                  <p class="calendar__item-text">{{ item.brief }}</p>
                </a>

                <div class="calendar__item-links">
                  <a class="calendar__item-adress" href="#">{{ item.location }}</a>
                  <a class="calendar__item-link" :href="item.uri">{{ item.uri }}</a>
                  <div class="calendar__item-buttons">
                    <a class="calendar__item-purchase" href="#">Купить билет</a>
                    <a class="calendar__item-more" href="#">Подробнее</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- /Calendar -->
      </div>

      <div class="footer" id="contacts">
        <div class="container">
          <AppFooter />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import AppFooter from "@/components/AppFooter";
import axios from "axios";

export default {
  name: "MainPage",

  components: { AppFooter },

  data() {
    // Хранилище
    return {
      calendarItemsData: null, // Переменная для хранения ответов из API

      calendarItems() {
        return this.calendarItemsData ? this.calendarItemsData.result : [];
      },
    };
  },

  methods: {
    loadCalendarItems() {
      axios
        .get("https://conf.ontico.ru/api/conferences/forCalendar.json")
        .then((response) => (this.calendarItemsData = response.data));
    },
  },

  created() {
    // При загрузке приложения запускать следующие методы
    this.loadCalendarItems();
  },
};
</script>

<style scoped>
</style>
