<template>
  <div class="results">
    <h1>Страница со списком напитков и рейтингами</h1>

    <table class="results-list">
      <thead>
        <tr>
          <th>Название</th>
          <th>Описание</th>
          <th>Рейтинг</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="result in results" v-bind:key="result">
          <td>{{ result.name }}</td>
          <td>{{ result.description }}</td>
          <td>{{ result.rating }}/10</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.results-list {
  border: 1px solid black;
  margin-left: auto;
  margin-right: auto;
}
.results-list > td {
  text-align: center;
}
</style>

<script>
export default {
  name: "Results",
  data() {
    return {
      results: [
        {
          id: 1,
          name: "вода",
          description: "лучший способ утолить жажду",
          rating: 10
        },
        {
          id: 2,
          name: "компот",
          description: "сладковато",
          rating: 4
        }
      ]
    };
  }
};
</script>

<style scoped></style>
