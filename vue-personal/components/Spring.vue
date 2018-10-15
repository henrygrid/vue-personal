<template>
  <section class="slide slide-2 projects spring hidden-slide">
    <div class="home--wrapper">
      <div class="home__content">
        <section class="home__content__header">
          <div v-if="$props.searchCommitted === true" class="spring__day__wrapper">
            <div class="spring__day__toggle__container">
              <span class="spring__day__one__title">1 Day</span>
              <label class="spring__switch" for="checkbox">
                <input type="checkbox" id="spring-checkbox" @click="viewToggle" />
                <div class="spring__slider round"></div>
              </label>
              <span class="spring__day__five__title">5 Day</span>
            </div>
            <h1 class="spring__city">{{ weather.weatherData.city.name }}</h1>
            <ul v-if="viewStatus === 1" :class=" [ viewStatus < 3 ? 'one-day-list': 'five-day-list'] + ' spring__day__list'">
              <li class="spring__day__list__item">
                <h1 class="spring__day__date">{{ getWeatherMonth($props.weatherData.list[0].dt_txt) }} {{ getWeatherDay($props.weatherData.list[0].dt_txt) }}</h1>
                <div v-bind:class="weatherClass + ' spring__day__image'"></div>
                <p class="spring__day__temp--high">{{ Math.floor($props.weatherData.list[0].main.temp) }} &#8457;</p>
                <p class="spring__day__temp--low">{{ Math.floor($props.weatherData.list[0].wind.speed) }} mph</p>
              </li>
            </ul>
            <ul v-else-if="viewStatus === 5" :class=" [ viewStatus < 3 ? 'one-day-list': 'five-day-list'] + ' spring__day__list'">
              <li v-for="(day, index) in getFiveDay($props.weatherData.list)" v-bind:key="`day-${index}`"  class="spring__day__list__item">
                <div>
                  <h1 class="spring__day__date">{{ getWeatherMonth(day.dt_txt) }} {{ getWeatherDay(day.dt_txt) }}</h1>
                  <div v-bind:class="getWeatherClass(day.weather[0].id) + ' spring__day__image'"></div>
                  <p class="spring__day__temp--high">{{ Math.floor(day.main.temp) }} &#8457;</p>
                  <p class="spring__day__temp--low">{{ Math.floor(day.wind.speed) }} mph</p>
                </div>
              </li>
            </ul>
          </div>
          <!-- <h1 class="home__content__header__heading">Henry Morrow - Web Developer</h1>
          <p class="home__content__header__description">Your year-round source for a great web presence.</p>
          <a class="home__content__header__link" href="">View my work</a> -->
          <!-- <div class="menu__button">
            <div class="snowflake"></div>
            <div class="ham-container" @click="toggleMenu">
              <span class="ham ham-top"></span>
              <span class="ham ham-middle"></span>
              <span class="ham ham-bottom"></span>
            </div>
          </div> -->
        </section>
        <!-- <section class="home__content__intro">
          <div class="home__content__intro__container">
            <h1 class="home__content__intro__heading">You wanna know how I got them? So I had a wife. She was beautiful, like you, who tells me I worry too much, who tells me I ought to smile more, who gambles and gets in deep with the sharks. Hey. One day they carve her face. And we have no money for surgeries. She can't take it. I just wanna see her smile again. I just want her to know that I don't care about the scars. So, I do this to myself. And you know what? She can't stand the sight of me. She leaves. Now I see the funny side. Now I'm always smiling.</h1>
          </div>
        </section> -->
        <footer class="spring-footer home__content__footer">

        </footer>
      </div>
      <div class="rain">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1536" preserveAspectRatio="xMidYMax slice">
          <g fill-opacity=".15" transform="translate(155 742)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(235 562)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(375 254)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(533 172)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(758 699)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(55 642)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(235 562)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(275 154)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(433 72)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(658 599)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(255 600)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(435 262)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(675 354)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(333 372)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z"/>
            </g>
          </g>
          <g fill-opacity=".15" transform="translate(128 619)">
            <g class="rain-bottom-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(8 776)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(189 925)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(548 844)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(685 1115)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(858 909)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(874 1438)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(657 1256)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(443 1372)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(339 1107)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(24 1305)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(8 8)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(189 157)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(548 76)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(685 347)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(858 141)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <!-- -->
          <g fill-opacity=".35" transform="translate(874 670)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(657 488)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(443 604)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(339 339)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
          <g fill-opacity=".35" transform="translate(24 537)">
            <g class="rain-top-layer">
              <path style="fill:#84DBFF; transform: scale(.05);" d="M438.4,329.6C438.4,430.933,356.267,512,256,512S73.6,430.933,73.6,329.6S256,0,256,0
              	S438.4,229.333,438.4,329.6z" cx="138" cy="1110.5" rx="6" ry="5.5"/>
            </g>
          </g>
        </svg>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Spring",
  props: ["weatherData", "searchCommitted"],
  data() {
    return {
      menuOpen: false,
      weatherClass: "rainy",
      weatherClasses: [],
      monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      viewStatus: 1,
      weather: this.$props,
      // weatherDays: this.$props.weatherData.list[0]
    }
  },
  methods: {
    getWeatherClass: function(weatherId) {
      if (200 <= weatherId && weatherId < 600) {
    		return "rainy";
    	} else if (600 <= weatherId && weatherId < 800) {
    		return "snowy";
    	} else if (800 <= weatherId && weatherId < 802) {
    		return "sunny";
    	} else if (802 <= weatherId && weatherId < 804) {
    		return "partly-cloudy";
    	} else if (804 <= weatherId && weatherId < 900) {
    		return "cloudy";
    	} else {
    		return "clear";
    	}
    },
    viewToggle: function() {
      if(this.viewStatus === 5) {
        this.viewStatus = 1;
      } else if (this.viewStatus === 1) {
        this.viewStatus = 5;
      }
    },
    getWeatherMonth: function(dateText) {
      let date = new Date(dateText);
      return this.monthNames[date.getMonth()];
    },
    getWeatherDay: function(dateText) {
      let date = new Date(dateText);
      return date.getDate();
    },
    getFiveDay: function(sampleArr) {
      let arr = sampleArr;
      let arr2 = [];
      for (let i = 7; i < arr.length; i += 8) {
        arr2.push(arr[i]);
      }
      return arr2;
    }
  },
}
</script>

<style>

@import '~/assets/scss/variables.scss';
@import '~/assets/scss/palette.scss';
@import '~/assets/scss/keyframes.scss';
@import '~/assets/scss/fonts.scss';
@import '~/assets/scss/spring.scss';

</style>
