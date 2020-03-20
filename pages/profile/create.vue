<template>
  <v-form ref="form" lazy-validation>
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
    <v-container fluid>
      <p>{{ radios || "null" }}</p>
      <v-radio-group v-model="resep.id_kategori" :mandatory="false">
        <v-radio label="masakan asia" value="1"></v-radio>
        <v-radio label="masakan eropa" value="2"></v-radio>
        <v-radio label="masakan amerika" value="3"></v-radio>
      </v-radio-group>
    </v-container>
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
      radios: "id kategori",
      resep: {},
      items: ["masakan asia", "masakan eropa", "masakan amerika"]
    };
  },
  mounted() {
    this.Dataku;
  },
  methods: {
    kirim() {
      Axios.post("http://localhost:3001/reseps/", this.resep).then(_ => {
        this.$router.push("/profile");
      });
    }
  }
};
</script>
