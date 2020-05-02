<template>
  <div id="app">
        <Modal></Modal>
        <nav class="navbar navbar-default navbar-fixed-top">
            <div class="container-fluid">
                <div class="navbar-header">
                    <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-navbar-collapse" aria-expanded="false">
                        <span class="sr-only">{{ $t("action.toggleNavbar") }}</span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                    </button>
                    <router-link class="navbar-brand" to="/"><img src="/resources/brand.png" style="width:auto;height:23px;margin-top: -1.5px;"/></router-link>
                </div>
                
                <div class="collapse navbar-collapse" id="bs-navbar-collapse">
                    <ul class="nav navbar-nav">
                        <li><a href="https://www.youtube.com/channel/UCp-5t9SrOQwXMU7iIjQfARg" target="_blank"><img src="resources/youtube_social_icon_red.png" height="15.5"/></a></li>
                        <li><a href="https://twitter.com/ookamimio" target="_blank"><img src="resources/Twitter_Social_Icon_Circle_Color.png" height="20"/></a></li>
                        <li><a href="https://www.lanzous.com/ib3yeob" target="_blank"><img src="resources/Android.png" height="21.5"/></a></li>
                        <li><a href="https://www.lanzous.com/iarrhef" target="_blank"><img src="resources/Apple.png" height="21"/></a></li>
                    </ul>
                    <ul class="nav navbar-nav navbar-right">
                        <li class="dropdown">
                            <a href="javascript:;" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">{{$t("lang." + currentLang)}} <span class="caret"></span></a>
                            <ul class="dropdown-menu">
                                <li><a href="javascript:;" @click="chlang('zh-CN')">{{$t("lang.zh-CN")}}</a></li>
                                <li><a href="javascript:;" @click="chlang('ja-JP')">{{$t("lang.ja-JP")}}</a></li>
                            </ul>
                        </li>
                    </ul>
                </div>

            </div>
        </nav>
        <div class="container-fluid main-content">
            <router-view></router-view>
        </div>
        <footer class="footer">
            <div class="container-fluid footer-content">
                <button class="btn-buttom btn-buttom-info"><a href="javascript:location.reload();" target="_blank" style="color: #eeeeee;text-decoration: none">Version 2.7.7</a></button>
                <div class="pull-left">
                    <div class="text-left"><a href="https://github.com/MioButton/MioButton" target="_blank">{{$t("info.toGithub")}}</a></div>
                    <div class="text-left">{{$t("info.notOfficial")}}</div>
                </div>
                <div class="pull-left">
                    <div class="text-left"><a href="https://miobutton.github.io/MioButton/" target="_blank">{{$t("info.audioStaff")}}</a></div>
                    <div>寒いもみじ雪 2020 <span style="color: rgba(0, 0, 0, 0.5)">Powered By Meowsound Idols</span></div>
                </div>
            </div>
        </footer>
  </div>
</template>

<style lang="scss">
@import "../node_modules/bootstrap/dist/css/bootstrap.css";
.main-content{ /*内容部分*/
    min-height: 100vh;
    background-color: #333333;
}
.btn-buttom{
    border: 0px;
    padding: 1px 10px;
}
.btn-buttom-info {
    color: #fff;
    font-size: 12px;
    background-color: rgba(4, 255, 0, 0.5);
    border-radius: 5px;
}
.btn-buttom-info:hover {
    color: #fff;
    font-size: 12px;
    background-color: rgba(4, 255, 0, 0.2);
    border-radius: 5px;
}
.btn-buttom-info:focus {
    color: #fff;
    font-size: 12px;
    background-color: rgba(4, 255, 0, 0.2);
    border-radius: 5px;
}
.navbar{ 
    background-color: rgba(34,34,34,0.85);/*顶栏部分*/
}
.navbar-fixed-top{ 
    border-width: 0 0 0px;/*顶栏边缘*/
}
.navbar-toggle{ 
    border: 0px solid transparent;/*右侧按钮边框*/
}
.navbar-default .navbar-toggle:hover, 
.navbar-default .navbar-toggle:focus{ 
    background-color: rgba(0,0,0,0.3);/*右侧按钮选定背景色*/
}
.navbar-collapse{ 
    border-top: 0px solid transparent;/*右侧二级菜单顶部边框*/
}
.navbar-default .navbar-toggle .icon-bar{ 
    background: #999999;/*右侧按钮颜色*/
}
.navbar-default .navbar-nav > li > a{ 
    color: #999999;/*右侧语言状态显示文字颜色*/
}
.navbar-default .navbar-nav > .open > a, .navbar-default .navbar-nav > .open > a:hover, .navbar-default .navbar-nav > .open > a:focus{
    background-color: rgba(0,0,0,0.3); /*语言栏背景颜色*/
    color: #999999; /*语言栏显示字体*/
}
.dropdown-menu > li > a{
    color: #cccccc; /*语言栏文字颜色（长）*/
}
.dropdown-menu{
    background-color: rgba(0,0,0,0.3); /*语言栏背景颜色（长）*/
}
.navbar-default .navbar-brand {
    color: #FFBA75; /*标题显示颜色*/
}
.navbar-default .navbar-brand:hover {
    color: #FFd0a1; /*标题显示选定颜色*/
}
.dropdown-menu > li > a:hover, .dropdown-menu > li > a:focus{
    background-color: rgba(0,0,0,0.3); /*语言选择栏选定背景色（大）*/
}
.navbar-default .navbar-nav > li > a:hover{
    color: #ffffff;/*语言选择栏状态显示文字选定颜色（大）*/
}
.navbar-default .navbar-nav .open .dropdown-menu > li > a:hover{
    color: #ffffff;/*语言选择栏选择项文字颜色（大）*/
}
.footer {
    width: 100%;
    height: 100%;
    min-height: 60px;
    background-color: #222222;
}
.footer-content {
    padding-top: 10px;
    padding-bottom: 10px;
    color: #999999;
}
.text-right{
    text-align: right;
}
</style>

<script>
import Vue from 'vue'
import Component from 'vue-class-component'
import Modal from './components/modal.vue'
//import fetchpost from './util/fetchpost'

@Component({
    components:{
        Modal
    }
})
class App extends Vue {
    get currentLang(){
        return this.$i18n.locale;
    }
    created(){
        // eslint-disable-next-line 
        console.log("Produced by MoewSound Idols");
        this.$i18n.locale = localStorage.getItem("lang") || this.$i18n.locale;
    }
    chlang(v){
        this.$i18n.locale = v;
        localStorage.setItem("lang", v);
    }
}

export default App;
</script>

