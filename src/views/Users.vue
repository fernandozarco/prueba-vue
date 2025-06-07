<template>
  <div class="users">
    <div class="search-bar">
        <label for="">Busqueda por nombre</label>
        <input type="text" v-model="query">
        {{ query }}
    </div>
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
        <tr v-for="(user, index) of filteredUsers" v-bind:key="index">
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
import { ref, onMounted, computed } from 'vue'
import User from './User.vue'
import { useRouter } from 'vue-router'

const users = ref([])
const userId = ref(null)
const router = useRouter()
const query = ref('')

onMounted(async () => {
  console.log('onmounted')
  const { data } = await axios.get('https://jsonplaceholder.typicode.com/users')
  users.value = data
  filteredUsers.value = [...users.value]
})

const viewUser = async (id) => userId.value = id

const filteredUsers = computed(() =>
  users.value.filter(user =>
    user.name.toLowerCase().includes(query.value.toLowerCase())
  )
)
</script>
<style scoped>
.users {
    border: thin solid purple;
    width: 50vw;
}
</style>
