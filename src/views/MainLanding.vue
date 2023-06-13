<template>
  <div class="flex flex-col gap-[2.5rem]">
    <!-- introduction section -->
    <div class="divCenter">
      <p
        id="landing_intro"
        ref="landingIntro"
        class="lg:text-xl text-md acrlyic w-auto text-center selector"
      ></p>
    </div>
    <section class="">
      <h1 class="text-4xl font-bold">Ninh Hong Diep</h1>
      <h3 class="text-lg">Front-end developer</h3>
    </section>
    <section class="pt-2">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Professional background
      </h2>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6"></p>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        <!-- &nbsp;&nbsp;&nbsp;&nbsp; -->
      </p>
    </section>

    <!-- journey section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Journey
      </h2>
      <br />
      <div class="flex flex-col gap-2">
        <!-- year 2017 -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>2017:</strong>
          &nbsp; Start studying at VNU University of Engineering and Technology
        </p>
        <!-- year 2021 -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>2021:</strong>
          &nbsp; Graduated VNU University of Engineering and Technology
        </p>
        <!-- year 1/2021 -12/2021  -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>1/2021 - 12/2021:</strong>
          &nbsp; BunbuSoft (ReactJS Developer)
        </p>
        <p class="lg:text-lg text-sm text-justify">
          <strong>12/2021 - 7/2022:</strong>
          &nbsp; BunbuSoft (Onsite for Cowell Asia) (VueJS Developer)
        </p>
        <p class="lg:text-lg text-sm text-justify">
          <strong>7/2021 - now:</strong>
          &nbsp; Miichisoft (Front-end Developer)
        </p>
      </div>
    </section>
    <!-- education section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Education
      </h2>
      <br />
      <div class="flex flex-col gap-2">
        <!-- year 2017 - 2021 -->
        <p class="lg:text-lg text-sm text-justify">
          <strong> 2017 - 2021 :</strong>
          &nbsp; VNU University of Engineering and Technology ( Information and
          Technology)
        </p>
      </div>
    </section>
  </div>
</template>

<script>
  import TypeIt from 'typeit';
  import 'animate.css';
  import { ref } from 'vue';

  export default {
    data() {
      return {
        display: false
      };
    },
    setup() {
      const landingIntro = ref('');

      if (landingIntro.value !== '') {
        landingIntro.value === '';
      }
    },
    mounted() {
      new TypeIt('#landing_intro', {
        speed: 50,
        waitUntilVisible: true,
        startDelay: 2000,
        startDelete: true,
        // remove cursor when finished
        afterComplete: function (instance) {
          instance.destroy();
        }
      })
        .type('Hello! I am a Front-end developer.')
        .go();
    }
  };
</script>

<style>
  .selector {
    background-color: var(--bg-sel);
  }

  .copyright {
    animation: fadeInLeft;
    animation-duration: 1s;
    animation-delay: 3s;
  }

  /* @keyframes copyright {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
    visibility: visible;
  }
} */
</style>
