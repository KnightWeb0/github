<script setup>
import { ref } from 'vue'
const props = defineProps({
  username: { type: String, required: true }
})

// we are grabbing data from an github api

// fetch('https://api.github.com/users/[username]')
//because we have props we can use them instead

//how do i get this data to work with me in the template
//we have to create a reactive vairable to use this data called user

const user = ref()

fetch(`https://api.github.com/users/${props.username}`).then(async (res) => {
  //this will give our data in a json format
  const data = await res.json()
  //now we can se the user .value to = data from our api
  //to access it
  user.value = data
})
</script>

<template>
  <pre> {{ user }}  </pre>

  if user exists display
  <div v-if="user" class="m-5 shadow-xl card card-side bg-base-100">
    <figure>
      <img :src="user.avatar_url" alt="Movie" />
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ user.name }}</h2>
      <p>
        <strong>Followers:</strong> {{ user.followers }} <strong>Following:</strong>
        {{ user.following }}
      </p>
      <div class="justify-end card-actions">
        <a :href="user.html_url" class="btn btn-primary">View Profile</a>
      </div>
    </div>
  </div>
</template>
