<template>
  <div>
    <div>
      <div>
        <h2
          class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
        >
          Overview
        </h2>
        <br />
        <p class="lg:text-lg text-sm text-justify leading-6">
          &nbsp;&nbsp;&nbsp;&nbsp; I am a front-end developer focused on
          <strong> VueJS , Nuxt , ReactJS , Next</strong>. Besides , I have
          experience building websites with
          <strong>
            Material UI , Antd , Tailwindcss , Bootstrap 5 , Style
            component</strong
          >.
        </p>
      </div>
      <br />
      <br />
      <br />
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        My technology
      </h2>
      <SkillBarContent />

      <!-- auto code block -->
    </div>
  </div>
</template>

<script>
  import TypeIt from 'typeit';
  // import Prism from 'prismjs';
  import 'animate.css';
  import { ref, computed, onMounted } from 'vue';
  import SkillBarContent from '../components/SkillBarContent.vue';
  import Skills from '../components/MainSkillsContent.json';

  export default {
    data() {
      return {
        skillsData: Skills,
        paddingValue: 0,
        loaded: false
      };
    },
    props: {
      responsiveValue: {
        type: Number,
        default: 0
      }
    },

    components: {
      SkillBarContent
    },
    methods: {
      fetch: function () {
        console.log(document.getElementById('render'));
      }
    },

    setup() {
      let contentRenderer = ref('');
      let textField = ref('');

      const clearCodeBlock = () => {
        contentRenderer.value.innerHTML = null;
      };

      const clearTerminalBlock = () => {
        textField.value.innerText = null;
      };

      const renderOutTextField = computed(() => {
        if (
          textField.value.innerText === null ||
          textField.value.innerText === undefined
        )
          return null;
        let content = textField.value.innerText;
        content = content.replaceAll('|', '');
        return content;
      });

      onMounted(() => {
        window.Prism = window.Prism || {};
        window.Prism.manual = true;
        setTimeout(() => {}, 5000);
      });

      return {
        contentRenderer,
        textField,
        clearCodeBlock,
        clearTerminalBlock,
        renderOutTextField
      };
    },

    watch: {
      windowWidth() {
        if (this.windowWidth > 1280) {
          this.paddingValue = Math.trunc(this.windowWidth - 1280) / 2;
        } else if (this.windowWidth < 1280) {
          this.paddingValue = 0;
        }
      }
    }
  };
</script>

<style>
  ::-webkit-scrollbar-track {
    background-color: transparent;
  }

  ::-webkit-scrollbar-thumb {
    background-color: var(--text-highlight-2);
    border-radius: 20px;
    border: 6px solid transparent;
    background-clip: content-box;
  }
  ::-webkit-scrollbar {
    width: 20px;
  }

  #render input {
    @apply w-20 rounded-lg border-2 border-pink-500;
  }

  .rendered-contents * {
    animation: fadeIn;
    animation-duration: 1s;
  }

  .rem-rendered-contents * {
    animation: fadeOut;
    animation-duration: 1s;
  }

  .highlight {
    color: var(--text-highlight);
    font-weight: bold;
  }

  .code-block-lines {
    color: var(--text);
    background-color: var(--text-highlight-2);
  }

  .code-block-terminal {
    margin-bottom: 0.5rem;
    margin-right: 0.5rem;
    border-radius: 50%;
    display: block;
  }

  #demo {
    white-space: nowrap;
    position: absolute;
    display: block;
  }

  #demo .html-tag {
    color: var(--text-highlight-2);
  }

  #demo .html-attribute {
    color: var(--text-highlight);
  }

  #demo .html-class {
    color: var(--text-highlight-2);
  }
</style>
