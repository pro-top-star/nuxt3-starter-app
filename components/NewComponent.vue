<template>
    <h1 class="mt-64 font-18 text-center">
        Welcome to my page!
    </h1>    
</template>
  
  <script lang="ts" setup>
  import { useI18n } from 'vue-i18n'
  
  import { useCounter } from '@/store/counter'
  import { isDark, toggleDark } from '@/composables/dark'
  
  const { t, locale, availableLocales } = useI18n()
  const counterStore = useCounter()
  
  // fetch data from server/api
  const { data } = await useAsyncData('/api/hello', () => {
    return $fetch('/api/hello', {
      params: {
        name: 'world'
      }
    })
  })
  
  const toggleLocales = () => {
    // change to some real logic
    const locales = availableLocales
    console.log(locale.value)
    locale.value = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  }
  
  const gotoGitHub = () => {
    window.open('https://github.com/xiaoluoboding/nuxt3-starter')
  }
  </script>
  
  <style scoped>
  .gradient-border {
    position: relative;
    border-radius: 0.5rem;
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
    width: 100%;
  }
  @media (prefers-color-scheme: light) {
    .gradient-border {
      background-color: rgba(255, 255, 255, 0.3);
    }
    .gradient-border::before {
      background: linear-gradient(
        90deg,
        #e2e2e2 0%,
        #e2e2e2 25%,
        #00dc82 50%,
        #36e4da 75%,
        #0047e1 100%
      );
    }
  }
  @media (prefers-color-scheme: dark) {
    .gradient-border {
      background-color: rgba(20, 20, 20, 0.3);
    }
    .gradient-border::before {
      background: linear-gradient(
        90deg,
        #303030 0%,
        #303030 25%,
        #00dc82 50%,
        #36e4da 75%,
        #0047e1 100%
      );
    }
  }
  .gradient-border::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border-radius: 0.5rem;
    padding: 2px;
    width: 100%;
    background-size: 400% auto;
    background-position: 0 0;
    opacity: 0.5;
    transition: background-position 0.3s ease-in-out, opacity 0.2s ease-in-out;
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor;
    mask-composite: exclude;
    z-index: -1;
  }
  .gradient-border:hover::before {
    background-position: -50% 0;
    opacity: 1;
  }
  </style>
  