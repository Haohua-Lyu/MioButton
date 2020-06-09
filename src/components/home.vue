<template>
    <div class="container-fluid" >
        <div>
            <div class="btn-body-status">
                <div>{{ voice.name ? $t("action.playing") + $t("voice." + voice.name ) : $t("action.noplay") }}</div>
                <audio id="player" @ended="voiceEnd(false)"></audio>
            </div>
            <button class="btn btn-control" style="right:15px;bottom:15px;" @click="stopPlay"><img src="/resources/stop.svg" style="width: 30px;"></button>
            <button class="btn btn-control" style="right:60px;bottom:15px;" @click="random"><img src="/resources/choose.svg" style="width: 30px;"></button>
            <button class="btn btn-control" style="right:105px;bottom:15px;" :class="{ 'disabled': autoCheck }" @click="overlap" :title="$t('info.overlapTips')"><input class="checkbox" type="checkbox" v-model="overlapCheck"><img src="/resources/over.svg" style="width: 30px;"></button>
            <button class="btn btn-control" style="right:164px;bottom:15px;" :class="{ 'disabled': overlapCheck }" @click="autoPlay"><input class="checkbox" type="checkbox" v-model="autoCheck"><img src="/resources/auto.svg" style="width: 30px;"></button>
            <div class="title">{{$t("info.title")}}<img src="/resources/bg.gif" style="width:63px;height:auto;margin-bottom: 3px;"></div>
                <div class="cate-header-panel">{{$t("action.live")}}
                    <div v-for="(item) in youtubeData.channels" :key="item.id"><button class="btn btn-info" v-if="item.id === 'UCp-5t9SrOQwXMU7iIjQfARg'">{{$t('info.subscriber')}}{{item.subscriberCount}}</button></div>
                    <div v-for="live in live_data" :key="live.startTime">
                        <div v-if="live.title.length">
                            <span v-if="live.type === 'upcoming'" style="font-size:17px;">{{$t("action.plan")}}{{ format_time(live.startTime) }}</span>
                            <span v-if="live.type === 'live'" class="warning--text" style="font-size:17px;">{{$t("action.ing")}}</span>
                            <button class="btn btn-info"><a 
                                :href="'https://www.youtube.com/watch?v=' + live.id"
                                target="_blank"
                                style="text-decoration: none;color: #ffffff;"
                                :class="live.type === 'live' ? 'error--text' : ''"
                            >
                              {{live.title}}
                            </a></button>
                        </div>
                    </div>
                </div>
                <div class="cate-header-panel">{{$t("action.random")}}
                        <input id="share" class="btn btn-random" style="width: 190px;-webkit-user-select:text !important;" type="text" name="u" value :placeholder="$t('action.placeholder')">
                        <button class="btn btn-info" @click="randomshare">{{$t("action.share")}}</button>
                </div>
                <div class="cate-header-panel">{{$t("action.adtitle")}}
                    <button class="btn btn-info-ad" onclick="window.open('https://www.bilibili.com/read/readlist/rl210208')">{{$t("action.weekly")}}</button>
                    <button class="btn btn-info-ad" onclick="window.open('https://vtbbtn.org')">{{$t("action.vtbbtn")}}</button>
                    <button class="btn btn-info-ad" onclick="window.open('https://sticker.ookamimio.org')">{{$t("action.sticker")}}</button>
                </div>
            <div v-for="category in voices" v-bind:key="category.categoryName">
                <div class="cate-header">{{ $t("voicecategory." + category.categoryName) }} 
                    <div class="cate-body">
                        <button class="btn btn-new" v-for="voiceItem in category.voiceList" v-bind:key="voiceItem.name" @click="play(voiceItem)">{{ $t("voice." + voiceItem.name )}}</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.title{
    text-align: left;
    margin-top: 65px;
    border-radius: 30px;
    text-align: left;
    color: #fff;
    font-size: 35px;
    padding-top: 10px;
    font-weight: 700;
    padding-bottom: 30px;
    max-width: max-content;
}
.btn:hover, .btn:focus, .btn.focus{
    color: #ffffff;
}
.btn-control{
    position: fixed;
    background-color: #ff7d7db7;/*背景颜色*/
    border: 0px; /*边框去除*/
    border-radius: 17px;/*边框圆角*/
    max-width: 100%;
    padding: 3px;
    font-weight: 600;
    margin-top: 0px;
    margin-bottom: 0px;
    font-weight: 700;
    font-size: 15px;
    text-align: center;
}
.btn-random{/*控制中心按钮*/
    background-color: #FFACAC;/*背景颜色*/
    border: 0px; /*边框去除*/
    border-radius: 17px;/*边框圆角*/
    padding-top: 3px;
    font-weight: 600;
    padding-bottom: 3px;
    margin-left: 5px;
    margin-right: 5px;
    word-warp: break-word !important;
    word-break: break-all !important;
    white-space: normal !important;
}
.btn-info{/*控制中心按钮*/
    background-color: #FFACAC;/*背景颜色*/
    border: 0px; /*边框去除*/
    border-radius: 17px;/*边框圆角*/
    max-width: 100%;
    margin: 5px;
    padding-top: 3px;
    font-weight: 600;
    padding-bottom: 3px;
    margin-top: 0px;
    margin-bottom: 0px;
    word-warp: break-word !important;
    word-break: break-all !important;
    white-space: normal !important;
}
.btn-info:hover{/*控制中心按钮选定*/
    background-color: #FF9696;/*背景颜色*/
}
.btn-info:focus{/*控制中心按钮选定*/
    background-color: #FF9696;/*背景颜色*/
}
.btn-info-ad{/*宣传中心按钮*/
    background-color: #FFACAC;/*背景颜色*/
    padding-top: 3px;
    margin: 0 5px;
    padding-bottom: 3px;
    font-weight: 600;
    border-radius: 17px;/*边框圆角*/
    max-width: 100%;
    word-warp: break-word !important;
    word-break: break-all !important;
    white-space: normal !important;
}
.btn-info-ad:hover{/*宣传中心按钮选定*/
    background-color: #FF9696;/*背景颜色*/
}
.btn-info-ad:focus{/*宣传中心按钮选定*/
    background-color: #FF9696;/*背景颜色*/
}
.cate-header{/*分类标题*/
    background-color: rgb(66, 66, 66);
    border-radius: 30px;
    text-align: left;
    font-weight: 600;
    color: #fff;
    padding-top: 18px;
    padding-left: 20px;
    font-size: 20px;
    margin-top: 12px;
    margin-bottom: 12px;
}
.btn-body-status{/*播放状态分类标题*/
    background-color: #ff7d7db7;
    color: #fff;
    text-align: center;
    position: fixed;
    top: 0px;
    left: 0px;
    right: 0px;
    font-size: 14px;
    padding-top: 0px;
    padding-bottom: 0px;
    padding-left: 30px;
    padding-right: 30px;
    font-weight: 600;
}
.cate-header-panel{/*控制中心分类标题*/
    background-color: rgba(255, 122, 124, 0.8);
    border-radius: 30px;
    text-align: left;
    color: #fff;
    font-size: 20px;
    padding-top: 14px;
    padding-left: 17px;
    padding-right: 17px;
    font-weight: 600;
    padding-bottom: 14px;
    margin-bottom: 12px;
    max-width: max-content;
}
.cate-body{
    margin-top: 12px;
    margin-bottom: 20px;
    padding-bottom: 12px;
    margin-right: 12px;
    margin-left: -8px;
    text-align: left;
    color: #aaaaaa;
}
.cate-body-function{/*功能分类内容*/
    margin-top: 10px;
    text-align: left;
    color: #aaaaaa;
}
.cate-body button{
    margin: 5px;
}
.btn-new {
    color: #fff;
    background-color: rgba(199, 53, 52, 0.8);
    border-radius: 15px;
    max-width: 100%;
    font-weight: 600;
    word-warp: break-word !important;
    word-break: break-all !important;
    white-space: normal !important;
}
.btn-new:focus{
    color: rgba(255, 122, 124, 0.815);
}
.checkbox {
    display: inline-block;
    vertical-align: middle;
    margin: 0;
}
</style>


