<template>
  <div id="app" class="container">
    <DataTable />
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
      githubPage: 1
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(GITHUB_API + this.githubPage)
        .then(({ data }) => {
          console.log(data);
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
