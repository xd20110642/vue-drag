<template>
  <div id="app">
    <div class="hello">
      <drag :it="items"></drag>
      <dragGroup></dragGroup>
    </div>
  </div>
</template>

<script>
import drag from './components/drag.vue'
import dragGroup from './components/dragGroup.vue'

export default {
  name: 'app',
  data() {
    return {
      items:[1,2,3],
      items2:[4,5,6]
    }
  },
  methods:{
    par(index){
        console.log('')
    }
  },
  components:{
    drag,
    dragGroup
  }
}
</script>

<style>
 .drag-field,.drop-field{
        height: 10rem;
        box-sizing: border-box;
        padding: 1rem;
        background-color: #eee;
        margin-top: 1rem;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    .item{
        width: 30%;
        height: 3rem;
        text-align: center;
        line-height: 3rem;
        font-size: .9rem;
        background-color: royalblue;
        color: #eee;
    }
    .item:hover{
        cursor: pointer;
    }
</style>
