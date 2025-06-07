<template>
    <div class="profile-card">
        <h1 class="name">{{ user.name }}</h1>
        <p class="info"><strong>Company:</strong> {{ user.company?.name }}</p>
        <p class="info"><strong>Phone:</strong> {{ user.phone }}</p>
        <p class="info"><strong>Email:</strong> {{ user.email }}</p>
        <p class="info"><strong>Username:</strong> {{ user.username }}</p>
        <p class="info"><strong>City:</strong> {{ user.address?.city }}</p>
    </div>
</template>
<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

const route = useRoute()
const userId = route.params.id
const user = ref({})

onMounted(async () => {
    const { data } = await axios.get(`https://jsonplaceholder.typicode.com/users/${userId}`)
    user.value = data
})
</script>
<style lang="scss" scoped>
.profile-card {
  background-color: #fff;
  border-radius: 12px;
  padding: 2rem;
  max-width: 400px;
  margin: 2rem auto;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);

  .name {
    font-size: 1.8rem;
    margin-bottom: 1rem;
    color: #2c3e50;
    font-weight: 700;
    border-bottom: 1px solid #eee;
    padding-bottom: 0.5rem;
  }

  .info {
    font-size: 1rem;
    margin: 0.4rem 0;
    color: #555;

    strong {
      color: #333;
      font-weight: 600;
      margin-right: 0.5rem;
    }
  }
}
</style>