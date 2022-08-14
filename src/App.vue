<template>
  <div id="app">
    <h1 class="title">Gifosaure</h1>
    <div class="centered">
      <b-field label="Chercher" class="centered">
          <b-input v-model="query" @input="searchTags"></b-input>
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
const gifs = [
        {
          url : "https://c.tenor.com/FsuzVwvsu2kAAAAd/tigger-tigger-winnie-the-pooh.gif",
          tags : ["tigrou", "sad", "triste", "winnie"],
        }, {
          url : "https://c.tenor.com/0MhHbJND7CIAAAAC/mister-v-again.gif",
          tags : ["mister v", "beaucoup", "encore"]
        },
        {
          url : "https://c.tenor.com/Hu-O81bs6SIAAAAM/rene-ren%C3%A9malleville.gif",
          tags : ["rene", "minute", "est", "honteux"]
        },
        {
          url :"https://c.tenor.com/oP3VasmkrSQAAAAS/cest-bien-cest.gif",
          tags : ["maillon", "faible", "content", "eleonore", "laurence", "boccolini"]
        },
        {
          url : "https://y.yarn.co/45aa62aa-f2d7-4f7e-a820-353274daca35_text.gif",
          tags : ["gina", "cancer", "not", "even", "cure"]
        }
      ]
export default {
  name: 'App',
  components: {
    GifCard
  },
  data() {
    return {
      query : "",
      gifs : gifs
    }
  },
  methods : {
    getScore(gif, tags) {
      let matches = 0;
      tags.forEach(searchTag => {
        gif.tags.forEach(gifTag => {
          if (gifTag.includes(searchTag.toLowerCase())) matches++;
        })
      })
      return matches;
    },
    searchTags() {
      let tags = this.query.split(" ").filter((s) => s !== '');
      console.log(tags);
      if (tags.length === 0) this.gifs = gifs
      else {
        tags = tags.map(e => e.normalize("NFD").replace(/[\u0300-\u036f]/g, ""))
        console.log(tags);
        gifs.forEach(gif => gif.score = this.getScore(gif, tags))
        console.log(gifs);
        this.gifs = gifs
          .filter(gif => gif.score !== 0)
          .sort((a, b) => {a.score < b.score})
      }
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