<script>
import Vue from 'vue'
import Component from 'vue-class-component'
import VoiceList from '../voices.json'
import axios from 'axios'

@Component
class HomePage extends Vue {
    live_data = null;
    voices = VoiceList.voices;
    autoCheck = false;
    overlapCheck = false;
    voice = {};
    live_data = {};
    live_data_loading = true;
    youtubeData = {channels: null};
    created() { 
        this.youtube()
    }
    youtube() {
        axios.get('https://api.jetri.co/channels')
        .then(response => {
        this.youtubeData = response.data
        })
    }
    mounted() {
        axios.get('https://api.jetri.co/live')
        .then(response => { 
            let fetched = response.data;
            let mio_lives = [];
            const channel_id = 'UCp-5t9SrOQwXMU7iIjQfARg';
            fetched.live.forEach(function(item){
                if (item.channel === channel_id){
                    mio_lives.push(item);
                }
            });
            fetched.upcoming.forEach(function(item){
                if (item.channel === channel_id){
                    mio_lives.push(item);
                }
            });
            this.live_data = mio_lives;
            this.live_data_loading = false;
        })
    }
    format_time(){
        var ts = arguments[0] || 0;
        var t,y,m,d,h,i,s;
        t = ts ? new Date(ts*1000) : new Date();y = t.getFullYear();m = t.getMonth()+1;d = t.getDate();h = t.getHours();i = t.getMinutes();s = t.getSeconds();
        return y+'-'+(m<10?'0'+m:m)+'-'+(d<10?'0'+d:d)+' '+(h<10?'0'+h:h)+':'+(i<10?'0'+i:i)+':'+(s<10?'0'+s:s);
    }
    play(item){
        if (this.overlapCheck) {
            let audio = new Audio("voices/" + item.path);
            this.voice = item;
            audio.play()
        } else {
            this.stopPlay();
            let player = document.getElementById('player');
            player.src = "voices/" + item.path;
            this.voice = item;
            player.play();
        }
    }
    stopPlay(){
        let player = document.getElementById('player');
        player.pause();
        this.voiceEnd(true);
    }
    voiceEnd(flag) {
        if(flag !== true && this.autoCheck) {
            this.random();
        } else {
            this.voice = {};
        }
    }
    random() {
        let tempList = this.voices[this._randomNum(0, this.voices.length - 1)];
        this.play(tempList.voiceList[this._randomNum(0, tempList.voiceList.length - 1)]);
    }
    randomshare() {
        let tempList = this.voices[this._randomNum(0, this.voices.length - 1)];
        var title=this.$t("voice."+ tempList.voiceList[this._randomNum(0, tempList.voiceList.length - 1)].name);
        var res=document.getElementById('share').value;
        if(this.$i18n.locale === 'ja-JP'){
            window.open("https://twitter.com/intent/tweet?text="+"%23ミオボタン %23ミオかわいい 今日、「"+res+"」のランダムオーディオは「"+title+"」です！ より多くのオーディオを聞くには、「ミオボタン」のWebサイトにアクセスしてください~ https://t.co/TLdj8E9Rct");
        } else {
            window.open("https://twitter.com/intent/tweet?text="+"%23ミオボタン %23ミオかわいい 今天，“"+res+"”的随机音频是“"+title+"”！ 访问狼按钮网站聆听更多音频 https://t.co/TLdj8E9Rct");
        }
    }
    autoPlay(){
        if (this.overlapCheck) {
            return;
        }
        this.autoCheck = !this.autoCheck;
    }
    overlap() {
        if (this.autoCheck) {
            return;
        }
        this.overlapCheck = !this.overlapCheck;
    }
    _randomNum(minNum, maxNum) {
        switch(arguments.length) {
            case 1:
                return parseInt(Math.random() * minNum + 1, 10);
            case 2:
                return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10);
            default:
                return 0;
        }
    } 
}
export default HomePage;
</script>