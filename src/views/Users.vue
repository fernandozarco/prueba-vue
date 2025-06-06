<template>
  <div class="users">
    <table>
      <thead>
        <tr>
          <th></th>
          <th>name</th>
          <th>username</th>
          <th>email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) of users" v-bind:key="index">
          <td>
            <button @click="$router.push(`/user/${user.id}`)">View</button>
            <!-- <button @click="viewUser(user.id)">View</button> -->
          </td>
          <td>{{ user.name }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <main>
  </main>
</template>

<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'
import User from './User.vue'
import { useRouter } from 'vue-router'

const users = ref([])
const userId = ref(null)
const router = useRouter()

onMounted(async () => {
  console.log('onmounted')
  const { data } = await axios.get('https://jsonplaceholder.typicode.com/users')
  users.value = data
  console.log(users.value)
})

const viewUser = async (id) => {
  console.log('viewUser', id)
  userId.value = id
}
</script>
<style scoped>
.users {
    border: thin solid purple;
    width: 50vw;
}
</style>
