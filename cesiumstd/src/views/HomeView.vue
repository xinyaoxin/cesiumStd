<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld />
    <!-- <Calculate /> -->
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Calculate from '@/components/Calculate.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    Calculate
  }
}
</script>
