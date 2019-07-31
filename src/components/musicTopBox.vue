<template>
  <div>

    <el-row>
      <el-col :span="24"><div class="">動態歌曲名稱OOOOOOO</div></el-col>
    </el-row>
    <el-row>
      <el-col :span="24"><div class="">動態歌曲歌手</div></el-col>
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
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="4">
                  <div class="inline">
                      <div class="iconBox box2"><div class="content"><font-awesome-icon icon="angle-double-left" /></div></div>
                      <div class="iconBox box2"><div class="content"><font-awesome-icon icon="play" /></div></div>
                      <div class="iconBox box2"><div class="content"><font-awesome-icon icon="pause"  /></div></div>
                      <div class="iconBox box2"><div class="content"><font-awesome-icon icon="angle-double-right" /></div></div>
                  </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="16">
                  <div class="inline">
                      <div class="iconBox box2"><div class="content"><font-awesome-icon icon="random" /></div></div>
                      <div class="iconBox box2 iconFade"><div class="content"><font-awesome-icon icon="retweet" /></div></div>
                  </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="4">
                        <div class="inline">
                          <div><font-awesome-icon icon="volume-up" /></div>
                          <div><el-slider v-model="volume" :min="20" :max="200"></el-slider></div>
                        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="12"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
      <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="8"><div class="grid-content bg-purple-light"></div></el-col>
      <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
    <el-row>
      <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
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
.musicControler {
  background-color:#dddddd;
  border-radius: 5px;
  height:auto;
  padding: 10px;
}
.ControlerInside{
  width:100%;
  height: 100%;
  margin:auto;
}
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
.box2 .content{
  position: absolute;
  top:50%;
  left: 50%;
  margin-left: -10px;
  margin-top: -10px;
}
.coverImg {
  width: 300px;
  height: 300px;
  overflow: hidden;
  border-radius: 5px;
  border: #2c3e50 1px solid;
}
.el-image{
  width:100%;
  height:100%;
}
.clearFix{
    display: block;
    content: "";
    clear: both;
}
.iconFade {
  opacity: 0.5;
}
  .el-row {
    margin-bottom: 20px;
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>
