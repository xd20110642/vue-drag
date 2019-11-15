<template>
  <div class="hello">
    <div class="drag-field"
     @dragover.prevent
     @drop.stop="dropBox"
    >
        <div class="item"
          v-for="(item,index) of items"
          :key="item"
          draggable="true"
          @dragover.prevent
          @dragstart="dragstart($event,index)"
          @dragend="dragend"
          @drop.stop="drop($event,index)"
        >
          {{item}}
        </div>
    </div>
    <!-- 第二部分 -->
  <div class="drag-field"
     @dragover.prevent
     @drop.stop="dropBox2"
    >
        <div class="item"
          v-for="(item,index) of items2"
          :key="item"
          draggable="true"
          @dragover.prevent
          @dragstart="dragstart($event,index)"
          @dragend="dragend"
          @drop.stop="drop2($event,index)"
        >
          {{item}}
        </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'dragGroup',
  props: {
    it: {
      type: Array,
      default: () => [5,6,10]
    },

  },
  data() {
    return {
      items:this.it,
      items2:[7,8,9]
    }
  },
  methods:{
    //   第一个盒子 第二块进入
    dropBox(){
      console.log("父盒子拖拽");
         let index=event.dataTransfer.getData('index');
         let temp=this.items2.splice(index,1);//截取被移动的元素
          this.items.push(...temp);
      },
    //   第二个盒子 显示的是第一块进入
      dropBox2(){
        console.log("父盒子拖拽2");
         let index=event.dataTransfer.getData('index');
         let temp=this.items.splice(index,1);//截取被移动的元素
          this.items2.push(...temp);
      },
    dragstart(event,index){
        event.dataTransfer.setData('index',index)
    },
    drop(event,index) {
      event.preventDefault();
      let ind=event.dataTransfer.getData('index');//获取到是移动的第几个
      let temp=this.items.concat([]);
      let xd=temp.splice(ind,1);//截取被移动的元素
      temp.splice(index,0,xd[0]);//插入指定位置元素
      this.items=temp;
      console.log('位置',index,'移动的第几个',ind,'items',this.items,'截取',xd)
    },
     drop2(event,index) {
      event.preventDefault();
      let ind=event.dataTransfer.getData('index');//获取到是移动的第几个
      let temp=this.items2.concat([]);
      let xd=temp.splice(ind,1);//截取被移动的元素
      temp.splice(index,0,xd[0]);//插入指定位置元素
      this.items2=temp;
      console.log('位置',index,'移动的第几个',ind,'items',this.items2,'截取',xd)
    },
    dragend(){
        event.dataTransfer.clearData()
    },
    dragend(){
        event.dataTransfer.clearData()
    }
  },
}
</script>

<style scoped>
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
