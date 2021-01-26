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
      <tr v-for="issue in showIssues" :key="issue.id" class="mt-2">
        <th scope="row">{{ showIssues.indexOf(issue) + 1 }}</th>
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
    githubIssues: Array,
    showIssues: Array
  }
};
</script>

<style scoped>
.avatar {
  max-width: 20px;
}
</style>
