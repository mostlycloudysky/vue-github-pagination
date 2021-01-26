<template>
  <table class="table">
    <thead class="table-dark">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Title</th>
        <th scope="col">Issue Number</th>
        <th scope="col">User Name</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="issue in githubIssues" :key="issue.id">
        <th scope="row">{{ githubIssues.indexOf(issue) + 1 }}</th>
        <td>{{ issue.title }}</td>
        <td>{{ issue.number }}</td>
        <td>{{ issue.user.login }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "DataTable",
  props: {
    githubIssues: Array
  }
};
</script>

<style scoped>
.avatar {
  max-width: 20px;
}
</style>
