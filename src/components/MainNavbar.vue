<template>
  <section class="pt-2 navbar fixed w-full">
    <div class="2xl:flex flex-row py-3 px-3 hidden justify-between mx-40">
      <!-- pc view port -->

      <div>
        <h1 class="text-2xl font-bold headers">
          <router-link
            to="/"
            @click="scrollTop"
            class="no-underline cursor-pointer"
            >Diep Ninh</router-link
          >
        </h1>
      </div>
      <div class="text-xl inline-block px-10 pt-[0.4rem]">
        <ul class="flex flex-row">
          <li
            class="px-4 flex flex-row"
            v-for="(value, index) in webRoutes"
            :key="index"
          >
            <button>
              <router-link :to="value.route" @click="scrollTop">{{
                value.title
              }}</router-link>
            </button>
          </li>
        </ul>
      </div>
      <!-- spacing -->
    </div>

    <!-------------------------------------------------------------------------------------->

    <!-- mobile viewport -->
    <div
      class="2xl:hidden flex flex-row py-3 items-center justify-between mx-10"
    >
      <div>
        <h1 class="text-3xl font-bold sm:-ml-[0px]">
          <router-link to="/" @click="scrollTop" class="scroll-smooth">
            Diep Ninh
          </router-link>
        </h1>
      </div>

      <div class="rightSide flex flex-row gap-4">
        <!-- drop down section  -->
        <div class="has-dpdn">
          <NavbarIcons
            :selected-icon="'burgerMenu'"
            @click="showDropdownNavigation"
          />
          <MobileNavbarComponent
            :is-showing-navbar-overlay="mobileDropdownNavigation"
            :navbar-items="webRoutes"
            @close-overlay="hideDropdownNavigation"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  import NavbarIcons from './MainNavbarComponents/NavbarIcons.vue';
  import MobileNavbarComponent from './MainNavbarComponents/NavbarMobileComponent.vue';
  import { computed, ref } from 'vue';

  export default {
    components: {
      NavbarIcons,
      MobileNavbarComponent
    },

    data() {
      return {
        windowWidth: window.innerWidth
      };
    },

    setup(props) {
      const webRoutes = {
        skills: {
          title: 'Skills',
          route: '/skills'
        },
        works: {
          title: 'Works',
          route: '/work'
        },
        contact: {
          title: 'Contact',
          route: '/contact'
        }
      };

      const mobileDropdownNavigation = ref(false);

      const showDropdownNavigation = () => {
        mobileDropdownNavigation.value = true;
      };

      const hideDropdownNavigation = () => {
        mobileDropdownNavigation.value = false;
      };

      const scrollTop = () => {
        document.body.scrollTop = 0;
        document.documentElement.scrollTop = 0;
      };

      return {
        webRoutes,
        mobileDropdownNavigation,
        showDropdownNavigation,
        hideDropdownNavigation,
        scrollTop
      };
    },

    emits: ['updateWindowSize'],
    mounted() {
      this.onResize();

      this.$nextTick(() => {
        window.addEventListener('resize', this.onResize);
      });
    },

    beforeDestroy() {
      window.removeEventListener('resize', this.onResize);
    },

    methods: {
      onResize() {
        this.windowWidth = window.innerWidth;
        this.$emit('updateWindowSize', this.windowWidth);
      }
    }
  };
</script>

<style>
  .navbar {
    /* background-color: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0)); */
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    z-index: 50;
    left: 50%;
    transform: translateX(-50%);
    transition: color 500ms ease-in-out;
    /* box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.1); */
  }

  .navbar > * {
    transition: color 500ms ease-in-out;
  }
  /* || drop down on focus  */
  /* ======================================================================= */
  .dpdn {
    /* positions  */
    position: absolute;
    opacity: 0;
    z-index: 40;
    visibility: hidden;

    /* typology */
    background-color: var(--bg-sel);
    color: var(--text);

    transition: opacity 0.15s ease-out;

    backdrop-filter: blur(50px);
    -webkit-backdrop-filter: blur(50px);
  }

  .has-dpdn:focus-within .dpdn {
    opacity: 1;
    pointer-events: auto;
    visibility: visible;
  }

  /* || drop down text underline animation */
  /* ======================================================================= */
  .dpdn_item {
    color: var(--text);
    display: inline-block;
    position: relative;
    font-size: 1rem;
  }

  .dpdn_item:after {
    content: '';
    position: absolute;
    width: 100%;
    transform: scaleX(0);
    height: 2px;
    bottom: 0;
    left: 0;
    background-color: var(--text);
    transform-origin: bottom right;
    transition: transform 0.25s ease-out;
  }

  .dpdn_item:hover:after {
    transform: scaleX(1);
    transform-origin: bottom left;
  }
  /* ======================================================================= */

  .navbar_burger {
    background-color: var(--text);
  }
  /* || SVG icons  */
  /* ======================================================================= */
  .svg_border {
    border-color: var(--text);
  }

  .svgColor {
    filter: var(--svg-color);
  }
  /* ======================================================================= */

  html {
    scroll-behavior: smooth;
  }

  .router-link-exact-active {
    /* color: white; */
    font-weight: bold;
    text-decoration: underline;
    cursor: default;
    color: var(--text-highlight);
    text-underline-offset: 4.1px;
    text-decoration-thickness: auto;
  }

  .route-hover :hover {
    color: var(--text-highlight-2);
    transition: color 500ms ease-in-out;
  }
</style>

<style scoped>
  .headers {
    transition: color 500ms ease-in-out;
  }
</style>
