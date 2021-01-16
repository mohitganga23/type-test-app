<template>
  <div class="container" v-if="showBtn">
    <div class="center">
      <p id="title">Take a free typing test</p>
      <p id="desc">Type a short piece of text to find out how fast can you type. Test your typing speed in words per minute. </p> 
      <p id="subtext">The test will take only 2-3 minutes! You can practice as much as necessary because you have no limits.</p>
      <button class="button" @click="startTest">Take the test !</button> 
    </div>     
  </div>  
  <div v-if="isActive">
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home,
  },
  data() {
    return {
      isActive: false,
      showBtn: true  
    }
  },
  methods:{
    startTest(){
      this.isActive = true;
      this.showBtn = false;
    }
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;500;900&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

.container{
  height: 200px;
  position: relative;
}

.center {
  margin: 0;
  position: absolute;
  top: 120%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}

#title {
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 0;
}

#desc {
  margin: 8px 0 ;
  font-size: 24px;
  font-weight: 500;
}

#subtext {
  font-size: 18px;
  font-style: italic;
  margin-top: 0;
}

p{
  font-family: 'Red Hat Display', sans-serif;
  color: white;
}

.button {
  font-family: 'Red Hat Display', sans-serif;
  font-weight: 700;
  background-color: white;
  border: 4px;
  color: #55c5ff;
  padding: 15px 32px;
  text-align: center;
  vertical-align: middle; 
  text-decoration: none;
  display: inline-block;
  font-size: 24px;
  border-radius: 30px;
}

.button:hover{
  cursor: pointer;
  
}

</style>
