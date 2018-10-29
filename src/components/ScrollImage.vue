<template>
    <div class="scroll-img" v-on:mouseover="stopScroll()" v-on:mouseout="moveScroll()"> 
        <div class="img-content">
            <!-- 图片 -->
            <transition-group tag="ul" :name="animationName">
                <li class="img-list-li" v-for="(item,index) in imgList" 
                v-show="index == showIndex" :key="index" @click="chooseThisImage(index)">
                    <img :src="item.img" alt="">
                </li>
            </transition-group>
            <!-- 计数点 -->
            <ul class="pageControl">
                <li class="page" v-for="(item,index) in this.imgList" :key="index"
                :class="{'active':index == showIndex}" @click="changePage(index)">
                </li>
            </ul>
            <!-- 左右切换图片button -->
            <div class="change-btn-li-left" @click="changeScroll(-1)" v-show="isShowChangeBtn">
                <div class="triangle-back-left"></div>
            </div>
            <div class="change-btn-li-right" @click="changeScroll(1)" v-show="isShowChangeBtn">
                <div class="triangle-back-right"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "ScrollImage",
  props: {
    imgList: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      // 记录展示的第页码
      showIndex: 0,
      // 是否显示切换按钮
      isShowChangeBtn: false,
      // 滚动方向
      animationName: "right",
      // 时间间隔
      timeInterval: 2500
    };
  },
  directives:{
      focus:{
          inserted(el){
              el.focus();
          }
      }
  },
  methods: {
      
    // 增加showIndex
    play() {
      this.showIndex++;
      if (this.showIndex === this.imgList.length) {
        this.showIndex = 0;
      }
    },
    // 开始滚动
    playScroll() {
        
      if (this.timer) {
        window.clearInterval(this.timer);
        this.timer = null;
      }
      this.timer = window.setInterval(this.play, this.timeInterval);
    },
    // 停止滚动 当鼠标移入
    stopScroll() {
      this.isShowChangeBtn = true;
      clearInterval(this.timer);
      this.timer = null;
    },
    // 开始继续滚动 当鼠标移出
    moveScroll() {
      this.animationName = "right";
      this.isShowChangeBtn = false;
      this.playScroll();
    },
    // 点击pagecontrol选择某一页
    changePage(index) {
      this.showIndex = index;
    },
    // 左右button
    changeScroll(page) {
      this.animationName = page == -1 ? "left" : "right";
      this.showIndex += page;
      if (this.showIndex === this.imgList.length) {
        this.showIndex = 0;
      }
      if (this.showIndex === -1) {
        this.showIndex = this.imgList.length - 1;
      }
    },
    // 选择该张图片进入详情
    chooseThisImage(index){
        console.log(index);
        
    },
    
  },
  created() {
    this.playScroll();
  }
};
</script>

<style scoped>
.scroll-img,
.img-content {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  margin: 0 auto;
}
/* 以下是轮播图片 */
ul {
  list-style: none;
  padding: 0px;
  display: flex;
  position: absolute;
}
.img-list-li {
  position: absolute;
}
.left-enter-active,
.right-enter-active {
  transform: translateX(0);
  transition: all 0.6s ease;
}
.left-leave-active {
  transform: translateX(100%);
  transition: all 0.6s ease;
}
.left-enter {
  transform: translateX(-100%);
}
.left-leave,
.right-leave {
  transform: translateX(0);
}
.right-leave-active {
  transform: translateX(-100%);
  transition: all 0.6s ease;
}
.right-enter {
  transform: translateX(100%);
}
/* 以下是分页圆点 */
.pageControl {
  position: absolute;
  list-style: none;
  padding: 2px;
  margin: 0 auto;
  border-radius: 6px;
  left: 50%;
  margin-left: -30px;
  bottom: 10px;
  text-align: center;
  z-index: 20;
  background-color: rgb(0, 0, 0, 0.2);
}
.page {
  margin: 0 2px;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: #fff;
}
.active {
  background-color: #f40 !important;
}
/* 以下是切换按钮 */
.change-btn-li-left {
  /* float: left; */
  position: absolute;
  top: 45%;
  left: 10px;
  background-color: rgb(0, 0, 0, 0.3);
  border-radius: 20px;
  width: 40px;
  height: 40px;
}
.triangle-back-left {
  margin-top: 5px;
  margin-left: 5px;
  width: 30px;
  height: 30px;
  background: url(../assets/img/left.png) no-repeat;
  background-size: 30px;
}
.change-btn-li-right {
  position: absolute;
  top: 45%;
  right: 10px;
  background-color: rgb(0, 0, 0, 0.3);
  border-radius: 20px;
  width: 40px;
  height: 40px;
}
.triangle-back-right {
  margin-top: 5px;
  margin-left: 5px;
  width: 30px;
  height: 30px;
  background: url(../assets/img/right.png) no-repeat;
  background-size: 30px;
}
</style>
