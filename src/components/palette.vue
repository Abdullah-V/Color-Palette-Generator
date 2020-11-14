<template>
  <li class="palette" @click="copyHex()">
    <input type="text" v-model="bcolor" class="input">
    <a href="#">
      <span class="color" :style="{backgroundColor:bcolor}"></span>
      <span class="colorText">{{ bcolor }}</span>
    </a>

  </li>
</template>

<script>
export default {
  props:["bcolor","index"],
  data(){
    return {
      tout:"",
    }
  },
  methods:{
    copyHex(){
      clearTimeout(this.tout)
      // this.$store.state.copiedColor = ""
      var copyText = document.querySelectorAll(".input")[this.index]
      copyText.select();
      copyText.setSelectionRange(0, 99999); 
      document.execCommand("copy");
      this.$store.state.copiedColor = copyText.value
      this.tout = setTimeout(() => {
        this.$store.state.copiedColor = ""
      }, 2000);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>




.palette:hover{
  transform: translateY(-17px);
  -webkit-box-shadow: 0px 5px 8px 0px rgba(71,71,71,1);
  -moz-box-shadow: 0px 5px 8px 0px rgba(71,71,71,1);
  box-shadow: 0px 5px 8px 0px rgba(71,71,71,1);
}


.palette{
  transition: 0.2s all;
  border-radius: 15px;
  width: 200px;
  height: 300px;
  margin: 20px;
  background-color: white;
}

.color{
  width: 100%;
  height: 230px;
  border-radius: 10px;
}

.colorText{
  text-align: center;
  padding: 16px;
}

a{
  display: flex;
  flex-direction: column;
  padding: 10px;
  text-decoration: none;
  color: black;
  font-size: 18px;
}


.input{
  position: absolute;
  opacity: 0;
}





</style>
