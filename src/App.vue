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
        (function(window,document,undefined){
			var hearts = [];
			window.requestAnimationFrame = (function(){
				return window.requestAnimationFrame ||
				window.webkitRequestAnimationFrame ||
				window.mozRequestAnimationFrame ||
				window.oRequestAnimationFrame ||
				window.msRequestAnimationFrame ||
				function (callback){
					setTimeout(callback,1000/60);
				}
			})();
			init();
			function init(){
				css(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: absolute;}.heart:after{top: -5px;}.heart:before{left: -5px;}");
				attachEvent();
				gameloop();
			}
			function gameloop(){
				for(var i=0;i<hearts.length;i++){
					if(hearts[i].alpha <=0){
						document.body.removeChild(hearts[i].el);
						hearts.splice(i,1);
						continue;
					}
					hearts[i].y--;
					hearts[i].scale += 0.004;
					hearts[i].alpha -= 0.013;
					hearts[i].el.style.cssText = "left:"+hearts[i].x+"px;top:"+hearts[i].y+"px;opacity:"+hearts[i].alpha+";transform:scale("+hearts[i].scale+","+hearts[i].scale+") rotate(45deg);background:"+hearts[i].color;
				}
				requestAnimationFrame(gameloop);
			}
			function attachEvent(){
				var old = typeof window.οnclick==="function" && window.onclick;
				window.onclick = function(event){
					old && old();
					createHeart(event);
				}
			}
			function createHeart(event){
				var d = document.createElement("div");
				d.className = "heart";
				hearts.push({
					el : d,
					x : event.clientX - 5,
					y : event.clientY - 5,
					scale : 1,
					alpha : 1,
					color : randomColor()
				});
				document.body.appendChild(d);
			}
			function css(css){
				var style = document.createElement("style");
				style.type="text/css";
				try{
					style.appendChild(document.createTextNode(css));
				}catch(ex){
					style.styleSheet.cssText = css;
				}
				document.getElementsByTagName('head')[0].appendChild(style);
			}
			function randomColor(){
				return "rgb("+(~~(Math.random()*255))+","+(~~(Math.random()*255))+","+(~~(Math.random()*255))+")";
			}
		})(window,document);
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

