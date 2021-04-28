<template>
  <div class="flex justify-center items-center p-5 bg-gray-600 shadow-md">
    <router-link :to="{ name: 'Home' }">
      <h1 class=" text-3xl text-gray-50 font-bold">
        Movie<span class=" text-gray-400">Search</span>
      </h1></router-link
    >
  </div>
  <div>
    <router-view />
  </div>
</template>

<style></style>
