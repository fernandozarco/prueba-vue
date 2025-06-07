<template>
  <div class="users">
    <div class="search-bar">
        <input type="text" v-model="query" placeholder="Busca por nombre" class="search-bar">
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
            <button @click="$router.push(`/user/${user.id}`)">View user</button>
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
<style lang="scss" scoped>
.users {
    width: 50vw;
}
.search-bar {
  display: flex;
  align-items: center;

  input[type="text"] {
    padding: 0.6rem 1rem;
    border: 2px solid #ccc;
    border-radius: 8px;
    font-size: 1rem;
    outline: none;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
    width: 100%;

    &:focus {
      border-color: #3498db;
      box-shadow: 0 0 5px rgba(52, 152, 219, 0.5);
    }

    &::placeholder {
      color: #999;
      font-style: italic;
    }
  }
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
  background-color: #fff;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  overflow: hidden;

  thead {
    background-color: #f5f5f5;

    th {
      text-align: left;
      padding: 0.75rem 1rem;
      font-weight: 600;
      color: #444;
      text-transform: capitalize;
    }
  }

  tbody {
    tr {
      border-top: 1px solid #eee;

      &:hover {
        background-color: #f0f8ff;
      }

      td {
        padding: 0.75rem 1rem;
        color: #333;
        vertical-align: middle;
      }

      button {
        background-color: #3498db;
        color: #fff;
        border: none;
        padding: 0.4rem 0.8rem;
        border-radius: 6px;
        cursor: pointer;
        transition: background-color 0.3s ease;

        &:hover {
          background-color: #2980b9;
        }
      }
    }
  }
}
</style>
