<template>
  <div>
    <div class="container">
      <template  v-for="article in articles">
      <div v-if="article.type!=='short'" :key="article.id" class="block-article" :style="{'background-image': 'url(' + article.preview + ')' }">
        <span> {{ article.title }}</span>
        <p> {{ article.short_description }}</p>
        <div class="date">
          {{$moment(article.date).fromNow()}}
        </div>
        <div class="back" />
      </div>
      <div v-else :key="'short' + article.id" class="block-short" >
        <div v-for="slot in article.data" class="pick" :key="slot.id">
          <span>{{slot.title}}</span>
          <p>{{$moment(slot.date).fromNow()}}</p>
        </div>
      </div>
      </template>
      <div class="background">
        <img src="@/assets/img/backgroung.png">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  components: {
  },
  async asyncData ({ $axios }) {
    const data = await $axios.$get('/news.json')
    return { articles: data.data }
  }
}
</script>

<style lang="scss" scoped>
.container{
  min-height: 100vh;
  border-radius: 12px;
  margin:auto;
  background-color: #fff;
  justify-content: center;
  margin-top:$top-menu;
  padding:1em 2em;
  margin-bottom:2em;
  display:flex;
  flex-wrap: wrap;
  .block-article{
    color:#fff;
    width: calc(50% - 1em);
    background-size: cover;
    background-position: center;
    margin:0 .5em;
    display:flex;
    flex-direction: column;
    margin-top:1em;
    padding:1em;
    border-radius: 12px;
    height: 23em;
    color: #fff;
    span{
      margin-top: auto;
      font-size: 2em;
      font-weight: 600;
      @media (max-width: $medium-bp) {
        font-size:1em;
      }
    }
    span, p,.date {
      z-index:2;
    }
    p{
       @media (max-width: $medium-bp) {
        font-size:.7em;
      }
    }
    .date{
      font-weight: 200;
       @media (max-width: $medium-bp) {
        font-size:.5em;
      }
    }
    .back{
      background-color: rgba(0,0,0,0.5);
      position: absolute;
      z-index: 1;
      width: calc(50% - 7em);
      height: 23em;
      margin: -1em;
      border-radius: 12px;
    }
    &:nth-last-child(2){
      width: calc(100%);
      .back{
        @media (min-width:$medium-bp) {
           width: calc(100% - 13em);
        }
      }
    }
  }
  .block-short{
    color:#000;
    background-color: #fff;
    justify-content: space-between;
    width: calc(50% - 1em);
    display:flex;
    flex-direction: column;
    margin:0 .5em;
    margin-top:1em;
    padding:1em;
    border-radius: 12px;
    height: 23em;
    border: 1px solid;
    border-color: rgba(0,0,0,0.2);
    .pick:not(:last-child){
      margin-bottom: .5em;
      border-bottom: 1px solid;
      border-color: rgba(0,0,0,0.2);
    }
    span{
      @media (max-width: $medium-bp) {
        font-size:.6em;
      }
      p{
        @media (max-width: $medium-bp) {
        font-size:.5em;
      }
      }
    }
    .pick{
      p{
        font-weight: 300;
        color:grey;
        font-size: .825em;
        margin-top: .5em;
        margin-bottom: 1em;
      }
    }
  }
  @media (max-width: $medium-bp){
    padding:.5em .2em;
    max-width: 16em;
    .block-article{
      width: 100%;
      margin:0;
      margin-top:1em;
      .back{
        width: calc(15.6em);
        &:nth-last-child(2){
          width:calc(15.6em) !important;
        }
      }
    }
    .block-short{
      width: calc(100%);
    }
  }
}
.background{
  opacity: .09;
  height: 100vh;
  left:-4em;
  position: fixed;
  z-index:-1;
  top: 0;
  left:-1em;
  img{
    height: 100vh;
  }
}
</style>
