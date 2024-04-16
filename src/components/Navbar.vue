<template>
  <header class="header">
    <nav class="nav" v-if="nav">

      <div class="nav__left">
        <button @click="switchLang" class="nav__lang">
          {{ $i18n.locale }}</button>


        <label class="switch">
          <input type="checkbox">
          <span @click="switchTheme"></span>
        </label>


      </div>

      <h1 class="nav__title">{{ $t('notes') }}</h1>


      <button class="nav__search_btn" @click="nav = !nav">
        <svg width="27" height="27" viewBox="0 0 27 27" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd"
            d="M18.14 15.905L26.735 24.5L24.5 26.735L15.905 18.14C14.3 19.295 12.365 20 10.25 20C4.865 20 0.5 15.635 0.5 10.25C0.5 4.865 4.865 0.5 10.25 0.5C15.635 0.5 20 4.865 20 10.25C20 12.365 19.295 14.3 18.14 15.905ZM10.25 3.5C6.515 3.5 3.5 6.515 3.5 10.25C3.5 13.985 6.515 17 10.25 17C13.985 17 17 13.985 17 10.25C17 6.515 13.985 3.5 10.25 3.5Z"
            fill="#49454F" />
        </svg>

      </button>
    </nav>


    <nav class="nav__search" v-else>
      <button class="nav__search_back" @click="nav = true, search = ''">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M24 10.5H5.745L14.13 2.115L12 0L0 12L12 24L14.115 21.885L5.745 13.5H24V10.5Z" fill="#1C1B1F" />
        </svg>

      </button>

      <input v-model="search" type="text" class="nav__search_input" autofocus :placeholder="$t('searchInput')">

      <button class="nav__search_clear" @click="search = ''">
        <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd"
            d="M15 0C6.705 0 0 6.705 0 15C0 23.295 6.705 30 15 30C23.295 30 30 23.295 30 15C30 6.705 23.295 0 15 0ZM15 27C8.385 27 3 21.615 3 15C3 8.385 8.385 3 15 3C21.615 3 27 8.385 27 15C27 21.615 21.615 27 15 27ZM15 12.885L20.385 7.5L22.5 9.615L17.115 15L22.5 20.385L20.385 22.5L15 17.115L9.615 22.5L7.5 20.385L12.885 15L7.5 9.615L9.615 7.5L15 12.885Z"
            fill="#49454F" />
        </svg>

      </button>
    </nav>

  </header>
</template>


<script>
export default {
  data() {
    return {
      nav: true,
      search: '',
    }
  },
  methods: {
    switchLang() {
      this.$i18n.locale == 'ru' ? this.$i18n.locale = 'eng' : this.$i18n.locale = 'ru'
      localStorage.lang = this.$i18n.locale
    },
    switchTheme() {
      console.log(1);
      let value = document.body.style.getPropertyValue('--white')

      if (value == '#fff') {
        // rgb(37, 37, 37)
        document.body.style.setProperty('--white', '#0f0f0f')
        document.body.style.setProperty('--shadow', '0px 4px 4px rgba(255, 255, 255, 0.25), 0px 1px 3px rgba(255, 255, 255, 0.3)')
        document.body.style.setProperty('--mainColor', 'rgb(37, 37, 37)')
        document.body.style.setProperty('--text', '#fff')
      } else {
        document.body.style.setProperty('--white', '#fff')
        document.body.style.setProperty('--shadow', '0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3)')
        document.body.style.setProperty('--mainColor', '#F3EDF7')
        document.body.style.setProperty('--text', '#1C1B1F')

      }
    }
  },
  watch: {
    search(newValue) {
      this.$emit('setSearch', newValue)
    }
  },
  created() {
    document.body.style.setProperty('--white', '#fff')
  }
};
</script>
