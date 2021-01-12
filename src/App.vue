<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{name: 'list'}">Lista</router-link>
      <router-link :to="{name: 'register'}">Cadastro</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>
export default {
  data(){
    return {
      age: 1
    }
  }
}
</script>
<style lang="scss">


</style>
