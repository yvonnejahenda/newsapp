<template>
  <div class="container">
  <div v-for="article in news">
<img :src="article.urlToImage" alt="">
<h3>{{article.title}}</h3>
<h4>{{article.author}}</h4>
<p>{{article.description}}</p>
<blockquote>
<a href="#"target="_blank" class="button">Read more</a>
</blockquote>

</div>
    
  </div>
</template>

<script>
const url ="https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=4ac0fe61c8e44dd3a091a5edcdb93e17"; 
import axios from 'axios'
const data = {
    news: []
}
export default {
  data: function() {
    return data
  },
  created() {
this.loadnews();
  },
  methods:{
  loadnews(){
  axios.get(url).then(function(response) {
  console.log(response.data.articles)
  data.news = response.data.articles
  }).catch(function(error)
  {
  console.log(error.message)
  })
  }
  }

}
</script>
