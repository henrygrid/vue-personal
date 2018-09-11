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
    <Home></Home>
    <Projects></Projects>
    <Blog></Blog>
    <Contact></Contact>
    <span class="button-row">
      <button @click="prevSlide" class="slide-trigger prev">-</button>
      <button @click="selectSlide" class="buttons slide-trigger button-filled first-button" id="button-1"></button>
      <button @click="selectSlide" class="buttons slide-trigger" id="button-2"></button>
      <button @click="selectSlide" class="buttons slide-trigger" id="button-3"></button>
      <button @click="selectSlide" class="buttons slide-trigger last-button" id="button-4"></button>
      <button @click="nextSlide" class="next slide-trigger">+</button>
    </span>
    <!-- <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div> -->
  </div>
</template>

<script>
import Home from '~/components/Home.vue'
import Projects from '~/components/Projects.vue'
import Blog from '~/components/Blog.vue'
import Contact from '~/components/Contact.vue'
import $ from 'jquery'

export default {
  components: {
    Home,
    Projects,
    Blog,
    Contact
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
@import '~/assets/scss/variables.scss';
@import '~/assets/scss/palette.scss';
@import '~/assets/scss/keyframes.scss';
@import '~/assets/scss/slider.scss';


</style>
