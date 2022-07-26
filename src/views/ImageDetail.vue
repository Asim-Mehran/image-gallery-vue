<template>
    <div>
    <div class="row">
      <div class="d-flex align-items-center justify-content-center">
      <img  v-bind:src="image?.url" /> 
      </div>   
  </div>
    <div class="row"><h3>{{image?.title}}</h3></div>
  </div>


</template>
<script>

export default {
  name: 'ImageDetail',
  props:{
    image:Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

