<template>
  <article>
    <section v-for="(n, index) in pageOffset" :key="index">
      <img :src="'https://picsum.photos/400/400?image='+index" alt="">
      <p>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, 
        sed diam nonumy eirmod tempor invidunt ut labore et dolore 
        magna aliquyam erat, sed diam voluptua. At vero eos et accusam 
        et justo duo dolores et ea rebum.
      </p>
    </section>
    <footer>
      <div ref="infinitescrolltrigger" id="scoll-trigger"></div>
      <div class="circle-loader" v-if="showloader"></div>
    </footer>
  </article>
</template>

<script>
  export default {
    data: () => {
      return {
        currentPage: 1,
        maxPerPage: 2,
        totalResults: 100,
        showloader: false
      }
    },
    computed: {
      pageCount() {
        return Math.ceil(this.totalResults/this.maxPerPage);
      },
      pageOffset() {
        return this.maxPerPage * this.currentPage;
      }
    },
    methods: {
      scrollTrigger() {
        const observer = new IntersectionObserver((entries) => {
          entries.forEach(entry => {
            if(entry.intersectionRatio > 0 && this.currentPage < this.pageCount) {
              this.showloader = true;
              setTimeout(() => {
                this.currentPage += 1;
                this.showloader = false;
              }, 2000); // simulate Ajax-Call ;-)
            }
          });
        });

        observer.observe(this.$refs.infinitescrolltrigger);
      }
    },
    mounted() {
      this.scrollTrigger();
    }
  }
</script>

<style lang="scss" scoped>
  article {
    margin: 0 auto;
    width: 400px;

    section {
      width: 400px;
      margin-bottom: 20px;
      border-radius: 10px;
      background-color: #efefef;
      color: #04525A;
      overflow: hidden;

      p {
        margin: 0;
        padding: 10px 20px;
      }
    }

    footer {
      position: relative;
      width: 400px;
      height: 100px;

      #scroll-trigger {
        height: 50px;
      }

      .circle-loader {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: 5px solid rgba(255, 255, 255, .2);
        border-top: 5px solid #fff;
        animation: animate 1.5s infinite linear;
      }
    }
  }

  @keyframes animate {
    0% {
      transform: translate(-50%,-50%) rotate(0deg);
    }
    100% {
      transform: translate(-50%,-50%) rotate(360deg);
    }
  }
</style>

