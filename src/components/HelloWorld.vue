<script setup lang="ts">
import 'simple-keyboard/build/css/index.css';
import axios from 'axios';
import { ref } from "vue";
defineProps<{
  msg: string;
}>();
const myscreen  = ref(null);
function mouseDown(ev) {
  console.log("hello")
  console.log("click img left=",ev.clientX);
	console.log("click img top=",ev.clientY);
  var scale =2 ;
  var myJSObject={"x":ev.clientX*scale,"y":ev.clientY*scale}

  axios.post('http://192.168.1.12:5050/api/click',myJSObject).then(resp => {

    console.log(resp.data);
    
  });
};
  function mouseMove(ev) {
    console.log(myscreen);
    console.log("offset x",myscreen.offsetLeft)
    console.log(ev.target.getBoundingClientRect())
   // const left = myscreen.getBoundingClientRect().left
   // const top =  myscreen.getBoundingClientRect().top
   // console.log("left=",left);
   // console.log("top=",top);

  console.log("hello move")
  console.log("click img left=",ev.clientX);
	console.log("click img top=",ev.clientY);
  var mousex = ev.clientX;
  var mousey = ev.clientY;
  console.log("hello screen")
  console.log("screen left=",mousex);
	console.log("screen top=",mousey);
  var myJSObject={"x":mousex,"y":mousey}

  axios.post('http://192.168.1.12:5050/api/move',myJSObject).then(resp => {

    console.log(resp.data);
    
  });


}
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
      What's next?
    </h3>
    <img
      id="bg" 
      ref="myscreen"
      @mousedown="mouseDown"
      @mousemove="mouseMove"
      src="http://192.168.1.17:7777"
      width="960"
      height="540"
    />
    <input
      type="text"
      :value="value"
      @input="handleInput($event.target.value)"
    />
    <button @click="keyinput">ShowKeyboard.</button>
    <input class="input" />
  <div class="simple-keyboard"></div>


  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
