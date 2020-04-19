<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            v-model="url"
            :counter="300"
            :rules="urlRules"
            label="URL сайта"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-text-field
            v-model="word"
            :counter="50"
            :rules="wordRules"
            label="Слово которое нужно найти"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row>
        <v-col cols="12" md="4">
          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="postWordCounter"
          >
            Отправить на подсчет
          </v-btn>
        </v-col>
        <v-col cols="12" md="4">
          <v-btn color="info" class="mr-4" @click="reset">
            Очистить форму
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
import axios from "axios";

const BASE_API_URL = "http://0.0.0.0:5000";

function is_url(str) {
  let regexp = /^(?:(?:https?|ftp):\/\/)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)(?:\.(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)*(?:\.(?:[a-z\u00a1-\uffff]{2,})))(?::\d{2,5})?(?:\/\S*)?$/;
  return regexp.test(str);
}
function allLetter(str) {
  let regexp = /^[a-zA-Z0-9А-Яа-я]+$/;
  return regexp.test(str);
}

export default {
  data: () => ({
    valid: true,
    word: "",
    wordRules: [
      v => !!v || "Слово нужено обязательно",
      v =>
        (v && allLetter(v) === true) ||
        "Должно быть одно слово состоящее из латиницы, кирилици или цыфры",
      v => (v && v.length <= 50) || "Слово не должно быть длиннее 50 символов"
    ],
    url: "",
    urlRules: [
      v => !!v || "URL нужен обязательно",
      v => (v && is_url(v) === true) || "Не сильно похоже на URL",
      v => (v && v.length <= 300) || "URL не долженбыть длиннее 300 знаков"
    ]
  }),

  methods: {
    getTasks() {
      axios.get(`${BASE_API_URL}/`).then(response => {
        this.tasks = response.data;
      });
    },
    postWordCounter() {
      if (this.url === "" || this.word === "") {
        alert("Поля должныбыть заполнены!");
      } else {
        const requestData = {
          url: this.url,
          word: this.word
        };
        axios
          .post(`${BASE_API_URL}/`, requestData)
          .then(() => {
            axios.get(`${BASE_API_URL}/`).then(response => {
              this.tasks.push(response.data);
            });
            Location.reload();
          })
          .catch(error => {
            console.log(error);
          });
      }
    },
    reset() {
      this.$refs.form.reset();
    }
  }
};
</script>

<style scoped></style>
