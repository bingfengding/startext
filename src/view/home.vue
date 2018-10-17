<template>
  <div id="home">
     <ul id="menu">
          <li data-menuanchor="page1"><a href="javascript:void(0)" @click="$refs.fullpage.api.moveTo(1)">Section 1</a></li>
          <li data-menuanchor="page2"><a href="javascript:void(0)" @click="$refs.fullpage.api.moveTo(2)">Section 2</a></li>
          <li data-menuanchor="page3"><a href="javascript:void(0)" @click="$refs.fullpage.api.moveTo(3)">Section 3</a></li>
          <li data-menuanchor="page4"><a href="javascript:void(0)" @click="$refs.fullpage.api.moveTo(4)">Section 3</a></li>
        </ul>
     <full-page :options="options1" id="fullpage" ref="fullpage">
      
    <div class="page pageBox1 section">
      <div class="center">
      <swiper :options="swiperOption1" ref="mySwiper1" id="swiper1">
        <swiper-slide v-for="(item,index) in list" :key="index">
          <transition name="slide-fade">
            <p :style="'scale(1.17075, 1.17075);opacity:'+ (1-Math.abs(isActive-index)*0.3)+'; transform: matrix('+(1-0.1*index+isActive*0.1)+',0,0,'+(1-0.1*index+isActive*0.1)+', 0, 0) translate(0,'+(isActive?(index-isActive)*50:0)+'%) scale('+(1+0.1*(isActive-index))+', '+(1+0.1*(isActive-index))+')'" :class="index===isActive?'bold':''">{{item.value}}</p>
          </transition>
        </swiper-slide>
      </swiper>
    </div>
    </div>
    <div class="page pageBox2 section">
      <p class="part part2">
        vue-fullpage2
      </p>
    </div>
    <div class="page pageBox3 section">
      <p class="part part3" >
        vue-fullpage3
      </p>
    </div>
    <div class="page pageBox4 section">
      <p class="part part4">
        vue-fullpage4
      </p>
    </div>
     </full-page>
   
    
  </div>
</template>
<script>
import { swiper, swiperSlide } from "vue-awesome-swiper"

export default {
  data(){
    return{
      ifBottomBl:true,
      options1:{
        licenseKey:"OPEN-SOURCE-GPLV3-LICENSE",
        continuousVertical:false,
        afterLoad: this.afterLoad,
        scrollBar: false,
        sectionsColor: ['#41b883', '#ff5f45', '#0798ec', '#fec401', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab'],
        //anchors: ['page1', 'page2', 'page3', 'page4'],
        menu: '#menu',
       // normalScrollElements:"#swiper1"
      },
      isActive:0,
      list:[
        {
          value:"我是一段很长 的文字，不知道东西"
        },{
          value:"我是一段很长字，具体哈哈哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，具体哈哈哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，具体，不什么东西"
        },{
          value:"我是一段很哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，哈哈哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，具，不什么东西"
        },{
          value:"我是一段很长不知么东西"
        },{
          value:"我是一段很长 的文哈哈，是什么东西"
        },{
          value:"我是一段很长 的文具体哈哈哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，，不什么东西"
        },{
          value:"我是一段很长 的文哈哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字哈哈，不什么东西"
        },{
          value:"我是一段很长 的文字，具体哈哈哈哈哈道是什么东西"
        },{
          value:"我是一段很长 的文字哈哈哈哈哈，是什么东西"
        },{}
      ],
      swiperOption1:{
        direction:"vertical",
        mousewheel: true,  
        centeredSlides:true,
        slidesPerView:11,
        // freeMode:true,
        // freeModeMomentum : true,
        height:700,
        roundLengths:true,
        on: { 
          slideChangeTransitionStart: ()=>{
            this.isActive = this.swiper1.activeIndex;//切换结束时，告诉我现在是第几个slide
            console.log(this.isActive)
          },
          reachEnd : ()=>{
           
          },
          progress:(progress)=>{
           
            if(progress==1){
           
            this.$refs.fullpage.api.setAllowScrolling(true,'down')
            } else if(progress){
              this.$refs.fullpage.api.setAllowScrolling(false,'down')
            }
          }
        }
      },
    }
  },
  computed:{
    swiper1() {
      return this.$refs.mySwiper1.swiper
      },

  },
  mounted() {
    this.$refs.fullpage.api.setAllowScrolling(false,'down')
  },
  created() {
    
  },
  methods:{
    afterLoad(origin,destination,direction){
      console.log(origin,destination,direction)
    }
  },
  
  components: {
    swiper,
    swiperSlide,
  
  }
}
</script>
<style lang="stylus" scoped>
#home
  text-align center
  .page-container 
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    .pageBox1
      display flex
      justify-content center
      padding-top 100px
      .center
        width 1800px
        height 700px
        overflow hidden
        .swiper-slide
          transform:translate3d(0,0,0)
  #menu
    background-color #cccccc
    position fixed
    top 0
    height 100px
    z-index 100
    width 100%
    li
      display inline-block
      margin 0 20px
      line-height 90px
      cursor pointer
</style>
<style lang="stylus">
#home
  .slide-fade-enter-active 
    transition: all .3s ease;
  .slide-fade-leave-active 
    transition: all .3s ease;
  .swiper-slide
    p
      height 70px
      line-height 70px
      font-size 40px
      transition: all .3s ease;
</style>

