<template>
  <div id="app" class="wrap">
    <header class="header">
      <p><span>GTWR </span>云计算平台</p>
      <div class="login-container">
	      <a class="loginLink" @click="login()">用户登录</a>
	      <a class="loginLink"> / </a>
	      <a class="loginLink"   v-for="item in wpList" :key="item.name"
	      :class="{active : active == item.name}"
	       @click="selected(item.name)">{{item.name}}</a>
	   </div>
    </header><!-- /header -->
    <div class="main-content">
      <keep-alive>
        <router-view v-if="$route.meta.keepAlive"></router-view>
      </keep-alive>
        <router-view v-if="!$route.meta.keepAlive"></router-view>
    </div>
    <cover-par v-show="cover_show"></cover-par>
    <cover-login v-show="login_show"></cover-login>
    <cover-sign v-show="sign_show"></cover-sign>
    <cover-reset v-show="reset_show"></cover-reset>
  </div>
</template>

<script>
require('./style/app.scss')
import coverPar from './components/coverForParSelect.vue'
import coverLogin from './components/coverForlogin.vue'
import coverSign from './components/coverForSign.vue'
import coverReset from './components/coverForReset.vue'
import {mapState} from 'vuex'

export default {
  name: 'App',
  data(){
  	return{
  		wpList:[
  		{
  			name:'匿名登录'
  		}
  		],
  		active:''
  	}
  },
  computed:{
    ...mapState({
        // ...
      cover_show: state => state.cover_show,
      login_show: state => state.login_show,
      sign_show: state => state.sign_show,
      reset_show: state => state.reset_show
    })
  },
  methods:{
    login:function(){
      this.$store.dispatch('LoginShowAction',true);
    },
     selected(name){
    this.$router.push({path:"/home/dataview"});
    this.active = name;
    }
  },
  mounted(){
    
  },
  components:{
    coverPar,
    coverLogin,
    coverSign,
    coverReset
  }
}
</script>

<style>

</style>
