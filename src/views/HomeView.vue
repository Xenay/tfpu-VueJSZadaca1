<template>
  <h1 class="pt-1 mb-1 fs-1">List</h1>

  <ul class="list-group list-group-flush">
    <Commit v-for="item in commits"
      :key="item.sha"
      :details="item"
      @click="setCommit(item.sha)"
      />

    </ul>
</template>


<script>
import Commit from "@/components/Commit.vue";
import store from "@/store";
import axios from "axios";
export default {
name: "HomeView",
  

 data() { 
    return {
      commits: [],
    };
  },
  
  created() {
    axios
      .get("https://api.github.com/repos/vuejs/vue/commits")
      .then((response) => {
        this.commits = response.data;
      });
  },
  
     
  
  components: {Commit,}, 
   methods: {
    setCommit(sha) {
      store.currentCommit = sha;
    },
  },
};
</script>    
