<template>
  <v-app id="inspire">
    <v-app-bar app clipped-left>
      <v-toolbar-title>Word Count</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <Form />
      <h1 class="mt-10 ml-4">После отправки перезагрузите страницу, тогда обновятся резульраты(скоро сделаю нормально... Спасибо за понимание)</h1>
      <h2 class="mt-10 ml-4">Табличка тасок</h2>
      <Tasks />
      <h2 class="mt-10 ml-4">Табличка результатов</h2>
      <Results />
    </v-content>

    <v-footer app>
      <span>&copy; 2020</span>
    </v-footer>
  </v-app>
</template>

<script>
import Results from "@/components/Results";
import Form from "@/components/Form";
import Tasks from "@/components/Tasks";

export default {
  name: "App",

  components: {
    Form,
    Results,
    Tasks
  },

  props: {
    source: String
  },

  created() {
    this.$vuetify.theme.dark = true;
  }
};
</script>
