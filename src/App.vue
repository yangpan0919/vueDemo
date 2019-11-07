<template>
  <div class="container">
    <Search/>
    <MainBody/>

  </div>
</template>

<script>

  import Search from './components/Search'
  import MainBody from './components/MainBody'

  export default {
    components: {MainBody, Search}
  }
</script>

<style scoped>


</style>
