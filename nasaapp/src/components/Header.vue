<template>
  <div class="headerMain">Nasa App Header</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.headerMain{
      background-color: cadetblue;
    padding: 2rem;
}
</style>
