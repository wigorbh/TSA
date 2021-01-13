<template>
  <div id="app">
    <div id="nav">
      <router-link class="anchor" :to="{name: 'list'}">Lista</router-link>
      <router-link class="anchor" :to="{name: 'register'}">&#9702; Cadastro</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>

</script>
<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

.anchor {
  color: #fff;
  margin-right: 30px;
  text-decoration: none;
}

#nav {
  align-items: center;
  background: #17222D;
  display: flex;
  height: 3rem;
  justify-content: flex-end;
  width: 100%;
}


</style>
