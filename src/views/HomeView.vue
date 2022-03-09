<template>
  <main>
    <section class="player">
      <h2 class="song-title" >{{ current.title }} - <span>{{ current.artist }}</span></h2>
      <div class="control">
        <button class="prev" @click="perv">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
      </div>
    </section>
    <section class="playlist">
      <h3>Your Playlist</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
        {{song.title}} - {{song.artist}}
      </button>
    </section>
    <section class="add-song">
      <form action="">
        <input type="file" class="file-upload" name="filename">
        <input type="submit" >
      </form>
    </section>
  </main>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  data(){
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Crows fly Black',
          artist: 'Tarot',
          src: require('../assets/01-tarot-crows_fly_black.mp3')
        },
        {
          title: 'Die Alive',
          artist: 'Tarja Turunen',
          src: require('../assets/08-tarja_turunen-die_alive-ser.mp3')
        },
        {
          title: 'Her Portrait In Black',
          artist: 'Atreyu',
          src: require('../assets/Atreyu - Her Portrait In Black (Underworld Evolution Soundtrack).mp3')
        },
        {
          title: 'Mirror Mirror',
          artist: 'Blind Guardian',
          src: require('../assets/Blind Guardian - Mirror Mirror.mp3')
        },
        {
          title: 'Don\'t say a word',
          artist: 'Sonata Arctica',
          src: require('../assets/Track05.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined"){
        this.current = song;

        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function(){
        this.index++;
        if(this.index > this.songs.length -1){
          this.index = 0;
        }
      }.bind(this));
      this.isPlaying = true;

    },

    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if(this.index > this.songs.length -1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
    perv(){
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;

  }
}
</script>

<style scoped>

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;

}


.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.control {
  display: flex;
  justify-content:center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button:hover {
  opacity:0.8;
}

.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #CC2E5D;
}

.next, .prev {
  font-size: 16px;
  font-weight: 200;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #CC2E5D;
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #FF5858;
}

.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
</style>
