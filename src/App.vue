<template>
  <div id="app">
    <transition name="alert">
      <span class="alert" v-if="$store.state.copiedColor">Color {{ $store.state.copiedColor }} copied to clipboard.</span>
    </transition>

    <ul class="flex">
        <palette v-for="(color,index) in $store.state.colors" :key="color" :index="index" :bcolor="$store.state.colors[index]"></palette>
    </ul> 

    <button class="btn-generate" @click="generatePalette()">Generate palette</button>

    <span class="des">Click button or enter for generate random color palette. <br> For copy hex color to clipboard click to palette.</span>


  </div>
</template>

<script>
import palette from './components/palette.vue'

export default {
  components: {
    palette
  },
  methods:{
    generateColor(){
      var hexKeys = "ABCDEF0123456789"
      var color = "#"
      for(var i = 0;i<6;i++){
        color += String(hexKeys[Math.floor(Math.random() * hexKeys.length)])
      }
      console.log(color);
      return color
    },
    generatePalette(){
      this.$store.state.colors = []
      for(var i = 0;i<5;i++){
        this.$store.state.colors.push(this.generateColor())
      }
    },
  },
  created(){
    this.generatePalette()
  },
  mounted(){
    window.addEventListener("keypress",(e) => {
      if(e.keyCode == 13){
        this.generatePalette()
      }
    })
  }
}
</script>

<style>

body{
  background-color:#d0d3d8;
}


ul{
  list-style: none;
}

.flex{
  display: flex;
  position: absolute;
  top: 37%;
  left: 50%;
  transform: translate(-50%,-50%);
}


.btn-generate{
  position: absolute;
  left: 50%;
  top: 80%;
  transform: translate(-50%,-50%);
  outline: none;
  border: 1px solid rgb(35, 0, 75);
  background-color: rgb(35, 0, 75);
  color: white;
  padding: 20px;
  border-radius: 30px;
  letter-spacing: 2px;
}


.des{
  padding: 10px;
  border-radius: 30px;
  background-color: white;
  position: absolute;
  left: 50%;
  top: 92%;
  transform: translate(-50%,-50%);
  outline: none;
  text-align: center;
  line-height: 23px;
}


.alert{
  transform: translate(-50%,-50%);
  text-align: center;
  width:25%;
  position: absolute;
  left: 50%;
  top: 7%;
  background-color: #0D2148;
  color: white;
  padding: 15px;
  border-radius: 30px;
}

.alert-enter{}
.alert-enter-active{animation: anim-in 0.5s ease-in-out forwards;}
.alert-leave{}
.alert-leave-active{animation: anim-out 0.5s ease-in-out forwards;}

@keyframes anim-in{
  from{
    top: 4%;
    opacity: 0;
  }
  to{
    top: 7%;
    opacity: 1;
  }
}


@keyframes anim-out{
  from{
    top: 7%;
    opacity: 1;
  }
  to{
    top: 4%;
    opacity: 0;
  }
}



</style>
