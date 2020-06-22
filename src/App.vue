<template>
  <div id="app">
    <header>
      <h1>32 Player</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
        {{current.title}}
        -
        <span>{{current.artist}}</span>
        </h2>
        <div class="control">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src==current.src) ? 'song playing' :'song'">
        {{song.title}} - {{song.artist}}

        </button>
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      current:{
        
      },
      index:0,
      isPlaying: false,
      songs:[
        {
        title:'Youngblood',
        artist:'5 Seconds Of Summer',
        src: require('./assets/songs/5 Seconds Of Summer - Youngblood (Lyrics Lyric Video).mp3')
      },
       {
        title:'Invincible',
        artist:'DEAF KEV',
        src: require('./assets/songs/DEAF KEV - Invincible NCS Release.mp3')
      },
      {
        title:'Time (Alan Walker Remix)',
        artist:'Hans Zimmer',
        src: require('./assets/songs/Hans Zimmer - Time (Alan Walker Remix).mp3')
      }
      
      ],
      player: new Audio()
    }
  },

  created(){
    this.current= this.songs[this.index];
    this.player.src=this.current.src;
  },

  methods:{
    play(song){
      if(typeof song.src != "undefined"){
        this.current = song;
        this.player.src= this.current.src;
      }

      this.player.play();
      this.player.addEventListener('ended', function(){
        this.index++;
        if(this.index > this.songs.length-1){
        this.index=0;
        }
        this.current= this.songs[this.index];
        this.play(this.current)

      }.bind(this));
      this.isPlaying= true;
    },
    pause(){
      this.player.pause();
      this.isPlaying=false;
    },

    next(){
      this.index++;
      if(this.index > this.songs.length-1){
        this.index=0;
      }
      this.current= this.songs[this.index];
      this.play(this.current)
    },

    prev(){
      this.index-- ;
      if(this.index < 0){
        this.index=this.songs.length-1;
      }
      this.current= this.songs[this.index];
      this.play(this.current)
      
    }
  }
}
</script>

<style>
 *{
   margin:0;
   padding:0;
   box-sizing:border-box;
   
 }

 body{
   font-family:sans-serif;
 }

 header{
   display:flex;
   justify-content:center;
   align-items:center;
   padding:15px;
   text-align:center;
   background-color:#212121;
   color:#fff;
 }

 
 main{
   width:100%;
   max-width:768px;
   margin: 0 auto;
 }

 .song-title{
   color:#53565A;
   font-size:32px;
   font-weight:700;
   text-transform:uppercase;
   text-align:center
 }

 .song-title span{
   font-weight:400;
   font-style:italic
 }

 .control{
   display:flex;
   justify-content:center;
   padding:30px 15px;


 }

 button{
   appearance:none;
   background:none;
   border:none;
   outline:none;
   cursor:pointer;
  
 }

 .play{
   font-size:20px;
   font-weight:700;
   padding:15px 25px;
   margin:0px 15px; 
   border-radius:10px;
   color:#FFF;
   background-color:#CC2E5D
 }
 .pause{
   font-size:20px;
   font-weight:700;
   padding:15px 25px;
   margin:0px 15px; 
   border-radius:10px;
   color:#FFF;
   background-color:#CC2E5D
 }

 .playlist{
   padding:5px;
   background-color:#53565A;
   color:#FFF;
 }

 .playlist h3{
   
   font-size:28px;
   font-weight:400;
   margin-bottom:32px;
   text-align:center;
 }

.playlist .song{
  color:#FFF;
  display:block;
  width:100%;
  padding:15px;
  font-size:20px;
  font-weight:600;
  cursor:pointer;
}

.playlist .song:hover{
  opacity:70%;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}

.playlist .song.playing{
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
 

</style>
