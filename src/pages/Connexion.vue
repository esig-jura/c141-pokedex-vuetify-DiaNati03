<template>
  <v-container>
    <h1 class="mb-6 text-center">Connexion</h1>

    <v-form @submit.prevent="login">
      <v-text-field v-model="username" label="Nom d’utilisateur" required />
      <v-text-field v-model="password" label="Mot de passe" required type="password" />

      <v-btn class="mt-4" color="primary" type="submit">Se connecter</v-btn>
    </v-form>
  </v-container>
</template>

<script setup>
  import { ref } from 'vue'
  import { useRouter } from 'vue-router'
  import { useAuthStore } from '@/stores/authStore'

  const username = ref('')
  const password = ref('')
  const router = useRouter()
  const authStore = useAuthStore()

  function login () {
    if (username.value && password.value) {
      authStore.login(username.value)
      router.push('/')
    }
  }
</script>
