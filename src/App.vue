<template>
  <div id="app" v-if="results">
    <div class="card-header-custom mx-5">
      <div>
        <p class="title mt-5">Overall Rating</p>
        <div class="votes">
          <p class="mb-0 mr-2 marks text-green">4.2</p>
          <StarRating v-model="rating"></StarRating>
          <p class="ml-3 mb-0">{{ results.dob.age }} Votes</p>
        </div>
      </div>
      <button class="btn-add">+</button>
    </div>
    <hr class="my-4" />
    <div class="user-container mx-5">
      <div class="user">
        <img
          class="avatar"
          :src="results.picture.thumbnail"
          alt="avatar"
        />
        <div class="ml-3">
          <p class="title mb-0">{{ `${results.name.first} ${results.name.last}` }}</p>
          <div class="votes">
            <StarRating v-model="rating"></StarRating>
            <p class="ml-3 mb-0">{{ `6` }} ago</p>
          </div>
        </div>
      </div>
      <p class="mb-0 mt-3 font-13">
        {{ `${results.email} and ${results.phone}` }}
      </p>
      <p class="mb-0 mt-3">{{`from ${results.dob.date} and ${results.dob.age}`}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import StarRating from "./components/StarRating";

export default {
  name: "App",
  components: {
    StarRating,
  },
  data() {
    return {
      results: null,
      rating: 3,
    };
  },
  created() {
    axios.get("https://randomuser.me/api").then((response) => {
      this.results = response.data.results[0];
      console.log(this.results)
    });
  },
};
</script>

<style>
#app {
  border-radius: 15px;
  width: 400px;
  height: 400px;
}
.card-header-custom {
  display: flex;
  justify-content: space-between;
}
.title {
  text-align: left;
  font-size: 14pt;
  font-weight: 600;
}
.btn-add {
  width: 60px;
  height: 60px;
  margin-top: auto;
  margin-bottom: auto;
  background-color: rgb(243, 246, 246);
  border: none;
  border-radius: 5px;
  outline: none;
}
.font-13 {
  font-size: 13pt;
}
.marks {
  font-size: 14pt;
}
.votes {
  display: flex;
}
.user {
  display: flex;
}
.user .avatar {
  width: 60px;
  height: 60px;
  margin-top: auto;
  margin-bottom: auto;
  border-radius: 15px;
}
</style>
