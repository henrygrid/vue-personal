<template>
  <section class="slide slide-1 home winter current-slide">
    <div class="home--wrapper">
      <div class="home__content">
        <section class="home__content__header">
          <div v-if="$props.searchCommitted === true" class="winter__day__wrapper">
            <div class="winter__day__toggle__container">
              <span class="winter__day__one__title">1 Day</span>
              <label class="winter__switch" for="checkbox">
                <input type="checkbox" id="winter-checkbox" @click="viewToggle" />
                <div class="winter__slider round"></div>
              </label>
              <span class="winter__day__five__title">5 Day</span>
            </div>
            <h1 class="winter__city">{{ weather.weatherData.city.name }}</h1>
            <ul v-if="viewStatus === 1" :class=" [ viewStatus < 3 ? 'one-day-list': 'five-day-list'] + ' winter__day__list'">
              <li class="winter__day__list__item">
                <h1 class="winter__day__date">{{ getWeatherMonth($props.weatherData.list[0].dt_txt) }} {{ getWeatherDay($props.weatherData.list[0].dt_txt) }}</h1>
                <div v-bind:class="weatherClass + ' winter__day__image'"></div>
                <p class="winter__day__temp--high">{{ Math.floor($props.weatherData.list[0].main.temp) }} &#8457;</p>
                <p class="winter__day__temp--low">{{ Math.floor($props.weatherData.list[0].wind.speed) }} mph</p>
              </li>
            </ul>
            <ul v-else-if="viewStatus === 5" :class=" [ viewStatus < 3 ? 'one-day-list': 'five-day-list'] + ' winter__day__list'">
              <li v-for="(day, index) in getFiveDay($props.weatherData.list)" v-bind:key="`day-${index}`"  class="winter__day__list__item">
                <div>
                  <h1 class="winter__day__date">{{ getWeatherMonth(day.dt_txt) }} {{ getWeatherDay(day.dt_txt) }}</h1>
                  <div v-bind:class="getWeatherClass(day.weather[0].id) + ' winter__day__image'"></div>
                  <p class="winter__day__temp--high">{{ Math.floor(day.main.temp) }} &#8457;</p>
                  <p class="winter__day__temp--low">{{ Math.floor(day.wind.speed) }} mph</p>
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
            <h1 class="home__content__intro__heading">Nice to meet you</h1>
            <p class="home__content__intro__text">I'm a developer, communicator and all around problem solver living in the Metro Detroit area. Let's start a conversation about how I can help you today.</p>
          </div> -->
        <!-- </section> -->
        <footer class="winter-footer home__content__footer">
          <div class="snowman"></div>
        </footer>
      </div>
      <div class="snow">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1536" preserveAspectRatio="xMidYMax slice">
          <g fill="#FFF" fill-opacity=".15" transform="translate(55 42)">
           <g id="snow-bottom-layer">
            <ellipse cx="6" cy="1009.5" rx="6" ry="5.5"/>
            <ellipse cx="138" cy="1110.5" rx="6" ry="5.5"/>
            <ellipse cx="398" cy="1055.5" rx="6" ry="5.5"/>
            <ellipse cx="719" cy="1284.5" rx="6" ry="5.5"/>
            <ellipse cx="760" cy="1155.5" rx="6" ry="5.5"/>
            <ellipse cx="635" cy="1459.5" rx="6" ry="5.5"/>
            <ellipse cx="478" cy="1335.5" rx="6" ry="5.5"/>
            <ellipse cx="322" cy="1414.5" rx="6" ry="5.5"/>
            <ellipse cx="247" cy="1234.5" rx="6" ry="5.5"/>
            <ellipse cx="154" cy="1425.5" rx="6" ry="5.5"/>
            <ellipse cx="731" cy="773.5" rx="6" ry="5.5"/>
            <ellipse cx="599" cy="874.5" rx="6" ry="5.5"/>
            <ellipse cx="339" cy="819.5" rx="6" ry="5.5"/>
            <ellipse cx="239" cy="1004.5" rx="6" ry="5.5"/>
            <ellipse cx="113" cy="863.5" rx="6" ry="5.5"/>
            <ellipse cx="102" cy="1223.5" rx="6" ry="5.5"/>
            <ellipse cx="395" cy="1155.5" rx="6" ry="5.5"/>
            <ellipse cx="826" cy="943.5" rx="6" ry="5.5"/>
            <ellipse cx="626" cy="1054.5" rx="6" ry="5.5"/>
            <ellipse cx="887" cy="1366.5" rx="6" ry="5.5"/>
            <ellipse cx="6" cy="241.5" rx="6" ry="5.5"/>
            <ellipse cx="138" cy="342.5" rx="6" ry="5.5"/>
            <ellipse cx="398" cy="287.5" rx="6" ry="5.5"/>
            <ellipse cx="719" cy="516.5" rx="6" ry="5.5"/>
            <ellipse cx="760" cy="387.5" rx="6" ry="5.5"/>
            <ellipse cx="635" cy="691.5" rx="6" ry="5.5"/>
            <ellipse cx="478" cy="567.5" rx="6" ry="5.5"/>
            <ellipse cx="322" cy="646.5" rx="6" ry="5.5"/>
            <ellipse cx="247" cy="466.5" rx="6" ry="5.5"/>
            <ellipse cx="154" cy="657.5" rx="6" ry="5.5"/>
            <ellipse cx="731" cy="5.5" rx="6" ry="5.5"/>
            <ellipse cx="599" cy="106.5" rx="6" ry="5.5"/>
            <ellipse cx="339" cy="51.5" rx="6" ry="5.5"/>
            <ellipse cx="239" cy="236.5" rx="6" ry="5.5"/>
            <ellipse cx="113" cy="95.5" rx="6" ry="5.5"/>
            <ellipse cx="102" cy="455.5" rx="6" ry="5.5"/>
            <ellipse cx="395" cy="387.5" rx="6" ry="5.5"/>
            <ellipse cx="826" cy="175.5" rx="6" ry="5.5"/>
            <ellipse cx="626" cy="286.5" rx="6" ry="5.5"/>
            <ellipse cx="887" cy="598.5" rx="6" ry="5.5"/>
           </g>
          </g>
          <g fill="#FFF" fill-opacity=".3" transform="translate(65 63)">
           <g id="snow-top-layer">
            <circle cx="8" cy="776" r="8"/>
            <circle cx="189" cy="925" r="8"/>
            <circle cx="548" cy="844" r="8"/>
            <circle cx="685" cy="1115" r="8"/>
            <circle cx="858" cy="909" r="8"/>
            <circle cx="874" cy="1438" r="8" transform="rotate(180 874 1438)"/>
            <circle cx="657" cy="1256" r="8" transform="rotate(180 657 1256)"/>
            <circle cx="443" cy="1372" r="8" transform="rotate(180 443 1372)"/>
            <circle cx="339" cy="1107" r="8" transform="rotate(180 339 1107)"/>
            <circle cx="24" cy="1305" r="8" transform="rotate(180 24 1305)"/>
            <circle cx="8" cy="8" r="8"/>
            <circle cx="189" cy="157" r="8"/>
            <circle cx="548" cy="76" r="8"/>
            <circle cx="685" cy="347" r="8"/>
            <circle cx="858" cy="141" r="8"/>
            <circle cx="874" cy="670" r="8" transform="rotate(180 874 670)"/>
            <circle cx="657" cy="488" r="8" transform="rotate(180 657 488)"/>
            <circle cx="443" cy="604" r="8" transform="rotate(180 443 604)"/>
            <circle cx="339" cy="339" r="8" transform="rotate(180 339 339)"/>
            <circle cx="24" cy="537" r="8" transform="rotate(180 24 537)"/>
           </g>
          </g>
        </svg>
      </div>
    </div>
  </section>
</template>

<script>
import $ from 'jquery';

export default {
  name: "Winter",
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
@import '~/assets/scss/winter.scss';

</style>
