<template>
<div class="container">
 <ul class="news__list">

   
<li v-for="article in articles" class="news__item">

<div class="card"> 
   
    <img class="images" :src = "article.urlToImage"/>
    

<div class="card-body">
    <div id="title" >{{article.title}}</div>
	<div id="description">{{article.description}}</div>
</div>

   </div> 

   
</li>
<div class="form">
        <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
        <label class="visually-hidden" for="search">Search</label>
        <input type="search" name="search" v-model="searchTerm"
        id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
        Search term here" />
        <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
        </form>
</div>


 </ul>
 </div>
</template>


<script>
export default {
 data() {
     return {
 articles: [],
 searchTerm: ''
 }

 },


  
 methods: {
 searchNews() {
 let self = this;
 fetch('https://newsapi.org/v2/everything?q='+
self.searchTerm + '&language=en', {
 headers: {
 'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
 }
})
 .then(function(response) {
 return response.json();
 })
 .then(function(data) {
 console.log(data);
 self.articles = data.articles;
 });
 }
 }
}
</script>


<style>

@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
* {
  box-sizing: border-box;
}

.news__list{
    
     
display: grid;
  grid-template-columns: 0.2fr 0.2fr 0.2fr ;

   
   
  }

.form{
    position: absolute;
    
   
}

.card {
 
  margin: 25px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  width: 300px;
}

.card-body {
  
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 20px;
  height: 350px;
}

#title{
    font-weight: bold;
    padding-bottom: 10%;

}

#description {
  font-size: 16px;

}
</style>