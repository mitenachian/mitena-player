<template>
  <div>

    <el-row>
      <el-col :span="24"><div class="padding_10">You Need To Calm Down</div></el-col>
    </el-row>
    <el-row>
      <el-col :span="24"><div class="padding_10">Taylor Swift</div></el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div>
         <span style="float:left">01:00</span>
         <span style="float:right">04:15</span>
         <div class="clearFix"></div>
        </div>
        <el-slider v-model="currentTime" :show-tooltip="false"></el-slider>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <div class="padding_10">
        <el-col :xs="24" :sm="10" :md="10" :lg="10" :xl="10">
          <div class="inline">
            <div class="iconBox box2"><div class="content"><font-awesome-icon icon="angle-double-left" /></div></div>
            <div class="iconBox box2"><div class="content"><font-awesome-icon icon="play" /></div></div>
            <div class="iconBox box2"><div class="content"><font-awesome-icon icon="pause" /></div></div>
            <div class="iconBox box2"><div class="content"><font-awesome-icon icon="angle-double-right" /></div></div>
          </div>
        </el-col>
        <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8">
          <div class="inline">
              <div class="iconBox box2"><div class="content"><font-awesome-icon icon="random" /></div></div>
              <div class="iconBox box2 iconFade"><div class="content"><font-awesome-icon icon="retweet" /></div></div>
          </div>
        </el-col>
        <el-col :xs="24" :sm="6" :md="6" :lg="6" :xl="6">
          <div><font-awesome-icon icon="volume-up" /></div>
          <div><el-slider v-model="volume" :min="20" :max="100"></el-slider></div>
        </el-col>
      </div>
    </el-row>
  </div>
</template>

<script>

export default {
  components: {
  },
  name: 'musicTopBox',
    data() {
    return {
      currentTime: 50,
      volume: 50,
    };
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.inline{
    overflow: auto;
    white-space: nowrap;
}
.iconBox {
  padding:2px;
  border: #2c3e50 solid 3px;
  display: inline-block;
  width: 40px;
  height: 40px;
  margin: 10px;
  border-radius: 50%;
  cursor: pointer;
  text-align: center;
  position: relative;
}
.iconBox:hover{
   border: #dddddd solid 3px;
}
.box2 .content{
  position: absolute;
  top:50%;
  left: 50%;
  margin-left: -8px;
  margin-top: -8px;
}
.clearFix{
    display: block;
    content: "";
    clear: both;
}
.iconFade {
  opacity: 0.5;
}
.padding_10{
  padding:10px;
}
</style>
