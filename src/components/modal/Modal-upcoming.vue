<template>
  <div class="modal-full" v-if="modal == 1">
    <div class="modal-area">
      <div class="modal-bg" :style="{ backgroundImage: `url(${imageurl(poster2[pick].backdrop_path)})`}"></div>
      <div class="modal-cnt">
        <div class="modal-img">
          <img :src='imageurl(poster2[pick].poster_path)' alt="" style="">
        </div>
        <div class="modal-text">
          <h1 class="modal-movie-tit">{{poster2[pick].title}}</h1>     
          <p class="modal-movie-date">{{poster2[pick].release_date }}</p>     
          <p class="overview" :class="{short : full}" @click="more">{{poster2[pick].overview}}</p>     
        </div>
        <iframe id="ytplayer" type="text/html" :src='youtubeurl(poster2[pick].id)' frameborder="0"></iframe>
      </div>      
      <button class="close-btn" @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { gsap } from 'gsap';    
export default {
  props : {
    poster2: Array,
    modal : Number,
    pick : Number,
  },
  data () {
    return{
      full : true,
      movieKey :''
    }
  },
  methods:{
    more() {
      this.full = !this.full
    },

    imageurl(img) {
      return `https://www.themoviedb.org/t/p/w300${img}`
    },

    youtubeurl(movieId) {
        axios.get(`https://api.themoviedb.org/3/movie/${movieId}/videos?api_key=eee59ded3d3f9fb38792c3a4c12362a5`)
        .then (결과 => {
          this.movieKey = 결과.data.results[0].key
          // console.log('영화 id : '+movieId, ', 영화 key : '+this.movieKey);
        })

      return `https://www.youtube.com/embed/${this.movieKey}?autoplay=1&origin=http://example.com`
    }
  },

  mounted(){
    gsap.to('.modal-movie-tit', {duration:0.3, opacity:0.5})    
  },
  }
</script>

<style>

</style>