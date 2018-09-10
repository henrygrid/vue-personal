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
    <section class="slide slide-1 main current-slide">
      <div class="slide-1__content">
        <h1 class="slide-1__content__heading">Your year-round source for a great web presence.</h1>
      </div>
    </section>
    <section class="slide slide-2 about hidden-slide">
      <div>2</div>
    </section>
    <section class="slide slide-3 projects hidden-slide">
      <div>3</div>
    </section>
    <section class="slide slide-4 last-slide contact hidden-slide">
      <div>4</div>
    </section>
    <span class="button-row">
      <button @click="prevSlide" class="slide-trigger prev">-</button>
      <button @click="selectSlide" class="buttons slide-trigger button-filled first-button" id="button-1"></button>
      <button @click="selectSlide" class="buttons slide-trigger" id="button-2"></button>
      <button @click="selectSlide" class="buttons slide-trigger" id="button-3"></button>
      <button @click="selectSlide" class="buttons slide-trigger last-button" id="button-4"></button>
      <button @click="nextSlide" class="next slide-trigger">+</button>
    </span>
  </div>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'
import $ from 'jquery'

export default {
  components: {
    AppLogo
  },
  methods: {
    triggerSlide: function(e, slideLoop, direction) {
      e.preventDefault();
      let currentButton = e.target;
      let button = $(".slide-trigger");
      let slideNumber;

      $(".buttons").removeClass("button-filled");

      $(".buttons").each(function(i) {
        if(e.target === this) {
          slideNumber = i + 1;
          $(this).addClass("button-filled");
        }
      });

      if ($(".slide")[slideNumber - 1] === $(".current-slide")[0]) {
        return;
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
            console.log(nextSlide);
            console.log(this);

            $(this).one("animationend", function(e) {
              $(this).removeClass("current-slide");
              $(this).removeClass("slide-out");
              $(this).addClass("hidden-slide");
              $(nextSlide).removeClass("next-slide");
              $(nextSlide).addClass("current-slide");
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

/* Palette

  Whitish: #F4F8F6;
  Teal: #7F85A0;
  Orange: #FCBE2D;
  Redish: #B33C52;
  Dark Blue: #024;

*/

.container {
  min-height: 100vh;
  /* display: flex;
  justify-content: center;
  align-items: center;
  text-align: center; */
  position: relative;
  overflow-x: hidden;
}

.slide {
  width: 100%;
  height: 100vh;
  display: block;
  position: absolute;
}

.slide div {
  color: #F4F8F6;
}

.slide-3 div {
  color: #000;
}

.slide-1 {
  background-color: #024;  /*dark blue*/
}

.slide-2 {
  background-color: #FCBE2D; /*orange*/
}

.slide-3 {
  background-color: #F4F8F6; /* whitish */
}

.slide-4 {
  background-color: #7F85A0; /*teal*/
}

.slide-out {
  animation: slow-slide-out 1.5s;
}

.current-slide {
  z-index: 10;
}

.hidden-slide {
  z-index: 5;
  transform: translateX(0);
}

.next-slide {
  z-index: 8;
}

.prev-slide {
  z-index: 7;
}

@keyframes slow-slide-out {
  0% {
    transform: translateX(0);
  }

  50% {
    transform: scale(.8);
  }

  100% {
    transform: translateX(-100%) scale(.8);
  }
}

@keyframes slow-slide-in {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(-100%);
  }
}

.button-row {
  display: block;
  position: absolute;
  bottom: 0;
  text-align: center;
  width: 100%;
  z-index: 100;
}

.buttons {
  border: 1px solid white;
  width: 10px;
  height: 16px;
  margin: 0 6px;
  background-color: transparent;
  border-radius: 50%;
}

.buttons:active,
.buttons:focus {
  outline: none;
}

.button-filled {
  background-color: #fff;
}

.slide-trigger {
  cursor: pointer;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
