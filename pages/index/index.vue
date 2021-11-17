<template>
  <div class="wedding">
    <div class="mainWarp" @tap="handleOpenPack">
    <img class="dot" :class="playing?'spin':''" src="../../images/musicdot.png" @tap.stop="handlePlayOrPause"> 
    <invitation :canOpen="canOpen" @onClose="canOpen = false, hasClosed = true" />
    <audio  id="player" loop  preload/>
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
	onShow(){
		this.music = uni.createInnerAudioContext();
		console.log(this.music)
		this.music.autoplay = true;
		this.music.src = 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/music/Perfect.mp3';
		this.music.onPlay(() => {
		  this.playing=true
		});
		this.music.onError((res) => {
		  console.log(res.errMsg);
		  console.log(res.errCode);
		});
		
	},
	onHide(){
		this.music.destroy()
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
    mounted() {},
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
