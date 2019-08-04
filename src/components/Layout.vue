<template>
    <el-container>
        <el-aside width="auto">
            <div class="logo" v-if="!isCollapse">
                <img src="../assets/logo.png"/>
            </div>
            <el-menu
                background-color="#545c64"
                text-color="#fff"
                active-text-color="#ffd04b"
                :collapse="isCollapse">
                <el-submenu index="1">
                    <template slot="title">
                    <i class="el-icon-location"></i>
                    <span>NEWS</span>
                    </template>
                    <el-menu-item-group>
                    <template slot="title">GROUP1</template>
                    <el-menu-item index="1-1">music</el-menu-item>
                    <el-menu-item index="1-2">music</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="GROUP2">
                    <el-menu-item index="1-3">music</el-menu-item>
                    </el-menu-item-group>
                    <el-submenu index="1-4">
                    <template slot="title">music</template>
                    <el-menu-item index="1-4-1">music</el-menu-item>
                    </el-submenu>
                </el-submenu>
                <el-menu-item index="2">
                    <i class="el-icon-headset"></i>
                    <span slot="title">MUSIC</span>
                </el-menu-item>
                <el-menu-item index="3" disabled>
                    <i class="el-icon-document"></i>
                    <span slot="title">ARTIST</span>
                </el-menu-item>
                <el-menu-item index="4">
                    <i class="el-icon-s-ticket"></i>
                    <span slot="title">EVENTS</span>
                </el-menu-item>
            </el-menu>
        </el-aside>
        <el-container>
            <el-header>
                <el-menu class="el-menu-demo" mode="horizontal"  background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
                    <el-menu-item index="1">
                        <i class="el-icon-menu" @click="isCollapse=!isCollapse"></i>
                    </el-menu-item>
                    <el-submenu index="2">
                        <template slot="title">Album</template>
                        <el-menu-item index="2-1">Something</el-menu-item>
                        <el-menu-item index="2-2">Something</el-menu-item>
                        <el-menu-item index="2-3">Something</el-menu-item>
                        <el-submenu index="2-4">
                        <template slot="title">Something</template>
                        <el-menu-item index="2-4-1">Something</el-menu-item>
                        <el-menu-item index="2-4-2">Something</el-menu-item>
                        <el-menu-item index="2-4-3">Something</el-menu-item>
                        </el-submenu>
                    </el-submenu>
                    <el-menu-item index="3" disabled>News</el-menu-item>
                    <el-menu-item index="4" >WHY</el-menu-item>
                </el-menu>
            </el-header>
            <el-main>
                <mainContent/>
            </el-main>
            <div class="footer">
                <playController/>
            </div>
        </el-container>
    </el-container>
</template>

<script>
import playController from './playController.vue';
import mainContent from './mainContent.vue';
export default {
  components: {
      playController,
      mainContent,
  },
name: 'home',
data() {
    return {
        window: {
            width: 0,
            height: 0
        },
        isCollapse: true,
    };
  },
  created() {
    window.addEventListener('resize', this.handleResize)
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
      if(this.window.width <= 992) {
          this.isCollapse = true;
      } else {
          this.isCollapse = false;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
    max-width: 1200px;
    margin: auto;
}
.el-aside {
    background-color: #545c64;
    color: white;
    min-height: 100vh;

}
.logo {
    background-color: #434a50;
}
.logo img {
    width: 150px;
    padding:30px;
}
.el-menu {
    border:0;
}
.el-header {
    overflow: hidden;
    padding:0 !important;
    border-bottom: 2px solid #f3b92a;
}
.el-footer {
     background-color: #434a50;
     min-height:100px;
     height: auto;
}
.clearFix{
    display: block;
    content: "";
    clear: both;
}
.footer{
    background-color: #434a50;
    color: white;
    height: auto;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
}
.el-main {
    margin:0px;
    padding:0px;
    overflow-y: hidden;
    background-color: #f3b92a;
    background-image:url('../assets/Iam.jpg'); 
    background-repeat: no-repeat;
    background-position: 0% 100%; 
}
</style>
