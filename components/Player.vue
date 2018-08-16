<template>
  <div class="player">
    <audio ref="audio">
      <source :src="song" type="audio/mpeg" />
    </audio>
    <div class="songs">
      <div class="song" v-for="song in songs" :key="song">
        <i class="material-icons current-song-icon" v-if="isSongCurrent(song)">{{ currentSongIcon }}</i>
        {{ song }}
      </div>
    </div>
    <div class="controls">
      <button class="control" @click="previous()"><i class="material-icons">skip_previous</i></button>
      <button class="control" @click="toggle()"><i class="material-icons">{{ centerIcon }}</i></button>
      <button class="control" @click="next()"><i class="material-icons">skip_next</i></button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Player',
  data() {
    return {
      songs: [
        'Milkshake_Daddy_-_08_-_Super_Sloppy_Space_Junk.mp3',
        'Obsibilo_-_03_-_Soixante-8.mp3'
      ],
      song: 'Milkshake_Daddy_-_08_-_Super_Sloppy_Space_Junk.mp3',
      status: 'pause'
    };
  },
  methods: {
    toggle() {
      if (this.status === 'play') {
        this.pause();
      } else {
        this.play();
      }
    },
    play() {
      this.status = 'play';
      this.$refs.audio.play();
    },
    pause() {
      this.status = 'pause';
      this.$refs.audio.pause();
    },
    next() {
      const index = this.songs.indexOf(this.song);
      this.song =
        index + 1 === this.songs.length ? this.songs[0] : this.songs[index + 1];
      this.$refs.audio.load();
      this.play();
    },
    previous() {
      const index = this.songs.indexOf(this.song);
      this.song =
        index - 1 < 0
          ? this.songs[this.songs.length - 1]
          : this.songs[index - 1];
      this.$refs.audio.load();
      this.play();
    },
    isSongCurrent(song) {
      return this.song === song;
    }
  },
  computed: {
    centerIcon() {
      return this.status === 'play'
        ? 'pause_circle_filled'
        : 'play_circle_filled';
    },
    currentSongIcon() {
      return this.status === 'play' ? 'play_arrow' : 'pause';
    }
  }
};
</script>

<style scoped>
.player {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 300px;
  max-width: 600px;
  border-radius: 10px;
  background-color: #242424;
}

.songs {
  flex: 1;
  overflow-y: auto;
  padding: 12px 0;
}

.song {
  width: 100%;
  height: 36px;
  display: flex;
  color: #8cbbd0;
  font-size: 18px;
  padding: 0 12px;
  cursor: pointer;
  text-align: left;
  overflow: hidden;
  line-height: 36px;
  align-items: center;
}

.song:hover {
  color: #e5662f;
  background-color: #2f84da;
}

.controls {
  width: 100%;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #2f84da;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
}

.control {
  padding: 0;
  width: 48px;
  height: 48px;
  border: none;
  margin: 0 12px;
  cursor: pointer;
  background-color: transparent;
  transition: transform 0.3s linear 0s;
}

.control:hover {
  transform: scale(1.5, 1.5);
}

.control:focus {
  outline: none;
}

.material-icons {
  font-size: 36px;
}

.current-song-icon {
  font-size: 24px;
  margin-right: 10px;
}
</style>
