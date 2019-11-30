<template>
  <div class="navigation">
    <h1>
      Newsgraph 
    </h1>
    <div class="links">
      <nuxt-link v-for="i in menu" :key="i.href" :class="['a-clear','component',{'active':getActive(i.href)}] " :to="i.href">
        {{ i.title }}
      </nuxt-link>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      menu: [
        {
          href: '/',
          title: 'Главная'
        },
        {
          href: '/news',
          title: 'Новости'
        }

      ]
    }
  },
  methods: {
    getActive (value) {
      return this.$route.path === value
    }
  }
}
</script>
<style lang="scss" scoped>
.navigation{
  color:white;
  justify-content: space-between;
  display: flex;
  align-items: center;
  height: $top-menu;
  padding: 1em 0;
  text-transform: uppercase;
  position: absolute;
  width: calc(100% - 8em);
  top: 0;
  .component{
    margin-right: auto;
    font-size:0.875em;
    font-weight: 700;
    &:hover{
      color:dimgray;
    }
  }
  @media (max-width: $small-bp){
    h1{
      display: none;
    }
  }
  .active{
    color: #d09959;
  }
  .links{
    width: 17em;
    display: flex;
  }
}
</style>
