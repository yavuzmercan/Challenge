<template>
  <div class="job-detail">
    <div class="job-detail__header">
      <h4>{{selectedjobsItem.positionName}}</h4>
      <p>{{selectedjobsItem.companyName}}</p>
      <p>{{selectedjobsItem.cityName}}</p>
    </div>
    <div class="job-detail__content">
      <p class="job-detail__desc">
        {{selectedjobsItem.description}}
        <br>
        {{selectedjobsItem.address}}
        <br>
        {{selectedjobsItem.contactPhone}}
        <br>
        {{selectedjobsItem.postalCode}}
        <br>
        {{selectedjobsItem.latLong}}
      </p>

      <router-link class="btn btn-primary" :to="{name: 'Home'}">Anasayfa</router-link>
      <router-link class="btn btn-primary" :to="{name: 'JobList', params: { city: 0, keyword: '' }}">İlanlar</router-link>

    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'JobDetail',
  data () {
    return {
      selectedjobsItem:[]
    }
  },
  methods:{
    gotoList: function(idx){
      this.$router.push({name: 'Home'})
    }
  },
  mounted(){
    var that = this;
    /*http://myjson.com/*/
    axios.get('https://api.myjson.com/bins/jsqxf')
    .then((response) =>{
      for(var i= 0; i < response.data.items.length; i++){
        if(response.data.items[i].jobId == this.$route.params.id){
          that.selectedjobsItem = response.data.items[i];
        }
      }
    })
    .catch((error) =>{
      console.log(error)
    })
  }
}
</script>

<style scoped="true" lang="scss">
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #fff;
}

.jumbotron{
  background-color: black;
}
</style>
