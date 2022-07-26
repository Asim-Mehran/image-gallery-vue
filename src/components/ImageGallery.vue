<template>
<div class="imagegallery">
<div class="row d-flex align-items-center justify-content-center">
   <div class="col-xl-3 col-lg-4 col-sm-6 col-md-6 ml-2">
    <input v-model="searchKeyword" @keyup="onTypeSearch()" type="text" placeholder="Type to search" class="search form-control" />
  </div>
</div>
  <div class="row">
    <div v-bind:key="image.id" v-for="image in filterList" class="col-xl-3 col-lg-4 col-sm-6 col-md-6 mt-5">
    <div class="container" @click="onClickImage(image)">
      <img  v-bind:src="getRandomSizeUrl(image.url)" /> 
       <div class="overlay">
    <div class="text">{{image.title}}</div>
    </div>
  </div>
  </div>
</div>
</div>
</template>

<script>
export default {
  name: 'ImageGallery',
  data(){
return {
  imageList:[],
  filterList:[],
  searchKeyword:''
}
  },
  methods:{
   onClickImage: function(image) {
    this.$router.push({name:'imagedetail',params:{ image} });
   },
    onTypeSearch: function() {
    this.filterList = this.imageList.filter(x=>x.title.toLowerCase().includes(this.searchKeyword.trim().toLowerCase()));
   },
   getRandomSizeUrl: function(url) {
    let splitUrl=url.split('600');
    let number=Math.floor(Math.random() * 50) + 250;
    return `${splitUrl[0]}/${number}/${splitUrl[1]}`;
   }
  },
  created:function(){
    fetch("https://jsonplaceholder.typicode.com/photos")
    .then((response) => response.json()).then((response) => {
     this.imageList= response.slice(0,16);
     this.filterList= response.slice(0,16);
})}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  position: relative;
}

.image {
  display: block;
  width: auto;
  height: auto;
}
.search::-ms-clear {
    display: none;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: .5s ease;
  background-color: #008CBA;
}

.container:hover .overlay {
  opacity: 1;
}

.text {
  color: white;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
}
</style>
