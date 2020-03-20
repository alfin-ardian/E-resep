<template>
  <div>
    <v-card :loading="loading" class="mx-auto my-12" max-width="374">
      <v-card-title class=" justify-center">{{ resep.judul }} </v-card-title>
      <v-img height="250" :src="resep.gambar"></v-img>

      <v-card-text>
        <v-row align="center" class="mx-0">
          <v-rating
            :value="4.5"
            color="amber"
            dense
            half-increments
            readonly
            size="14"
          ></v-rating>

          <div class="grey--text ml-4">4.5 (413)</div>
        </v-row>

        <div class="my-4 subtitle-1">
          <v-avatar>
            <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
          </v-avatar>
          by : chef {{ resep.by }}
        </div>

        <h4>Bahan-bahan:</h4>
        <div>
          {{ resep.bahan }}
        </div>
        <h4>Cara buat:</h4>
        <div>
          {{ resep.resep }}
        </div>
      </v-card-text>
      <v-btn
        class="justify-center"
        color="deep-purple lighten-2"
        href="/profile"
      >
        kembali
      </v-btn>

      <v-divider class="mx-4"></v-divider>
    </v-card>
  </div>
</template>
<script>
import Axios from "axios";
import search from "~/components/search.vue";
export default {
  data() {
    return {
      resep: {},
      id: this.$route.params.profileId
    };
  },
  mounted() {
    Axios.get(
      "http://localhost:3001/reseps/" + this.$route.params.profileId
    ).then(res => {
      this.resep = res.data || {};
    });
  },
  components: {
    search
  }
};
</script>
