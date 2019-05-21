
<template>
<div class="job-list">
  <div class="row">
    <div class="col-xs-6">
      <h3 class="job-list__title">İlanlar</h3>
    </div>
    <div class="col-xs-6 text-right">
    <router-link class="btn btn-primary" :to="{name: 'Home'}">Anasayfa</router-link>
    </div>
  </div>

  <ul class="job-list__items">
    <li class="job-list__item"
    v-for="item in filteredList"
    :key="item.jobId"
    @click="gotoDetail(item.jobId)">
      <h4 class="job-list__position-name">{{item.positionName}}</h4>
      <p class="job-list__compony-name">{{item.companyName}}</p>
      <p class="job-list__city">{{item.cityName}}</p>
    </li>

  </ul>
</div>
</template>

<script>
import axios from 'axios'


export default {
  name: 'JobList',
  data: function() {
  	return {
      jobs:[],
    	//location: this.$route.params.city,
      //keyword: this.$route.params.keyword.toLowerCase()
    }
  },
  methods:{
    gotoDetail: function(idx){
      this.$router.push({name:'JobDetail', params:{id: idx,city: this.location, keyword: this.keyword }})
    }
  },
  created(){
    console.log("asd")
    /*http://myjson.com/*/
    axios.get('https://api.myjson.com/bins/19edxv')
    .then((response) =>{
      this.jobs = response.data.items;
    })
    .catch((error) =>{
      console.log(error)
    })
  },
  computed: {
    filteredList() {
      var vm = this;
      var loc = vm.location;
      var ke = vm.keyword;
      
      if( Object.keys(this.$route.params).length == 0){
        return vm.jobs;
      }
      else{
        return vm.jobs.filter(function(job){
          return (job.cityName === vm.location &&  job.positionName.toLowerCase().includes(vm.keyword)) || (vm.location == 0 && job.positionName.toLowerCase().includes(vm.keyword))
        })
      }
    },
    location() {
      return Object.keys(this.$route.params).length == 0 ? "0" : this.$route.params.city;
    },
    keyword() {
      return Object.keys(this.$route.params).length == 0 ? "" : this.$route.params.keyword;
    }
  }
}

</script>

<style lang="scss" scoped="true">
  .job-list{
      &__items{
        list-style: none;
        padding: 0;
      }
      &__title{
        color: #912da2;
        margin-top: 0;
      }
      &__item{
        padding: 20px;
        border-bottom: 1px solid #ebebeb;
        cursor: pointer;
        &:hover{
          background-color: #fafbfc;
        }
      }
      &__position-name{
        font-size: 17px;
        margin-bottom: 4px;
      }
      &__compony-name{
        font-size: 15px;
        color:#666;
        margin-bottom: 4px;
      }
      &__city{
        font-size: 13px;
        color:#999;
      }
  }
</style>
