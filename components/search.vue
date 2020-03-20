<template>
  <v-toolbar color="orange accent-1">
    <v-text-field
      hide-details
      prepend-icon="mdi-magnify"
      single-line
      v-model="cari"
      placeholder="cari resep disini.."
    ></v-text-field>
    <template v-slot:extension>
      <v-tabs
        v-model="tab"
        :hide-slider="!model"
        color="blue-grey"
        slider-color="blue-grey"
      >
        <v-tab href="/profile/create">tambah resep</v-tab>
        <v-tab :disabled="!model">masakan asia</v-tab>
        <v-tab :disabled="!model">masakan eropa</v-tab>
        <v-tab :disabled="!model">masakan amerika</v-tab>
      </v-tabs>
    </template>
  </v-toolbar>
</template>
