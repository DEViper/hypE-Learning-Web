<template>
  <div>
    <div>
      <v-form class="mt-10">
        <v-container fill-height fluid>
          <v-card class="mx-auto" max-width="700" tile>
            <h1 justify="center" align="center">Dodaj nowe pytanie</h1>
            <v-row justify="center" align="center">
              <v-col cols="12" md="10">
                <v-text-field v-model="title" label="Pytanie"></v-text-field>
              </v-col>
              <v-col cols="12" md="8">
                <v-text-field
                  cols="8"
                  md="8"
                  label="Odpowiedź nr 1"
                  v-model="a"
                ></v-text-field>
                <v-text-field
                  cols="8"
                  md="8"
                  v-model="b"
                  label="Odpowiedź nr 2"
                ></v-text-field>
                <v-text-field
                  cols="8"
                  md="8"
                  v-model="c"
                  label="Odpowiedź nr 3"
                ></v-text-field>
                <v-text-field
                  cols="8"
                  md="8"
                  v-model="d"
                  label="Odpowiedź nr 4"
                ></v-text-field>

                <h3>Zaznacz prawidłową odpowiedź</h3>
                <v-radio-group>
                  <v-radio label="a" @change="setCorrectAnswer('a')"></v-radio>
                  <v-radio label="b" @change="setCorrectAnswer('b')"></v-radio>
                  <v-radio label="c" @change="setCorrectAnswer('c')"></v-radio>
                  <v-radio label="d" @change="setCorrectAnswer('d')"></v-radio>
                </v-radio-group>
              </v-col>
            </v-row>
          </v-card>

          <v-col cols="12" md="7">
            <v-btn color="success" class="mr-4" @click="addQuestion"
              >Dodaj pytanie</v-btn
            >
          </v-col>
        </v-container>
      </v-form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { server } from "@/utils/helper";
export default {
  name: "AddQuestion",

  data: () => ({
    title: "",
    a: "",
    b: "",
    c: "",
    d: "",
    correctAnswer: "",
  }),

  methods: {
    addQuestion: function() {
      const userJson = localStorage.getItem("user");
      const user = JSON.parse(userJson);
      const token = user.token;
      axios.post(
        `${server.baseURL}/quizzes/${this.$route.params.quizId}/question`,
        {
          title: this.title,
          a: this.a,
          b: this.b,
          c: this.c,
          d: this.d,
          correctAnswer: this.correctAnswer,
        },
        {
          headers: {
            Authorization: ` Bearer ${token}`,
          },
        }
      );
    },

    setCorrectAnswer: function(answer) {
      this.correctAnswer = answer;
    },
  },
};
</script>
<style scoped></style>
