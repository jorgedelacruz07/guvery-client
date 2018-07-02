<template>
  <section>
    <!--Toolbars  -->
    <v-toolbar dark color="primary">
      <v-toolbar-title class="white--text">Guvery</v-toolbar-title>
    </v-toolbar>
  </section>
</template>

<script>
export default {
  data () {
    return {
      drawer: null,
      items: [
        { title: 'Home', icon: 'dashboard' },
        { title: 'About', icon: 'question_answer' }
      ]
    }
  }
}
</script>

<style lang="css">
</style>
