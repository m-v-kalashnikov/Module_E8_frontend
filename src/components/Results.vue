<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">URL сайта</th>
          <th class="text-left">Слово которое искали</th>
          <th class="text-left">Найдено слов</th>
          <th class="text-left">HTTP статус код</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in results" :key="item.address">
          <td>{{ item.address }}</td>
          <td>{{ item.word }}</td>
          <td>{{ item.words_count }}</td>
          <td>{{ item.http_status_code }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
import axios from "axios";

const BASE_API_URL = "http://0.0.0.0:5000";

export default {
  methods: {
    getResults() {
      axios.get(`${BASE_API_URL}/results`).then(response => {
        this.results = response.data;
      });
    }
  },
  data() {
    return {
      results: {}
    };
  },
  mounted() {
    this.getResults();
  }
};
</script>
