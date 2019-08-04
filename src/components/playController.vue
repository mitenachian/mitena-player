<template>
  <div>
    <el-row>
      <el-col :xs="24" :sm="24" :md="5" :lg="6" :xl="6">
        <div class="vhCenter">
          <div><p class="colorYellow">{{ current.title }}-{{ current.artist }}</p></div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
            <span style="float:left"><span class="controlIcon"><font-awesome-icon icon="volume-down"/></span></span>
            <span style="float:right"><span class="controlIcon"><font-awesome-icon icon="volume-up"/></span></span>
            <div class="clearFix"></div>
          </div>
             <el-slider v-model="volume" :min="0" :max="100" @input="onVolumeChange" @change="onVolumeChange"></el-slider>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="6" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
            <p>
              <span class="controlIcon"  @click="prev"><font-awesome-icon icon="angle-double-left" /></span>
              <span v-if="isPlaying"  @click="pause" class="controlIcon"><font-awesome-icon icon="pause" /></span>
              <span v-else class="controlIcon"  @click="play"><font-awesome-icon icon="play"/></span>
              <span class="controlIcon" @click="next"><font-awesome-icon icon="angle-double-right" /></span>
            </p>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="5" :lg="6" :xl="6">
        <div class="vhCenter">
            <div>
            <span style="float:left">{{ nowTime }}</span>
            <span style="float:right">{{ totalTime }}</span>
            <div class="clearFix"></div>
            </div>
            <!--<el-progress  @click="seek" :percentage="percentage" color="#f56c6c"></el-progress>-->
            <el-slider ref="progress"  @change="seek" :value="timeBar" :min="0" :max="duration" :show-tooltip="false" ></el-slider>
          </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
             <p>
             <span class="controlIcon"
             :class="{ 'colorYellow': isShuffle }"
             @click="shuffle">
             <font-awesome-icon icon="random" />
             </span>

             <span class="controlIcon"
             :class="{ 'colorYellow': repeatMode }"
             @click="repeat"
             >
             <font-awesome-icon icon="retweet" />
             </span>
             <span class="controlIcon"
             @click="toggleVideo"
             >
             <i class="el-icon-s-platform"></i>
             </span>
             </p>
          </div>
        </div>
      </el-col>
    </el-row>
      <div class="player-iframe" :class="{ 'player-iframe-s': showVideo }">
        <div id="player-iframe"></div>
      </div>  
  </div>
</template>
<script>
import _ from 'lodash';
import {
  getBuffer,
  getCurrentTime,
  pause,
  play,
  stop,
  seek,
  setVolume
} from '@/yt/ytplayer';
export default {
  components: {
  },
  name: 'playController',
    data() {
    return {
      showVideo: false,
      isPlaying: false,
      isShuffle: false,
      duration: null,
      currentTime: null,
      buffer: null,
      intervalId: null,
      volume: 50
    };
  },
  computed: {
    timeBar(){
      if(!this.currentTime) return 0;
      return this.currentTime;
    },
    percentage() {
      if (!this.currentTime || !this.duration) return 0;
      return (this.currentTime / this.duration) * 100;
    },
    bufferPercentage() {
      return this.buffer * 100;
    },
    index() {
      return this.$store.state.index;
    },
    current() {
      return this.$store.getters.current;
    },
    isLast() {
      return this.$store.getters.isLast;
    },
    repeatMode() {
      return this.$store.state.repeatMode;
    },
    nowTime() {
      if (!this.currentTime && this.isPlaying) return '00:00';
      if (!this.currentTime) return '';
      return `${_.padStart(
        Math.floor(this.currentTime / 60),
        2,
        '0'
      )}:${_.padStart(Math.floor(this.currentTime % 60), 2, '0')}`;
    },
    totalTime() {
      if (!this.duration) return '';
      return `${_.padStart(
        Math.floor(this.duration / 60),
        2,
        '0'
      )}:${_.padStart(Math.floor(this.duration % 60), 2, '0')}`;
    }
  },
  watch: {
    current(value, prev) {
      if (prev !== value) {
        this.stop();
        setTimeout(() => {
          this.play();
        }, 100);
      }
    }
  },
  methods: {
    play() {
      console.log("現正播放" + this.current.title)
      if (this.current) {
        play(this.current, this.onPlay, this.onPause, this.onEnd);
      }
    },
    onPlay(duration, currentTime) {
      this.isPlaying = true;
      this.duration = duration;
      this.currentTime = currentTime;
      this.intervalId = setInterval(() => {
        this.currentTime = getCurrentTime();
        this.buffer = getBuffer();
      }, 300);
    },
    clearInterval() {
      if (this.intervalId) {
        clearInterval(this.intervalId);
        this.intervalId = null;
      }
    },
    pause() {
      pause(this.onPause);
    },
    stop() {
      stop(this.onStop);
    },
    onPause() {
      this.clearInterval();
      this.isPlaying = false;
    },
    onStop() {
      this.clearInterval();
      this.isPlaying = false;
      this.duration = null;
      this.currentTime = null;
      this.buffer = null;
    },
    onEnd() {
      this.onStop();
      if (this.repeatMode === 'one') {
        this.play();
      } else if (!this.isLast || this.repeatMode === 'all') {
        this.$store.commit('nextSong', this.isShuffle);
        setTimeout(() => {
          this.play();
        }, 100);
      }
    },
    seek(e) {
      seek(
        parseFloat(this.currentTime)
      );
    },
    next() {
      const isPlayingNow = this.isPlaying;
      this.stop();
      this.$store.commit('nextSong', this.isShuffle);
      if (isPlayingNow) {
        setTimeout(() => {
          this.play();
        }, 100);
      }
    },
    prev() {
      const isPlayingNow = this.isPlaying;
      this.stop();
      this.$store.commit('prevSong');
      if (isPlayingNow) {
        setTimeout(() => {
          this.play();
        }, 0);
      }
    },
    shuffle() {
      this.isShuffle = !this.isShuffle;
    },
    repeat() {
      this.$store.commit('toggleRepeatMode');
    },
    onVolumeChange(e) {
      // this.volume = parseInt(e.target.value, 10);
      setVolume(this.volume);
    },
    toggleVideo() {
      this.showVideo = !this.showVideo;
      if (!this.isPlaying) {
        this.play();
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.vhCenter{
  margin:auto 0;
  padding:10px;
  vertical-align: middle;
  text-align:center
  }
.clearFix{
    display: block;
    content: "";
    clear: both;
}
.controlIcon {
  padding:0 20px 0 20px;
  cursor: pointer;
}
.controlIcon :hover {
  cursor: pointer;
  color:rgb(255, 208, 75);
}
.colorYellow {
  color: rgb(255, 208, 75);
}
.player-iframe {
 
    margin-top: 20px;
    position: absolute;
    top: -99999px;
    left: -99999px;
    width: 140px;
    height: 80px;
}
.player-iframe-s {
      top: unset;
      left: unset;
      bottom: 400px !important;
      right: 520px !important;
 }
</style>
