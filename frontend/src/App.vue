<template>
  <div class="flex flex-col min-h-screen bg-gray-100">
    <!-- Header -->
    <header class="bg-red-500 text-white p-4">
      <div class="container mx-auto flex justify-between items-center">
        <!-- Menu -->
        <div class="flex gap-4">
          <router-link to="/" class="text-xl font-bold">Home</router-link>
          <router-link to="/about" class="text-xl font-bold">About</router-link>
          <router-link v-if="auth.username" to="/restricted" class="text-xl font-bold">Restricted Page</router-link>
          <p v-else @click="showAlert" class="text-xl font-bold cursor-pointer">Restricted Page</p>
        </div>
        <!-- Authenticated User -->
        <div class="flex gap-2 items-center">
          <p v-if="auth.username" class="text-xl font-bold">{{ auth.username }}</p>
          <div v-if="auth.username">
            <!-- Change background color here -->
            <button class="bg-yellow-500 text-white py-1 px-3 rounded" to="/login" @click="onLogin">Logout</button>
          </div>
          <div v-else>
            <router-link class="bg-yellow-500 text-black py-1 px-3 rounded" to="/login">Login</router-link>
          </div>
        </div>
      </div>
    </header>

    <!-- Body -->
    <main class="container mx-auto flex-grow p-4">
      <router-view></router-view>
    </main>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth";

const auth = useAuthStore();
const router = useRouter();

const onLogin = () => {
  auth.logout();
  router.push("/login");
};

const showAlert = () => {
  alert("You must log in to access this page!");
};
</script>
