<template>
  <swiper
  :breakpoints="swiperOptions.breakpoints"
  :modules="modules"
  :slides-per-view="8"
  navigation
  @swiper="onSwiper"
  @slideChange="onSlideChange">
    <swiper-slide @click="pick=i; modalopen();" v-for='(a,i) in movielist' :key='i'>
      <div class="poster">
        <div class="poster-img">
          <img :src='`https://www.themoviedb.org/t/p/w300${a.poster_path}`' alt="" style="width:100%">
        </div>
        <div class="poster-con">
          <h5>{{a.title}}</h5>     
          <span>{{a.release_date}}</span>
        </div>
      </div>
    </swiper-slide>
  </swiper>
          
  <MoviePopup @closeModal="modal--;" :modal="modal" :pick="pick" :movielist='movielist' />
</template>

<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation,} from 'swiper';
import MoviePopup from './modal/MoviePopup.vue'

import 'swiper/css';
import 'swiper/css/navigation';

export default {
  components:{
    Swiper,
    SwiperSlide,    
    MoviePopup : MoviePopup,
  },
  props : {
    swiperOptions : Object,
    movielist:Array
  },
  data (){
    return {
      modal : 0,
      pick : 0,
    }
  },
  methods:{
    modalopen(){
      this.modal=1;
    }
  },
  setup() {
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log('slide change');
    };
    return {
      onSwiper,
      onSlideChange,
      modules: [ Navigation ]
    };
  },
  mounted(){

  }}
</script>

<style>

</style>