<template>
  <div id="app" class="container">
    <h1 class="pb-2">
      <icons :icon="['fas', 'start']" />
      Hubination
    </h1>
    <DataTable :showIssues="showIssues" :githubIssues="githubIssues" />
    <div class="my-5">
      <ul class="pagination pagination-md justify-content-center text-center">
        <li class="page-item" :class="page === 1 ? 'disabled' : ''">
          <a class="page-link" @click="prevPage">Previous</a>
        </li>
        <li class="page-link" style="background-color: inherit">
          {{ page }} of {{ lastPage }}
        </li>
        <li class="page-item" :class="page === lastPage ? 'disabled' : ''">
          <a class="page-link" @click="nextPage">Next</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import DataTable from "./components/DataTable";
import axios from "axios";
const GITHUB_API =
  "https://api.github.com/repos/angular/angular/issues?state=closed&per_page=100&page=";
export default {
  name: "app",
  components: {
    DataTable
  },
  data() {
    return {
      githubPage: 1,
      githubIssues: [],
      page: 1,
      loading: false,
      perPage: 20
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.loading = true;
      axios
        .get(GITHUB_API + this.githubPage)
        .then(response => {
          this.githubIssues = response.data;
          console.log(`Github issues are ${JSON.stringify(this.githubIssues)}`);
        })
        .catch(err => {
          console.log(err);
        });
    },
    prevPage() {
      this.loading = true;
      this.page--;
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
    nextPage() {
      this.loading = true;
      this.page++;
      window.scrollTo({ top: 0, behavior: "smooth" });
    }
  },
  computed: {
    showIssues() {
      let start = (this.page - 1) * this.page;
      let end = start + this.perPage;
      // this.loading = false;
      return this.githubIssues.slice(start, end);
    },
    lastPage() {
      let length = this.githubIssues.length;
      return length / this.perPage;
    }
  }
};
</script>

<style>
@keyframes spinner {
  to {
    transform: rotate(360deg);
  }
}
.fa-spinner {
  animation: spinner 1s linear infinite;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
a:hover {
  cursor: pointer;
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
