<template>
  <div id="app">
    <p>获取dom</p>
    <p>目标通过id和ref获取原生dom标签</p>
    <h1 id="h" ref="myH1">我是孤独的h1</h1>
    <p>获取组件对象</p>
    <Demo ref="de"></Demo>

    <h1>点击改data 获取原生内容</h1>
    <p ref ='a'>{{count}}</p>
    <button @click="btn">点击加一观察内容</button>


    <h1>nextTick使用场景</h1>
    <input type="text" ref="myinp" v-if="show">
    <button v-else @click="btn1">点击变成输入框</button>
    <ComeHa :list="list"></ComeHa>
  </div>
</template>

<script>
import Demo from './components/Demo.vue'
import Com from './components/COMEHa.vue'
export default {
  data() {
    return {
      count:0,
      show:false,
      list: [
        {
          goods_count:1,
          goods_img:'http://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          goods_name:'以每日hiash卡是开发合肥市返回话费卡沙发客服',
          goods_price:108,
          goods_state:true,
          id:1
        
        },
        {
          goods_count:1,
          goods_img:'http://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          goods_name:'以每日hiash卡是开发合肥市l返回话费卡硕大的见哦按讲道理沙发客服',
          goods_price:158,
          goods_state:true,
          id:2
        
        },
        {
          goods_count:1,
          goods_img:'http://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          goods_name:'以每日hiash卡是开发合肥市啥的卡号地块返回话费卡沙发客服',
          goods_price:138,
          goods_state:true,
          id:3
        
        },
        {
          goods_count:1,
          goods_img:'http://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          goods_name:'以每日hiash卡是开发合肥市返回话费卡沙发客服',
          goods_price:158,
          goods_state:true,
          id:4
        
        },
        {
          goods_count:1,
          goods_img:'http://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          goods_name:'以每日hiash卡是开发合肥的哈利开始导航卡申卡电话卡市返回话费卡沙发客服',
          goods_price:10,
          goods_state:true,
          id:5
        
        }]
    }
  },
mounted(){
  let h=document.querySelector('#h')
  console.log(h);
  console.log( this.$refs.myH1);
  console.log( this.$refs.de.fn());
 
},
components:{
  Demo,
  [Com.name]:Com
},
methods:{
  btn(){
    this.count++;//vue检测数据更新,开启一个Dom更新队列(异步任务)不会立即更新dom
    console.log(this.$refs.a.innerHTML); //所有获得的是更新前的值
    //方法一可以在updated中获取
    // 解决方案二
    this.$nextTick(()=>{
      console.log(this.$refs.a.innerHTML);//能拿到更新后的
    })
  },
     btn1(){
    this.show=true
    //显示输入框后获取焦点
    // this.$refs.myinp.focus()  //报错原因data变换更新是异步的 input还没有挂载到真实dom无法获取没有这个方法
    this.$nextTick(()=>{
      this.$refs.myinp.focus() 
    })
  }
}
}
</script>

<style>

</style>