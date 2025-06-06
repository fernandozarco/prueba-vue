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
    console.log('HIJO APP', userId)
    const { data } = await axios.get(`https://jsonplaceholder.typicode.com/users/${userId}`)
    user.value = data
    console.log('user', user.value)
})

</script>
<style>
.profile-card {
    border: thin solid red;
    margin: 1rem;
}
</style>