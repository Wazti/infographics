<template>
  <div class="layout">
    <nuxt />
    <navigation-bar />
  </div>
</template>

<script>
import NavigationBar from '@/components/NavigationBar'
export default {
  components: {
    NavigationBar
  }
}
</script>
<style lang="scss">

html{
  font-family: Geometria;
}
.layout{
  padding:0 4em;
  @media (max-width: $small-bp){
    padding: 0 .5em;
  }
}
*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

</style>
