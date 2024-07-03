<template>
<div id="slideshow">
  <div class="page"
       v-for="item in pageContain"
       :style="style"
  >{{displayValue}}</div>
</div>
</template>
<script setup>
import {computed, ref} from "vue";
  const showIndex=ref(0)
  const displayValue=ref('')
  const pageContain=ref(5)
  fetch('https://v1.jinrishici.com/all.json').then(r=>r.json()).then(r=>{
    displayValue.value=r.content
  })
  const style=computed(()=>`left:${(showIndex.value)*100}%`)
  setInterval(()=>{
    fetch('https://v1.jinrishici.com/all.json').then(r=>r.json()).then(r=>{
      displayValue.value=r.content
    })
    showIndex.value>-pageContain.value+1?showIndex.value--:showIndex.value=0
  },3000)
</script>
<style>
body{
  padding: 0;
  margin: 0;
}
#app{
  width: 100vw;
  height: 100vh;
  #slideshow{
    width: inherit;
    height: inherit;
    display: flex;
    overflow:scroll;
    &::-webkit-scrollbar{
      height: 0;
      width: 0;
    }
    .page{
      position: relative;
      width: 100%;
      height: 100%;
      flex: 1 0 100%;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      font-size: 22px;
      transition: all 0.8s ease-in-out;
      background-image: url('./bgi.png');
      background-repeat: no-repeat;
      background-position: center;
    }
  }
}
</style>
