<template>
    <div class="left"
    >
      <ul class="list">
        <li 
          v-for="(item, index) in list" :key="item.id"
          ref="listItems" 
          @mousedown="play(index, item)"
          @mouseup="resetActive"
          @click="sendId(index)"
          :class="getClass(index)"
        >
          {{ item.keyTrigger }}<audio ref="audio"  canplay preload="auto" :src="isbank?item.bankUrl:item.url"
        :volume="volume/100"
          ></audio>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['list', 'isVoice',"isbank","volume"],
    data() {
      return {
        currentIndex: -1,
      };
    },
    methods: {
      play(index) {
        if(this.isVoice){
            this.currentIndex = index;
            this.$nextTick(() => {
                this.$refs.audio[index].volume = this.volume / 100;
                this.$refs.audio[index].play();
            });
       }else{
         return
       }
      },
      resetActive() {
        this.currentIndex = -1;
      },
      sendId(index) {
        this.$emit('lookId', this.list[index].id);
      },
      getClass(index) {
        return {
          active: index === this.currentIndex && this.isVoice,
          active1: index === this.currentIndex && !this.isVoice,
        };
      },
    },
    mounted(){
        document.addEventListener('keydown', (e) => {
            const keyCode = e.keyCode;
            this.list.forEach((item, index) => {
                if (keyCode === item.keyCode) {
                    this.play(index);
                }
            })
        })
        document.addEventListener('keyup', () => {
            this.resetActive();
        })
    }
  };
  </script>
  

<style lang="scss">
.left{
            width: 60%;
            height: 600px;
            ul{
                margin-top: 20px;
                display: flex;
                flex-wrap: wrap;
                padding: 10px;
                li{
                    margin: 10px;
                    width: 170px;
                    height: 150px;
                    background: #717171;
                    margin-right: 10px;
                    font-size: 35px;
                    color: black;
                    box-shadow:  0px 0px 10px #717171;
                    border-radius: 10px;
                    text-align: center;
                    line-height: 150px;
                    cursor: pointer;
                    span{
                        pointer-events: none;
                    }
                }
                .active{
                    background: orange;
                    box-shadow: 0 0 0 0;
                }
                .active1{
                    box-shadow: 0 0 0 0 #717171;
                }
            }
        }
</style>