<template>
  <div class="header">
    <div class="banner-container">
      

      <marquee behavior="scroll" direction="left" class="banner-title">Never forget, you're always elevating!</marquee>
    </div>
    <div class="hello-container">
      <img class="logo-image" src="../assets/logo.png" />
      <h1 class="title" style="position:relative; left:180px">
        Welcome to {{ this.$store.state.profile.firstName }}'s Tech Wellovater!
      </h1>
      <div style="position: relative; left: 700px; top:36px; font-size:24px" id="nav">
        <router-link
          id="link"
          v-bind:to="{ name: 'logout' }"
          v-if="$store.state.token != ''"
          >Logout</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "te-header",
};
</script>

<style scoped>
.banner-container {
  background-color: #8cc63f;
  color: white;
  display: flex;
  justify-content: center;
}
.hello-container {
  background-color: #00adee;
  display: flex;
  justify-content: flex-start;
font-family: proxima-nova;
  height: 90px;
  margin-top: 10px;
  margin-bottom: 10px;
  
}
h1 {
  color: white;
  display: flex;
  padding: 30px;
  position: relative;
  padding-left: 24%;
}

#nav {
  justify-content: left !important;
}
#link {
  color: white;
}
</style>