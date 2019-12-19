<template>
  <div class="demo">
    <header></header>
    <nav :class=" searchBarFixed === true ? 'isFixed' : '' "></nav>
    <main :class=" searchBarFixed === true ? 'mainFixed' : '' ">
      <p @click="isshow">点击按钮</p>
      <div class=""></div>
      <div :class="['ishide', canshow ? 'showit' : 'closeit']">
        <!-- 一大堆话展示，到时候真正做的时候，把它移出屏幕至负数 -->
      </div>
      <div class="testDrag" @mousedown="dragDiv" @mousemove="toMove"
       @mouseup="closeDrag" ref="drag"></div>
    </main>
    <footer></footer>
  </div>
</template>

<script>
export default {
  components: {
    // stickySlot,
  },
  data() {
    return {
      searchBarFixed: false,
      canshow: false,
      canMove: false,
      x: 0,
      y: 0,
      l: 0,
      t: 0,
      // headerData: [],
      // footerData: [],
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    aaa() {
      // console.log('q、qq');
    },
    isshow() {
      this.canshow = !this.canshow;
    },
    dragDiv(e) {
      this.canMove = true;
      // 获取x坐标和y坐标
      this.x = e.clientX;
      this.y = e.clientY;

      // 获取左部和顶部的偏移量
      this.l = this.$refs.drag.offsetLeft;
      this.t = this.$refs.drag.offsetTop;
    },
    toMove(e) {
      if (this.canMove) {
        // 获取x和y
        const nx = e.clientX;
        const ny = e.clientY;
        // 计算移动后的左偏移量和顶部的偏移量
        const nl = nx - (this.x - this.l);
        const nt = ny - (this.y - this.t);

        this.$refs.drag.style.left = `${nl}px`;
        this.$refs.drag.style.top = `${nt}px`;
      }
    },
    closeDrag() {
      this.canMove = false;
      // this.$refs.drag[0].unbind('mousemove', this.dragDiv);
    },
    handleScroll() {
      this.$nextTick(() => {
        const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
        // const offsetTop = document.querySelector('nav').offsetTop;
        if (scrollTop >= 200) {
          this.searchBarFixed = true;
        } else {
          this.searchBarFixed = false;
        }
      });
    },
  },
};

</script>

<style>
  .demo {
    overflow: auto;
    position: relative;
  }
  header {
    width: 100%;
    height: 200px;
    background-color: rgb(99, 124, 65);
  }
  nav {
    width: 100%;
    height: 100px;
    background-color: aqua;
  }
  p {
    margin: 0px;
    padding-top: 100px;
    background-color: brown;
  }
  main {
    width: 100%;
    height: 1500px;
    background-color: blue;
    position: relative;
  }
  .mainFixed {
    margin-top: 100px;
  }
  footer {
    width: 100%;
    height: 500px;
    background-color: rgb(255, 102, 0);
  }
  .isFixed{
    position:fixed;
    top:0;
    left:0;
    width:100%;
    z-index:999;
  }
  .ishide {
    background-color: rgb(187, 30, 140);
    width: 100px;
    height: 100px;
    position: absolute;
    left: 0px;
    top: 200px;
    opacity: 0;
    transition: opacity .5s, left .5s;
    transition-timing-function: cubic-bezier(.23,1.48,.97,1.2);
  }
  .showit {
    left: 200px;
    opacity: 1;
  }
  .testDrag {
    width: 170px;
    height: 170px;
    background-color: rgb(42, 165, 58);
    top: 700px;
    left: 75px;
    position: absolute;
  }
  /* .closeit {
    display: none;
    animation: myanimation .5s;
  } */
  /* @keyframes myanimation {
    from {
      display: block;
    }
    to {
      display: none;
    }
  } */
</style>
