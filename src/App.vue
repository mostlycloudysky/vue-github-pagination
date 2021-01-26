<template>
  <div id="app" class="container">
    <DataTable :githubIssues="githubIssues" />
  </div>
</template>

<script>
import DataTable from "./components/DataTable";
import axios from "axios";
const GITHUB_API =
  "https://api.github.com/repos/angular/angular/issues?state=closed&per_page=5&page=";
export default {
  name: "app",
  components: {
    DataTable
  },
  data() {
    return {
      githubPage: 1,
      githubIssues: []
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(GITHUB_API + this.githubPage)
        .then(response => {
          this.githubIssues = response.data;
          console.log(`Github issues are ${JSON.stringify(this.githubIssues)}`);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
