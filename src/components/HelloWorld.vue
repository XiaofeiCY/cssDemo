<template>
  <div class="demo">
    <header></header>
    <nav :class=" searchBarFixed === true ? 'isFixed' : '' "></nav>
    <main :class=" searchBarFixed === true ? 'mainFixed' : '' ">
      <p @click="isshow">点击按钮</p>
      <div class=""></div>
      <div :class="['ishide', canshow ? 'showit' : 'closeit']" @click="aaa">
        一大堆话展示
      </div>
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
    left: 200px;
    top: 200px;
    opacity: 0;
    transition: opacity 1s;
  }
  .showit {
    opacity: 1;
  }
  .closeit {
    /* display: none; */
    /* animation: myanimation .5s; */
  }
  /* @keyframes myanimation {
    from {
      display: block;
    }
    to {
      display: none;
    }
  } */
</style>
