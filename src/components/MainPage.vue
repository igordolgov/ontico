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
        <!-- <div class="container"> -->
          <AppFooter />
        <!-- </div> -->
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
.board {
    padding: 1px;
    text-align: center;
}

.board__title {
    font-size: 3.75em;
    font-weight: normal;
    margin: 0;
    padding: 0;
}

.board__alt-title {
    margin: 0 0 0.6em;
    padding: 0;
    color: #C1C1C1;
    font-size: 1.88em;
    font-weight: normal;
}

.board__sub-title {
    margin: 0 auto;
    padding: 0;
    max-width: 16.3em;
    font-size: 1.5em;
    font-weight: normal;
    color: #1A1A1A;
}

.login__link {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    transition: opacity 0.3s ease;
}

.login__link:hover {
    opacity: 0.8;
}

.login__icon {
    width: 27px;
    height: 27px;
}

.login__text {
    margin-left: 6px;
    color: #010000;
    font-size: 16px;
    font-weight: 400;
    letter-spacing: -0.4px;
}

.rescheduled {
    text-align: center;
    margin: 20px 0 130px 0;
}

.rescheduled__link {
    padding: 15px 50px;
    margin: 0 24px;
    display: inline-block;
    color: #fff;
    font-size: 30px;
    line-height: 1.2;
    font-weight: 700;
    text-align: center;
    text-decoration: none;
    background-color: red;
    border-radius: 34px;
    transition: opacity 0.3s ease;
}

.rescheduled__link:hover {
    color: #fff;
    opacity: 0.8;
    text-decoration: none;
}

@media (max-width: 1000px) {
    .rescheduled__link {
        font-size: 24px;
        padding: 15px 25px;
    }
}

@media (max-width: 768px) {
    .board__title {
        font-size: 3em;
    }
    .rescheduled {
        margin-bottom: 24px;
    }
    .rescheduled__link {
        font-size: 18px;
        padding: 15px;
    }
}

@media (max-width: 480px) {
    .board__title {
        font-size: 2.5em;
    }
    .rescheduled__link {
        font-size: 16px;
        padding: 10px;
    }
}

.download {
    margin: 20px 0 20px;
}

.download__link {
    font-size: 1.65em;
}

.calendar__items {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 50px;
    margin-bottom: 230px;
}

.calendar__item-inner {
    font-size: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1 1 auto;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.12);
    padding: 25px 30px 50px;
}

.calendar__item-inner:hover {
    box-shadow: 0 4px 15px rgba(13, 13, 13, 0.5);
    transition: transform .5s linear;
}

.calendar__item-date {
    line-height: 22px;
    margin-bottom: 20px;
}

.calendar__item-logo {
    height: 100px;
    margin-bottom: 15px;
    width: 50%;
    object-fit: contain;
}

.calendar__item-information {
    cursor: default;
    display: flex;
    /* flex-wrap: wrap; */
    flex-direction: column;
    justify-content: space-between;
}

.calendar__item-title {
    font-size: 1.5rem;
    line-height: 1.8rem;
    margin-bottom: 15px;
    /* min-height: 90px; */
}

.calendar__item-text {
    font-size: 16px;
    line-height: 19px;
    margin-bottom: 20px;
}

.calendar__item-adress {
    display: block;
    font-size: 0.875rem;
    line-height: 17px;
    margin-bottom: 12px;
    padding-left: 20px;
    position: relative;
}

.calendar__item-link {
    display: block;
    font-size: 0.875rem;
    line-height: 17px;
    margin-bottom: 35px;
    padding-left: 20px;
    position: relative;
}

.calendar__item-link:hover {
    text-decoration: underline;
}

.calendar__item-adress::before {
    background-image: url('/assets/adress-icon.svg');
    content: "";
    height: 18px;
    left: 0;
    position: absolute;
    top: -5px;
    width: 13px;
}

.calendar__item-link::before {
    background-image: url('/assets/link-icon.svg');
    content: "";
    height: 13px;
    top: 0;
    left: 0;
    position: absolute;
    width: 13px;
}

.calendar__item-buttons {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.calendar__item-purchase {
    background-color: #6B46D4;
    color: #fff;
    font-size: 1.125rem;
    line-height: 22px;
    padding: 10px 20px;
    font-weight: bold;
}

.calendar__item-purchase:hover {
    background-color: #3D12B7;
    color: #fff;
    transition: transform .3s linear;
}

.calendar__item-more {
    color: #6B46D4;
    line-height: 22px;
    font-size: 18px;
    padding: 10px 20px;
    font-weight: bold;
}

.calendar__item-more:hover {
    color: #3D12B7;
    text-decoration: underline;
}

@media (max-width: 720px) {
    .calendar__items {
        gap: 24px;
        margin-bottom: 24px;
    }
}

@media (max-width: 420px) {
    .calendar__item-inner {
        font-size: 70%;
        padding: 25px 20px 50px;
    }
}
</style>
