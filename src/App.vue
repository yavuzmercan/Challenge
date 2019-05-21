<template>
<div class="container">
  <div class="row">
    <div id="app" class="col-xs-12 col-sm-8 col-sm-push-2">
      <router-view/>
    </div>
  </div>
</div>
</template>


<script>
export default {
  name: 'app'
}
</script>

<style lang="scss" scoped="">
  #app {
    margin-top: 60px;
  }
</style>
