<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          src="https://www.hermes.com/sites/all/themes/custom/hermes/img/hermes-logo.svg"
          class="my-3"
          contain
          height="100"
        />
      </v-col>

      <v-col class="mb-4" cols="12">
        <h1 class="display-2 font-weight-bold mb-3">
          エルメス100万円ガチャ
        </h1>
      </v-col>

      <v-col class="mb-4" cols="12">
        <v-btn 
          class="ma-4"
          color="primary"
          dark
          width="140"
          @click="getCalculate()"
        >
          回す
        </v-btn>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
        v-if="loading"
      >
        <v-progress-circular indeterminate></v-progress-circular>
      </v-col>

      <v-col
        class="mb-1"
        cols="12"
        v-if="total"
      >
        <p class="headline font-weight-bold my-0">
          合計：{{total.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}円
        </p>
      </v-col>

      <v-col
        cols="12"
        v-for="(part, index) in data"
        :key="index"
      >
        <v-card
          class="my-2 py-5"
          elevation="2"
          outlined
          color="brown lighten-5"
        >
          <v-row>
            <v-col>
              <p class="headline font-weight-bold my-0">
                {{part[0]}}
              </p>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <p class="headline my-0">
                {{part[1].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}円
              </p>
            </v-col>
          </v-row>
          <v-row>
            <v-col align="center">
              <v-img
                :src="part[2] != '' ? part[2] : 'https://www.shoshinsha-design.com/wp-content/uploads/2020/05/noimage-760x460.png'"
                max-width="150"
                contain
                alt="No Image"
              />
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: 'HerGacha',

  data: () => ({
    data: [],
    loading: false,
    total: 0,
  }),

  methods: {
    getCalculate() {
      this.data = [];
      this.total = 0;
      this.loading = true;
      axios
        .get("https://script.google.com/macros/s/AKfycbzywMeQFf8T1vVjJaGg7oQM8M9DJEQxMn9xXsWZSK4XQrL_lSpI5hMAuFFtukyLlaGJ/exec")
        .then((response) => {
            response.data.forEach((item) => {
              this.total = this.total + Number(item[1]);
            });
            this.data = response.data;
            this.loading = false;
          }
        )
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },
  },
}
</script>
