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
                    <router-link class="navbar-brand" to="/">{{ $t("info.title") }}</router-link>
                </div>
                
                <div class="collapse navbar-collapse" id="bs-navbar-collapse">
                    <ul class="nav navbar-nav">
                        <li><a href="https://www.youtube.com/channel/UCp-5t9SrOQwXMU7iIjQfARg" target="_blank"><img src="resources/youtube_social_icon_red.png" height="18"/></a></li>
                        <li><a href="https://twitter.com/ookamimio" target="_blank"><img src="resources/Twitter_Social_Icon_Circle_Color.png" height="20"/></a></li>
                        <li><a href="http://t.cn/A6ZtZRD2" target="_blank"><img src="resources/Android.png" height="21"/></a></li>
                        <li><a href="https://www.lanzous.com/iarrhef" target="_blank"><img src="resources/Apple.png" height="21"/></a></li>
                        <li><a href="javascript:location.reload();" target="_blank"><img src="resources/refresh.png" height="20"/></a></li>
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
                <div class="pull-left">
                    <div class="text-left"><a href="https://github.com/MioButton/MioButton" target="_blank">{{$t("info.toGithub")}} <img src="https://img.shields.io/github/stars/MioButton/MioButton.svg?style=social"/></a></div>
                    <div class="text-left">{{$t("info.notOfficial")}}</div>
                </div>
                <div class="pull-left">
                    <div class="text-left"><a href="https://miobutton.github.io/MioButton/" target="_blank">{{$t("info.audioStaff")}}</a></div>
                    <div>寒いもみじ雪 2020 <span style="color: rgba(0, 0, 0, 0.3)">Powered By Meowsound Idols</span></div>
                </div>
            </div>
        </footer>
  </div>
</template>

<script type="text/javascript">
        !function (e, t, a) {function r() {for (var e = 0; e < s.length; e++) s[e].alpha <= 0 ? (t.body.removeChild(s[e].el), s.splice(e, 1)) : (s[e].y--, s[e].scale += .004, s[e].alpha -= .013, s[e].el.style.cssText = "left:" + s[e].x + "px;top:" + s[e].y + "px;opacity:" + s[e].alpha + ";transform:scale(" + s[e].scale + "," + s[e].scale + ") rotate(45deg);background:" + s[e].color + ";z-index:99999");requestAnimationFrame(r)}function n() {var t = "function" == typeof e.onclick && e.onclick;e.onclick = function (e) {t && t(), o(e)}}function o(e) {var a = t.createElement("div");a.className = "heart", s.push({el: a,x: e.clientX - 5,y: e.clientY - 5,scale: 1,alpha: 1,color: c()}), t.body.appendChild(a)}function i(e) {var a = t.createElement("style");a.type = "text/css";try {a.appendChild(t.createTextNode(e))} catch (t) {a.styleSheet.cssText = e}t.getElementsByTagName("head")[0].appendChild(a)}function c() {return "rgb(" + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + ")"}var s = [];e.requestAnimationFrame = e.requestAnimationFrame || e.webkitRequestAnimationFrame || e.mozRequestAnimationFrame || e.oRequestAnimationFrame || e.msRequestAnimationFrame || function (e) {setTimeout(e, 1e3 / 60)}, i(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"), n(), r()}(window, document);
</script>

<style lang="scss">
@import "../node_modules/bootstrap/dist/css/bootstrap.css";
body{
    padding-top: 51px;
}
.main-content{
    min-height: 100vh;
    background-image: url('/resources/bg.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
.footer {
    width: 100%;
    height: 100%;
    min-height: 60px;
    background-color: #ebebeb;
}
.footer-content {
    padding-top: 10px;
    color: #555;
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

