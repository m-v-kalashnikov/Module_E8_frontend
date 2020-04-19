<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">URL сайта</th>
          <th class="text-left">Слово которое искали</th>
          <th class="text-left">Дата создания</th>
          <th class="text-left">HTTP статус код</th>
          <th class="text-left">Статус задачи</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in tasks" :key="item.address">
          <td>{{ item.address }}</td>
          <td>{{ item.word }}</td>
          <td>{{ item.timestamp }}</td>
          <td>{{ item.http_status }}</td>
          <td>{{ item.task_status }}</td>
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
    getTasks() {
      axios.get(`${BASE_API_URL}/`).then(response => {
        this.tasks = response.data;
      });
    }
  },
  data() {
    return {
      tasks: {}
    };
  },
  mounted() {
    this.getTasks();
  }
};
</script>
