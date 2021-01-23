<template>
  <select v-model="currentLocale" @change="localeChanged">
    <!--<option v-for="locale in availableLocales" :key="locale" :value="locale">{{ locale }}</option>-->
    <option v-for="locale in availableLocales" :key="locale" :value="locale">{{ $t("locale." + locale) }}</option>
  </select>
</template>

<script>
export default {
  name: "LocaleSwitcher",
  data: function () {
    return {
      currentLocale: this.$i18n.locale.toString(),
      availableLocales: this.$i18n.availableLocales
    }
  },
  methods: {
    localeChanged () {
      this.$router.push({
        path: this.$tp(this.$route.path, this.currentLocale, true)
      })
      this.$context.locale = this.currentLocale
      alert("言語は" + this.$context.locale + "です")
    }
  }
}
</script>