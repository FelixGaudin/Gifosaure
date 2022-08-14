<template>
  <div id="app">
    <h1 class="title">Gifosaure</h1>
    <div class="centered">
      <b-field label="Chercher" class="centered">
          <b-input v-model="query"></b-input>
      </b-field>
    </div>

    <div class="gifs">
      <div class="gif" v-for="gif in gifs" :key="gif.url">
        <GifCard :url="gif.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import GifCard from './components/GifCard.vue'

export default {
  name: 'App',
  components: {
    GifCard
  },
  data() {
    return {
      query : "",
      gifs : [
        {
          url : "https://c.tenor.com/FsuzVwvsu2kAAAAd/tigger-tigger-winnie-the-pooh.gif",
          tags : [],
        }, {
          url : "https://c.tenor.com/0MhHbJND7CIAAAAC/mister-v-again.gif",
          tags : []
        },
        {
          url : "https://c.tenor.com/Hu-O81bs6SIAAAAM/rene-ren%C3%A9malleville.gif",
          tags : []
        },
        {
          url :"https://c.tenor.com/oP3VasmkrSQAAAAS/cest-bien-cest.gif",
          tags : []
        },
        {
          url : "https://y.yarn.co/45aa62aa-f2d7-4f7e-a820-353274daca35_text.gif",
          tags : []
        }
      ]
    }
  }
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/@mdi/font@5.8.55/css/materialdesignicons.min.css');
@import url('https://use.fontawesome.com/releases/v5.2.0/css/all.css');

html,body{
  border:none; padding:0; margin:0;
  background:#FFFFFF;
  color:#202020;
}
body{
  text-align:center;
  font-family:"Roboto",sans-serif;
}
#app {
  margin: 2em;
}
.title {
  font-size: 2em;
}
.centered {
    margin: auto;
    align-items: center;
    text-align: center;
    width: 60vw;
}
.gifs {
    width: 70vw;
    margin: auto;
    margin-top: 30px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
}
.gif {
    margin: 10px;
    width: 300px;
    /* min-width: 100px; */
    /* max-height: 25vw; */
}
</style>
