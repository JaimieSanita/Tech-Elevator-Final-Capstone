<template>
  <nav class="panel is-primary is-pulled-right"> 
  <p class="panel-heading">
    Exercise History
  <p class="panel-tabs">
    <a>Name</a>
    <a>Date Assigned</a>
    <a>Length</a>
    <a>Description</a>
    <a>Calories Burned</a>
    <a>Use Equipment</a>
  </p>
  <a class="panel-block is-active">
    <span class="panel-icon">
      <i class="fas fa-running" aria-hidden="true"></i>
    </span>
    Ran  02/02/2020   10min   went running  12  false
  </a>
  
</nav>
</template>

<script>
export default {
  name:"exercise-history",

}
</script>

<style>
.panel{
resize: both;
width: 100%;
padding: 1px;

}

</style>