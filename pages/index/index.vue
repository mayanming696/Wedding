<template>
  <div class="wedding">
    <div class="mainWarp" @click="handleOpenPack">
    <img class="dot" :class="playing?'spin':''" src="../../images/musicdot.png" @click.stop="handlePlayOrPause"> 
    <invitation :canOpen="canOpen" @onClose="canOpen = false, hasClosed = true" />
    <audio src="../../music/cnm.mp3" id="player" loop autoplay preload/>
    </div>
  </div>
</template>

<script>
  import Invitation from '@/components/Invitation'
  export default {
    components: {
      Invitation
    },
    data () {
      return {
        canOpen: false,
        hasClick: false,
        crtPage: 0,
        pageNum: 5,
        playing: false,
		music:null
      }      
    },
	onLoad(){
		this.music = uni.createInnerAudioContext();
		this.music.autoplay = true;
		this.music.src = 'https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-hello-uniapp/2cc220e0-c27a-11ea-9dfb-6da8e309e0d8.mp3';
		this.music.onPlay(() => {
		  this.playing=true
		});
		this.music.onError((res) => {
		  console.log(res.errMsg);
		  console.log(res.errCode);
		});
	},
    methods: {
      handleOpenPack () {
        this.canOpen = true;
      },
      handlePlayOrPause() {
        if(this.playing) {
			this.playing=false
          this.music.pause();
        } else {
		this.playing=true
         this.music.play();
        }
      }
    },
    mounted() {
      // swipeInit(function(direction) {
      //   let crt = this.crtPage;
      //   let num = this.pageNum;        
      //   let next;
      //   if(direction === 'up' && (crt + 1) < num) {          
      //     next = crt + 1;          
      //   } else if(direction === 'down' && (crt - 1) >= 0){
      //     next = crt - 1;
      //   } else {
      //     return ;
      //   }
      //   this.crtPage = next;
      //   for(let i = 0; i < num; i++) {
      //     document.querySelector(`.page${i}`).style.transform = `translate(0, ${100 * (i - next)}%)`
      //   }
      // }.bind(this));
      // const player = document.querySelector('#player');
      // document.addEventListener("WeixinJSBridgeReady", function () { 
      //   this.hasClick = true;
      //   player.play(); 
        
      // }, false);
      // document.body.addEventListener('click', () => {
      //   if(!this.hasClick) {
      //     this.hasClick = true;
      //     player.play();
      //   }       
      // });
      // let $audio = document.getElementById('player');
      // $audio.addEventListener("playing", function() {
      //   document.querySelector(`.dot`).className = "dot spin";
      //   this.playing = true;
      // }.bind(this));
      // $audio.addEventListener("pause", function() {
      //   document.querySelector(`.dot`).className = "dot";
      //   this.playing = false;
      // }.bind(this));
    },
    // name: 'Wedding'
  }

</script>

<style lang="less">
@import '@/assets/base.less';
@import '@/assets/bg.less';
html,
body{
  height: 100%;
  overflow: hidden;
}
@keyframes dot_ani {
  0% {
    -webkit-transform: rotate(0deg)
  }
  100% {
    -webkit-transform: rotate(360deg)
  } 
}
.wedding{
  position: relative;
  height: 100%;
  min-height: 100%;
  margin: 0 auto;
  .mainWarp{height: 100%;width: 100%;}
  .dot {
    position: absolute;
    right: 15px;
    top: 15px;
    width: 35px;
    height: 35px;    
    z-index: 999;
  }
  .spin {
    animation: dot_ani 1s linear infinite;
  }
}
</style>
