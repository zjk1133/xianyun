<template>
<div style="padding:50px">
    <div class="header">
        <span
        v-for=" (item,index) in ['ww','dd','ss'] "
        :key="index"
        :class="{aa:current===index}"
        @click="handle(index)"
        > {{item}} </span>
    </div>
    <div v-if="current === 0">
           <ul>
               <li>为什么黄飞鸿来广州都带伞？</li>
               <li>为什么黄飞鸿来广州都带伞？</li>
               <li>为什么黄飞鸿来广州都带伞？</li>
           </ul>
       </div>

       <div  v-if="current === 1">
           <ul>
               <li>猛龙总冠军</li>
               <li>猛龙总冠军</li>
               <li>猛龙总冠军</li>
           </ul>
       </div>

       <div  v-if="current === 2">
           <ul>
               <li>伊朗同学可能击败什么无人机</li>
               <li>伊朗同学可能击败什么无人机</li>
               <li>伊朗同学可能击败什么无人机</li>
           </ul>
       </div>
</div>
    
</template>

<script>
export default {
    data () {
        return {
            current:0
        }
    },
    methods: {
        handle(index){
            this.current=index
        }
    }
}
</script>

<style scoped>
.header span{
    cursor: pointer;
}
.header .aa{
    color: tomato
}
</style>

