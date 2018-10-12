<template>
  <div class="container">
    <!-- <div>
      <app-logo/>
      <h1 class="title">
        vue-personal
      </h1>
      <h2 class="subtitle">
        Portfolio Site
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green">Documentation</a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey">GitHub</a>
      </div>
    </div> -->
    <Winter :weatherData=weatherData></Winter>
    <Spring :weatherData=weatherData></Spring>
    <Summer :weatherData=weatherData></Summer>
    <Fall :weatherData=weatherData></Fall>
    <div class="search__box">
      <input type="search" class="search__input" v-on:keyup.enter="getWeather" placeholder="Enter City"/>
      <span class="search__icon" @click="getWeather"></span>
    </div>
    <div class="menu__button">
      <div class="snowflake menu-cover"></div>
      <div class="ham-container" @click="toggleMenu">
        <span class="ham ham-top"></span>
        <span class="ham ham-middle"></span>
        <span class="ham ham-bottom"></span>
      </div>
    </div>
    <!-- <span class="button-row">
      <button @click="prevSlide" class="slide-trigger prev">-</button>
      <div class="button-wrapper" @click="selectSlide">
        <span class="button-title">Winter</span>
        <button class="buttons slide-trigger button-filled first-button" id="button-1"></button>
      </div>
      <div class="button-wrapper" @click="selectSlide">
        <span class="button-title">Spring</span>
        <button class="buttons slide-trigger" id="button-2"></button>
      </div>
      <div class="button-wrapper" @click="selectSlide">
        <span class="button-title">Summer</span>
        <button class="buttons slide-trigger" id="button-3"></button>
      </div>
      <div class="button-wrapper" @click="selectSlide">
        <span class="button-title">Fall</span>
        <button class="buttons slide-trigger last-button" id="button-4"></button>
      </div>
      <button @click="nextSlide" class="next slide-trigger">+</button>
    </span> -->
    <!-- <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div> -->
    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/smashicons" title="Smashicons">Smashicons</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>  -->
    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/smashicons" title="Smashicons">Smashicons</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>  -->
    <!-- <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>  -->
    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/vectors-market" title="Vectors Market">Vectors Market</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>  -->
    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/smashicons" title="Smashicons">Smashicons</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div> -->
    <!-- -->
  </div>
</template>

<script>
import Winter from '~/components/Winter.vue'
import Spring from '~/components/Spring.vue'
import Summer from '~/components/Summer.vue'
import Fall from '~/components/Fall.vue'
import $ from 'jquery'

