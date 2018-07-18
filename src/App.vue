<template>
  <div class="container">
  <input v-model ='search' type="search" name="search"value="" placeholder="Type to search...">

   <button v-on:click="loadnews" type="button">search</button>
   <p v-if="loading">Please wait...</p>
  
  <div v-for="article in news">
<img :src="article.urlToImage" alt="">


<h3>{{article.title}}</h3>
<h4>{{article.author}}</h4>
<p>{{article.description}}</p>
<a class="button" :href="article.url" target="blank">Read More</a>


</div>
    
  </div>
</template>

<script>

import axios from 'axios'
const baseUrl="https://newsapi.org/v2";
const apikey="4ac0fe61c8e44dd3a091a5edcdb93e17";
const endpoint="/everything";


const data = {
    news: [],
    search: '',
    loading:false
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
    if(this.search.length <1){
      return;
    }
    this.loading=true;
    this.news=[];

    let url = baseUrl 
    + endpoint 
    + "?q=" +this.search 
    +'&apikey=' +apikey;

  axios.get(url).then(function(response) {
  console.log(response.data.articles)
  data.loading = false;
  data.news = response.data.articles
  }).catch(function(error)
  {
  console.log(error.message)
  })
  }
  }

}
</script>
