<template>
  <div class="outter">
    <header class="header">
      <nav class="nav-wrapper">
        <router-link to="/top" class="fl logo"></router-link>
        <router-link to="/top" class="fl btn_hot" active-class="active"><span>HOT</span></router-link>
        <router-link to="/new" class="fl btn_new" active-class="active"><span>NEW</span></router-link>
        <div class="right-part">
          <router-link to="/login" class="loginbtn btn" v-show="!this.isLogin">登录</router-link>
          <a href="http://mainnet.asch.io/#/login" target="_blank" class="loginbtn btn" v-show="!this.isLogin">注册</a>
          <span class="logoutbtn btn" @click="logout" v-show="this.isLogin">注销</span>
          <router-link to="/account" class="accountbtn btn" v-show="this.isLogin">我的账户</router-link>
          <span class="submitbtn btn"@click="showPublish" v-show="this.isLogin">发布</span>
        </div>
      </nav>
    </header>
  </div>
</template>

<script>
  import { mapState } from 'vuex'
  export default {
    name: 'topbar',
    components: {
    },
    data: function () {
      return {
      }
    },
    methods: {
      logout: function () {
        this.$store.commit('callToast', {msgHeader: '注意', msgContent: '是否要进行注销？', _confirmfunc: '注销', _cancelfunc: '取消', deals: undefined, contract: 5})
      },
      showPublish: function () {
        if (this.isLogin === true) {
          this.$router.push('/publish')
        } else {
          this.$store.commit('callToast', {msgHeader: '发生错误', msgContent: '请先登录', _confirmfunc: '去登录', _cancelfunc: '不了', deals: undefined, contract: 3})
          this.$router.push('/login')
        }
      }
    },
    computed: {
      ...mapState(['isLogin', 'isPublishShow'])
    },
    created: function () {
      if (!window.sessionStorage.secret) {
        return
      }
      this.$store.dispatch('getUserInfo', {
        secret: window.sessionStorage.getItem('secret'),
        that: this
      })
      this.$router.push('/top')
    }
  }
</script>

<style lang="" scoped>
  .header{
    min-width: 1000px;
    background:linear-gradient(rgb(254, 254, 254), rgb(239, 239, 239));; 
    position: fixed;
    z-index: 9999;
    height: 60px;
    top: 0;
    left: 0;
    right: 0;
  }
  .nav-wrapper{
    height: 60px;
    width: 62.5%;
    margin: auto;
    text-align: center;
  }
  .nav-wrapper>a{
    display: inline-block;
    color: rgba(255, 255, 255, .8);
    font-size: 20px;
    margin-top: 5px;
  }
  .nav-wrapper .btn_hot{
    background-size: 100% 100%;
    margin-top: 0;
    width: 10.5%;
    height: 100%;
  }
  .nav-wrapper .btn_new{
    background-size: 100% 100%;
    margin-top: 0;
    width: 10.5%;
    height: 100%;
  }
  .nav-wrapper .right-part{
    width: 30%;
    height: 60px;
    float: right;
  }
  .btn_hot span{
    display: inline-block;
    color: rgb(255, 1, 1);
    background-size: 100% 100%;
    line-height: 60px;
    width: 100%;
    height: 100%;
  }
  .btn_new span{
    display: inline-block;
    color: rgb(23, 180, 173);
    line-height: 60px;
    width: 100%;
    height: 100%;
  }
  .nav-wrapper .logo{
    display: inline-block;
    width: 160px;
    height: 40px;
    background: url(/static/img/logo.png) no-repeat;
    margin-right: 15px;
    margin-top: 8px;
    background-size:100% 100%;
  }
  .fl{
    float: left;
  }
  .header .active{
    background-color: rgb(255, 255, 255);
    font-size: 20px;
  }
  .header .btn{
    display: inline-block;
    height: 20px;
    padding: 20px 15px;
    color: rgba(0, 0, 0, 1);
    display: inline-block;
    font-size: 20px;
    cursor: pointer;
  }
  .header .btn:hover{
    background-color: rgb(255, 255, 255);
  }
  .nav-wrapper{
  }
  @media screen and (max-width: 1441px) {
    /* 1360屏幕下 */
    .header{
      height: 40px;
    }
    .nav-wrapper{
      height: 40px;
      width: 80%;
    }
    .nav-wrapper .btn_hot{
      width: 7%;
    }
    .nav-wrapper .btn_new{
      width: 7%;
    }
    .nav-wrapper .right-part{
      width: 40%;
      height: 40px;
    }
    .btn_hot span{
      font-size: 13.3px;
      height: 40px;
      line-height: 40px;
    }
    .btn_new span{
      font-size: 13.3px;
      height: 40px;
      line-height: 40px;
    }
    .nav-wrapper .logo{
      width: 101px;
      height: 25px;
      margin-right: 15px;
      margin-top: 8px;
      margin-left: 5%;
    }
    .header .btn{
      width: 17%;
      height: 13.3px;
      padding: 13.5px 8px;
      font-size: 13.3px;
    }
  }
</style>
