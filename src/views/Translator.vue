<template>
  <div class="about">
    <h1>This is an akios page</h1>
    <p v-if="errored" v-cloak>{{ error }}</p>
    <p v-if="loading" v-cloak>Loading...</p>

    <div v-else>
      <ul>
        <li v-for="todo in todos" :key="todo.id" v-cloak>{{ todo.title }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

// ビューモデル
export default Vue.extend({
  data() {
    return {
      loading: true,
      errored: false,
      error: null,
      todos: null
    }
  },
  mounted() {
    axios
      .get('https://jsonplaceholder.typicode.com/todos', {
        params: { userId: '1' }
      })
      .then(response => {
        this.todos = response.data
      })
      .catch(err => {
        ;(this.errored = true), (this.error = err)
      })
      .finally(() => (this.loading = false))
  }
})
</script>
