<template>
  <navbar class="container"/>
  <div>
    <router-view></router-view>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar"
export default {
  components: {
    Navbar
  }
}
</script>

<style>
  
</style>