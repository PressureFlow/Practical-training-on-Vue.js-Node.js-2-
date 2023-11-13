<template>
  <NavComp/>

  <router-view v-slot="{ Component }">
    
    <transition name="fade" mode="out-in">
      <component :is="Component"/>
    </transition>

  </router-view>
  
</template>

<script>
import NavComp from './components/Navigation/Navigation.vue'


export default {
  name: 'App',
  components: {
    NavComp
  }
}
</script>

<style>
#app {
  font-family: sans-serif, 'Montseratt';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}



</style>
