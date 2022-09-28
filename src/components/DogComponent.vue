<template>
  <v-card color="grey lighten-2">
    <v-card-title>
      <div>
        <h3>{{ dog.name }}</h3>
        <p>{{ dog.breed }}</p>
      </div>
    </v-card-title>
    <v-img :src="img" height="170px" />
    <v-btn @click="$emit('addFavorites', dog)">Add To Favorites</v-btn>
  </v-card>
</template>

<script>
import axios from "../plugins/axios";

export default {
  name: "DogComponent",
  props: {
    dog: {
      type: Object,
    },
  },
  data: function () {
    return {
      img: "",
    };
  },
  methods: {
    getData: function () {
      axios
        .get("/breed/" + this.dog.breed + "/images/random")
        .then((res) => {
          console.log(res.data.message);
          this.img = res.data.message;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

  created: function () {
    this.getData();
  },
};
</script>
