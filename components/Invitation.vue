<template>
	<div class="componentsWarp">
  <div class="wedding-invitation" :class="{ 'invitation-bounce':canOpen }">
    <div class="invitation-container" :class="{ 'invitation-down':isOpening }">
      <div class="invitation-cover">
        <div class="cover-content" :class="{'invitation-up':isOpening}">
          <div class="content-inside">
            <img class="content-inside-photo" src="@/images/photo.jpg">
            <!-- <p>我要求婚啦！</p> -->
            <p><b>Marco & June</b></p>
            <p>时间：2021-12-25</p>
            <p>地点：<b>深圳市坪山区我愿意咖啡屋</b></p>
            <div class="content-inside-bless">
              <input
                placeholder="写下你的祝福" 
                @focus="isFocused = true"
                v-model="wish"
                ref="wishInput"
              >
              <p v-if="!wish && isFocused && hasEntered">请输入祝福哦</p>
              <div style="margin-top: 50upx;">
                <button @click="closeInvitation">发送你的祝福</button>
                <!-- <button @click="closeInvitation">关闭</button> -->
              </div>
            </div>
          </div>
        </div>
        <div class="cover-inside-left" :class="{'opening':isOpening}"></div>
        <div class="cover-inside-right" :class="{'opening':isOpening}"></div>
        <img class="cover-inside-seal" src="@/images/seal.png" @click="openInvitation" :class="{'invitation-flight':isOpening}">
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: ['canOpen'],
  data() {
    return {
      isOpening: false,
      wish: '',
      isFocused: false,
      hasEntered: false
    }
  },
  methods: {
    // 打开邀请函
    openInvitation(){
      this.isOpening = true
    },
    closeInvitation () {
      this.isOpening = false
      setTimeout(() => {
        this.$emit('onClose')
      }, 660)
    },
    // 发送弹幕
    sendBarrage(){
      this.$nextTick(() => {
        this.hasEntered = true
        if (!this.wish) {
          return
        }
        this.isOpening = false
        // this.$refs.wishInput.blur()
        // setTimeout(() => {
        //   this.$emit('sendBarrage', this.wish)
        // }, 660)
      })
    }
  }
}
</script>

<style lang="less">
	.componentsWarp{
		height: 100%;
		width: 100%;
		position: fixed;
		left: 0;
		top: 0;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
  .wedding-invitation{
    // position: absolute;
    // top: 0;
    // left: 0;
	position: absolute;
	top: 100upx;
	left: 30upx;
	width: calc(100% - 60upx);
	height: calc(100% - 250upx);
    // padding: 180upx 30upx 30upx 180upx;
    // padding-top: 100upx;
    z-index: 4;
    transform: scale(0.05);
    opacity: 0;
    transition: transform 0.8s cubic-bezier(.26,1.84,.39,.61), opacity 0.5s linear;
    background-size: 100%;
	margin: auto;
    // overflow: hidden;
    &.invitation-bounce{
      opacity: 1;
      transform: scale(1);
      -webkit-transform: scale(1);
    }
    .invitation-container{
      position: relative;
      width: 100%;
      height: 100%;
      transition: transform 0.6s cubic-bezier(0.4, 0, 1, 1);
      &.invitation-down{
        transform: translateY(20px);
      }
      .invitation-cover{
        width: 92%;
        height: 100%;
        background-color: #D65047;
        border-radius: 10px;
        perspective: 500px;
        box-shadow: 0 0 20px 2px rgba(0, 0, 0, 0.15);
		margin: auto;
        .cover-content{
          // position: absolute;
          // top: 0;
          // left: 0;
          // width: 100%;
          height: 100%;
          padding: 10px 20px;
          transition: transform 0.6s cubic-bezier(0.4, 0, 1, 1);
		  overflow: hidden;
          &.invitation-up{
            transform: translateY(-60upx);
          }
          .content-inside{
			  display: flex;
			  flex-direction: column;
			  align-items: center;
            height: calc(100% - 60upx);
            padding: 20upx;
            // color: #a9895d;
            color: #544c37;
            // background-color: #FFF1DE;
            background-color: #f1ede2;
            text-align: center;
            overflow: auto;
            .content-inside-photo{
              width: 100%;
			  height: 40%;
              margin-bottom: 10px;
              padding: 5px;
              border: 1px solid #f7debb;
              // border: 1px solid #a2b6a4;
            }
            p{
              margin-top: 0;
              margin-bottom: 5px;
            }
            .content-inside-bless{
              input{
                width: 100%;
                height: 35px;
                margin-bottom: 10px;
                outline: none;
                border: none;
                border-bottom: 1px solid #f7debb;
                // border-bottom: 1px solid #a2b6a4;
                color: #a9895d;
                background: transparent;
                font-size: 16px;
                &::-webkit-input-placeholder { color: #E8D1B1;font-size: 12px; }
                &::-moz-placeholder { color: #E8D1B1;font-size: 12px; }
                &:-ms-input-placeholder { color: #E8D1B1;font-size: 12px; }
                &:-moz-placeholder { color: #E8D1B1;font-size: 12px; }
              }
              >div{
                display: flex;
                button{
                  width: 100%;
                  height: 35px;
				  line-height: 35px;
                  color: #a9895d;
                  background: #f7debb;
                  border: none;
                  outline: none;
                  &:disabled{
                    opacity: 0.8;
                  }
                  &:first-child{
                    margin-right: 10px;
                    flex: 1;
                  }
                  &:last-child{
                    width: 80px;
                    border: 1px solid #f7debb;
                    background: transparent;
                  }
                }
              }
            }
          }
        }
        .cover-inside-left{
          position: absolute;
          left: 0;
          top: 0;
          width: 70%;
          height: 100%;
          border-radius: 10px;
          // background-color: #D65047;
          background-color: #f3f0e6;
          box-shadow: 5px 0 10px rgba(0,0,0,0.2);
          z-index: 6;
          transition: transform 0.5s;
          transform-origin: 0 50%;
          &.opening{
            transform: rotate3d(0,1,0,-140deg);
          }
        }
        .cover-inside-right{
          position: absolute;
          right: 0;
          top: 0;
          width: 40%;
          height: 100%;
          border-radius: 10px;
          // background-color: #D65047;
          background-color: #f3f0e6;
          box-shadow: -5px 0 10px rgba(0,0,0,0.2);
          z-index: 5;
          transition: transform 0.5s;
          transform-origin: 100% 50%;
          &.opening{
            transform: rotate3d(0,1,0,140deg);
          }
        }
        .cover-inside-seal{
          position: absolute;
          left: 70%;
          bottom: 100px;
          width: 80px;
          height: 80px;
          margin-left: -40px;
          z-index: 7;
          transform-origin: 50% 50%;
          transition: all 0.8s cubic-bezier(0.4, 0, 1, 1);
          &.invitation-flight{
            opacity: 0;
          }
        }
      }
    }
  }
</style>
