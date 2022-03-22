<template>
<div>
    <div class="card">
  <div class="card-header text-center">
    Sha = {{commit.sha}}
  </div>
  <div class="card-body">
    <h5 class="card-title">Author</h5>
    <p class="card-text">{{commit.commit.author.name}}</p>
     <h5 class="card-title">Email</h5>
    <p class="card-text">{{commit.commit.author.email}}</p>
    <h5 class="card-title">Date</h5>
    <p class="card-text">{{commit.commit.author.date}}</p>
    <h5 class="card-title">Message</h5>
    <p class="card-text">{{commit.commit.message}}</p>
  </div>
</div>
</div>
</template>

<script>
import store from "@/store";
import axios from "axios";

export default {
  name: "About",
  data: () => ({
    commit: {},
  }),
  created() {
    axios
      .get("https://api.github.com/repos/vuejs/vue/commits")
      .then((response) => {
        this.commit = response.data.find(
          (commit) => commit.sha === store.currentCommit
        );
      });
  },
};
</script>