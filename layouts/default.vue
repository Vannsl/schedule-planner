<template>
  <v-app>
    <v-toolbar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-toolbar-title>
        <nuxt-link to="/" v-text="title" />
      </v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer
      :fixed="fixed"
      app
    >
      <v-spacer></v-spacer>
      <v-layout>
        <v-container v-html="$t('layout.copy')" />
        <v-container pl-2>
          <nuxt-link to="imprint">
            {{ $t('layout.imprint') }}
          </nuxt-link>
        </v-container>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      fixed: false,
      title: this.$t('layout.title')
    }
  }
}
</script>

<style scoped>
a {
  text-decoration: none;
}

a:link {
  color: black;
}

/* visited link */
a:visited {
  color: black;
}

/* mouse over link */
a:hover {
  color: hotpink;
}

/* selected link */
a:active {
  color: black;
}
</style>
