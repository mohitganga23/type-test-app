<template>
  <div class="container" v-if="showBtn">
  <div class="split left">
      <div class="centered">
        <img 
          src="./assets/4401280.jpg"/>
      </div>
    </div>

    <div class="split right">
      <div class="centered">
        <p id="title">Take a free typing test</p>
        <p id="desc">Type a short piece of text to find out how fast can you type. Test your typing speed in words per minute. </p> 
        <button class="button" @click="startTest">
        Take the Test!
        </button>
      </div>
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
  position: relative;
}


#title {
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 0;
}

#desc {
  margin: 4px 0 ;
  font-size: 18px;
  font-weight: 500;
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
  margin-top: 8px;
  vertical-align: middle; 
  text-decoration: none;
  display: inline-block;
  font-size: 24px;  
  border-radius: 30px;
}

.button:hover{
  cursor: pointer;
}

.split {
  height: 100%;
  width: 50%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
}

/* Control the left side */
.left {
  left: 0;
  background-color: #fff;
}

/* Control the right side */
.right {
  right: 0;
  background-color: #55c5ff;
}

/* If you want the content centered horizontally and vertically */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}

/* Style the image inside the centered container, if needed */
.centered img {
  width: 350px;
  border-radius: 50%;
}

</style>
