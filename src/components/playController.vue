<template>
  <div>
    <el-row>
      <el-col :xs="24" :sm="24" :md="5" :lg="6" :xl="6">
        <div class="vhCenter">
          <div><p class="colorYellow">You Need To Calm Down - Taylor Swift</p></div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="6" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
            <p>
              <span class="controlIcon"><font-awesome-icon icon="angle-double-left" /></span>
              <span v-if="playing" class="controlIcon"><font-awesome-icon icon="pause" /></span>
              <span v-else class="controlIcon"><font-awesome-icon icon="play"/></span>
              <span class="controlIcon"><font-awesome-icon icon="angle-double-right" /></span>
            </p>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="5" :lg="6" :xl="6">
        <div class="vhCenter">
            <div>
            <span style="float:left">01:00</span>
            <span style="float:right">04:15</span>
            <div class="clearFix"></div>
            </div>
            <el-slider v-model="currentTime" :show-tooltip="false"></el-slider>
          </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
             <p>
             <span class="controlIcon"><font-awesome-icon icon="random" /></span>
             <span class="controlIcon"><font-awesome-icon icon="retweet" /></span>
             </p>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4">
        <div class="vhCenter">
          <div>
            <span style="float:left"><span class="controlIcon"><font-awesome-icon icon="volume-down"/></span></span>
            <span style="float:right"><span class="controlIcon"><font-awesome-icon icon="volume-up"/></span></span>
            <div class="clearFix"></div>
          </div>
             <el-slider v-model="volume" :min="10" :max="100"></el-slider>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>

export default {
  components: {
  },
  name: 'playController',
    data() {
    return {
      currentTime: 30,
      volume: 20,
      playing: false,
    };
  },

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
</style>
