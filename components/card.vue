<template>
  <div>
    <v-toolbar color="orange accent-1">
      <v-btn
        color="orange accent-1"
        class="ma-2 white--text"
        href="/profile/create"
      >
        Tambah
        <v-icon right dark>mdi-cloud-upload</v-icon>
      </v-btn>
      <v-text-field
        hide-details
        prepend-icon="mdi-magnify"
        single-line
        v-model="cari"
        placeholder="cari resep disini.."
      ></v-text-field>
      <template v-slot:extension>
        <v-tabs color="blue-grey" slider-color="blue-grey">
          <v-tab href="/profile/">menu</v-tab>
          <v-tab @click="getKategori(1)">masakan asia</v-tab>
          <v-tab @click="getKategori(2)">masakan eropa</v-tab>
          <v-tab @click="getKategori(3)">masakan amerika</v-tab>
        </v-tabs>
      </template>
    </v-toolbar>
    <div class="row">
      <v-col
        v-for="resep in filtered"
        :key="String(resep.id)"
        :id="String(resep.id)"
        cols="4"
        class="d-flex child-flex"
      >
        <v-card class="mx-auto my-12" max-width="374">
          <v-img
            height="250"
            :src="resep.gambar"
            @click="view(resep.id)"
          ></v-img>

          <v-card-title class="justify-center" @click="view(resep.id)">{{
            resep.judul
          }}</v-card-title>

          <v-card-text>
            <v-row align="center" class="mx-0" @click="view(resep.id)">
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

            <div class="my-4 subtitle-1" @click="view(resep.id)">
              $ • {{ resep.kategori }}
            </div>

            <div @click="view(resep.id)">
              {{ resep.keterangan }}
            </div>
          </v-card-text>

          <v-divider class="mx-4"></v-divider>

          <v-card-actions>
            <v-btn outlined color="primary" @click="edit(resep.id)">
              <v-icon left>mdi-pencil</v-icon> Edit
            </v-btn>
            <v-btn color="error" outlined @click="hapus(resep.id)">
              <v-icon>mdi-delete</v-icon>
              Delete
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </div>
  </div>
</template>
<script>
import Axios from "axios";
export default {
  data() {
    return {
      reseps: [],
      cari: ""
    };
  },
  computed: {
    filtered() {
      return this.reseps.filter(item =>
        item.judul.toLowerCase().match(this.cari.trim().toLowerCase())
      );
    }
  },
  mounted() {
    this.Dataku();
  },
  methods: {
    async Dataku() {
      try {
        const res = await Axios.get("http://localhost:3001/reseps?_sort=id&_order=desc");
        this.reseps = res.data;
      } catch (err) {
        Console.error(err);
        this.isError = true;
      }
    },
    async getKategori(id) {
      try {
        const res = await Axios.get(
          "http://localhost:3001/reseps?id_kategori=" + id
        );
        this.reseps = res.data;
      } catch (err) {
        Console.error(err);
        this.isError = true;
      }
    },
    view(resepId) {
      this.$router.push({ path: "/profile/" + resepId });
    },
    hapus(resepId) {
      const setuju = confirm("anda yakin ingin menghapus?");
      if (!setuju) {
        return;
      }
      Axios.delete("http://localhost:3001/reseps/" + resepId).then(_ => {
        this.Dataku();
      });
    },
    edit(resepId) {
      this.$router.push({ path: "/profile/" + resepId + "/edit" });
    }
  }
};
</script>
