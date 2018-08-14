<template>
  <div class="container">

    <v-touch v-on:swipeleft="onSwipeLeft" v-on:tap="onSwipeTap" v-on:swiperight="onSwipeRight" class="content" :style="styleobj"></v-touch>
  </div>
</template>
<script>
import Vue from 'vue'
import VueTouch from 'vue-touch'
Vue.use(VueTouch, {name: 'v-touch'})
export default {
  data(){
    return{
      imgid:this.$route.params.id+1

    }
  },
  created () {
    this.$emit('routerEmit', 'photo');

    if(!this.$route.params.id){
        this.$router.push("/photo/photo")
    }

  },
  computed:{
    styleobj(){
      return {background:`#000 url('./img/${this.imgid}.jpg') no-repeat center/contain`}
    }
    
  },
  methods:{
    onSwipeRight(){
      console.log('right');
        this.imgid--;
      if(this.imgid<1){
          this.imgid=16;
      }
    },
    onSwipeLeft(){
      console.log('left');
        this.imgid++;
        if(this.imgid>16){
           this.imgid=1;
        }
    },
    onSwipeTap(){
      console.log('tap');
        this.$router.go(-1);
    }
  }
}
</script>
<style scoped>
.content{
    
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    z-index: -1;
  }
</style>

