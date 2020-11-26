<template>
  <div id="app">
    <header>
      <h1>Spotify</h1>
    </header>
    <main>
      <!-- Debut de la section Player -->
      <div class="container bg-succes">
        <section class="player">
          <div class="card-header bg-white">
            <h2 class="song-title">
              {{ current.title }} - <span>{{ current.artist }}</span>
            </h2>
          </div>

          <div class="controls card-body bg-dark">
            <button class="prev btn btn-success" @click="prev">
              Précedent
            </button>
            <button
              class="play btn btn-primary"
              v-if="!isPlaying"
              @click="play"
            >
              Play
            </button>
            <button class="pause btn btn-primary" v-else @click="pause">
              Pause
            </button>
            <button class="next btn btn-success" @click="next">Suivant</button>
          </div>
        </section>
      </div>
      <!-- Fin de la section Player -->

      <!-- Debut de la section Playlist  -->
      <div class="container">
        <section class="playlist">
          <div class="card-header bg-secondary text-light">
            <h3>Playlist</h3>
          </div>
          <div class="card-body bg-dark">
            <button
              v-for="song in songs"
              :key="song.src"
              @click="play(song)"
              class="(song.src == current.src) ? 'song playing' : 'song'"
            >
              <div class="card">
                <div class="card-header bg-info text-light">
                  {{ song.title }}
                </div>
                <div class="card-body">{{ song.artist }}</div>
              </div>
            </button>
          </div>
        </section>
      </div>
      <!-- Fin de la section Playlist -->
    </main>
  </div>
</template> 

<script>
export default {
  name: "app",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,

      // Debut Element Morceau
      songs: [
        {
          title: "St-Chinian",
          artist: "Twans",
          src: require("./assets/stchinian.mp3"),
        },
        {
          title: "Blanc et Noir",
          artist: "Twans",
          src: require("./assets/blanc-noir.mp3"),
        },
        {
          title: "Entre l'Aquitaine et la Loire",
          artist: "Twans",
          src: require("./assets/aquitaine.mp3"),
        },
        {
          title: "Muskd",
          artist: "Twans",
          src: require("./assets/muskd.mp3"),
        },
        {
          title: "L'ombre des palmiers",
          artist: "Twans",
          src: require("./assets/ombre.mp3"),
        },
        // Fin Element Morceau
      ],
      player: new Audio(),
    };
  },

  // Contrôle des Morceaux
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];

      this.play(this.current);
    },

    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
};
// Fin de contrôle des morceaux
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  background-color: rgb(230, 230, 230);
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: black;
  color: floralwhite;
}

.container {
  border-radius: 15px;
  padding: 60px;
  margin: 60px;
}

.controls {
  display: flex;
  justify-content: center;
  padding: 30px 15px;
}

.play,
.pause {
  margin: 0px 25px;
}
</style>