export default {
  components: {
    Winter,
    Spring,
    Summer,
    Fall
  },
  data() {
    return {
      menuOpen: false,
      currentWeather: "snowy",
      monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      weatherData: {},
      weatherOne: {},
      weatherFive: []
    }
  },
  mounted() {
    let city = "detroit";
    let vm = this;
    $.getJSON('http://api.openweathermap.org/data/2.5/forecast?q=' + city + ',us&units=imperial&APPID=f3ca74b01a93f4ec83050fe63dd88908', (data) => {
      vm.weatherData = data;
      console.log(vm.weatherData);
    });
  },
  methods: {
    toTitleCase: function(str) {
      return str.replace(/\w\S*/g, function(txt) {
    	    return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();
    	});
    },
    getSearchLocation: function() {
      let city = $('.search__input').val();
    	city = this.toTitleCase(city).replace(/\s+/g, '+');
    	return city;
    },
    getWeather: function() {
      let city = this.getSearchLocation();
      let vm = this;
      let weatherData;
      console.log(city);
      $.getJSON('http://api.openweathermap.org/data/2.5/forecast?q=' + city + ',us&units=imperial&APPID=f3ca74b01a93f4ec83050fe63dd88908', (data) => {
        vm.weatherData = data;
        console.log(vm.weatherData);
      });
    },
    toggleMenu: function(e) {
      if (!this.menuOpen) {
        $(".ham-top").css("animation", "ham-top-to-cross 1s forwards");
        $(".ham-middle").css("animation", "ham-middle-to-cross 1s forwards");
        $(".ham-bottom").hide(1000);
        $(".button-row").css("transform", "translateX(-10px)");
        this.menuOpen = true;
      } else {
        $(".ham-top").css("animation", "ham-top-to-burger 1s forwards");
        $(".ham-middle").css("animation", "ham-middle-to-burger 1s forwards");
        $(".ham-bottom").show(1000);
        $(".button-row").css("transform", "translateX(120px)");
        this.menuOpen = false;
      }
    },
    triggerSlide: function(e, slideLoop, direction) {
      e.preventDefault();
      let button = $(".slide-trigger");
      let slideNumber;
      let currentButton = $(e.target).find("button")[0];
      let primaryColor;
      let secondaryColor;
      let menuIcons = [
        {
          title: 'snowflake',
          backgroundColor: '#024',
          menuColor: '#fff'
        },
        {
          title: 'cloud',
          backgroundColor: '#42d2d2',
          menuColor: '#fff'
        },
        {
          title: 'sun',
          backgroundColor: '#69d2e7',
          menuColor: '#EFC334'
        },
        {
          title: 'leaf-menu',
          backgroundColor: '#599ed9',
          menuColor: '#93DA62'
        }
      ];
      let currentMenu;

      $(menuIcons).each(function() {
        if($(".menu-cover").hasClass(this.title)) {
          currentMenu = this.title;
        }
      });

      $(".buttons").removeClass("button-filled");

      $(".buttons").each(function(i) {
        if(currentButton === this) {
          slideNumber = i + 1;
          $(this).addClass("button-filled");
        }
      });

      if ($(".slide")[slideNumber - 1] === $(".current-slide")[0]) {
        return;
      }

      let slideType;

      switch (slideNumber) {
        case 1:
          slideType = "snowflake";
          primaryColor = '#fff';
          secondaryColor = '#fff';
          break;
        case 2:
          slideType = "cloud";
          primaryColor = "#42d2d2";
          secondaryColor = '#fff';
          break;
        case 3:
          slideType = "sun";
          primaryColor = "#69d2e7";
          secondaryColor = '#fff';
          break;
        case 4:
          slideType = "leaf-menu";
          primaryColor = "#599ed9";
          secondaryColor = '#fff';
          break;
      }

      $(".slide").each(function(i) {

        let nextSlide;

        let buttonNumber;

        console.log(direction);

        switch (direction) {
            case "next":
              nextSlide = $(this).next()[0];
              buttonNumber = i + 2;
              break;
            case "prev":
              nextSlide = $(this).prev()[0];
              buttonNumber = i;
              break;
            case "number":
              nextSlide = $(".slide-" + slideNumber);
              break;
        }

        if($(this).hasClass("current-slide")) {

          if(!$(nextSlide).hasClass("slide")) {
            $(slideLoop).removeClass("hidden-slide");
            $(slideLoop).addClass("next-slide");
            $(this).addClass("slide-out");
            $(button).prop("disabled", true);

            switch(slideLoop) {
              case ".slide-1":
                $(".first-button").addClass("button-filled");
                break;
              case ".last-slide":
                $(".last-button").addClass("button-filled");
                break;
            }

            $(this).one("animationend", function(e) {
              $(this).removeClass("current-slide");
              $(this).removeClass("slide-out");
              $(this).addClass("hidden-slide");
              $(slideLoop).removeClass("next-slide");
              $(slideLoop).addClass("current-slide");
              $(button).prop("disabled", false);
            });
          } else {
            $(nextSlide).removeClass("hidden-slide");
            $(nextSlide).addClass("next-slide");
            $(this).addClass("slide-out");
            $(button).prop("disabled", true);
            $("#button-" + buttonNumber).addClass("button-filled");
            $(".menu__button").removeClass("show__menu-button");
            $(".menu__button").addClass("hide__menu-button");

            $(this).one("animationend", function(e) {
              $(this).removeClass("current-slide");
              $(this).removeClass("slide-out");
              $(this).addClass("hidden-slide");
              $(nextSlide).removeClass("next-slide");
              $(nextSlide).addClass("current-slide");
              $(".menu-cover").removeClass(currentMenu);
              $(".menu-cover").addClass(slideType);
              $(".ham").css("background-color", primaryColor);
              $(".button-title").css("color", secondaryColor);
              $(".buttons, .button-filled").css("background-color", secondaryColor);
              $(".menu__button").removeClass("hide__menu-button");
              $(".menu__button").addClass("show__menu-button");
              $(button).prop("disabled", false);
            });
          }
        }
      });

    },
    nextSlide: function(e) {
      this.triggerSlide(e, ".slide-1", "next");
    },
    prevSlide: function(e) {
      this.triggerSlide(e, ".last-slide", "prev");
    },
    selectSlide: function(e) {
      this.triggerSlide(e, null, "number");
    }
  }
}
</script>

<style>
@import '~/assets/scss/variables.scss';
@import '~/assets/scss/palette.scss';
@import '~/assets/scss/keyframes.scss';
@import '~/assets/scss/slider.scss';


</style>
