<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="resep.judul"
      :counter="30"
      label="Judul masakan"
      required
    ></v-text-field>

    <v-text-field
      v-model="resep.keterangan"
      label="Keterangan"
      required
    ></v-text-field>
    <v-select
      v-model="resep.kategori"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Kategori"
      required
    ></v-select>
    <v-text-field v-model="resep.by" label="Chef" required></v-text-field>

    <v-text-field
      v-model="resep.gambar"
      label="tambahkan url gambar"
      required
    ></v-text-field>
    <v-textarea
      outlined
      name="input-7-4"
      label="bahan"
      v-model="resep.bahan"
    ></v-textarea>
    <v-textarea
      outlined
      name="input-7-4"
      label="Cara buat"
      v-model="resep.resep"
    ></v-textarea>

    <v-btn color="error" class="mr-4" @click.prevent="kirim">
      simpan
    </v-btn>

    <v-btn color="warning" href="/profile">
      kembali
    </v-btn>
  </v-form>
</template>
<script>
import Axios from "axios";
export default {
  data() {
    return {
      resep: {},
      items: ["masakan asia", "masakan eropa", "masakan amerika"]
    };
  },
  mounted() {
    this.getDetail();
  },
  methods: {
    getDetail() {
      Axios.get(
        "http://localhost:3001/reseps/" + this.$route.params.profileId
      ).then(res => {
        this.resep = res.data || {};
      });
    },
    kirim() {
      Axios.patch(
        "http://localhost:3001/reseps/" + this.$route.params.profileId,
        this.resep
      ).then(_ => {
        this.$router.push("/profile");
      });
    }
  }
};
</script>
