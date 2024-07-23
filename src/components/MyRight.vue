<template>
  <div class="right">
    <div class="power_btn">
      <p>Power</p>
      <span class="power"  ref="power"
      @click="toggleVoice"
      ><em 
      ref="em" 
      :class="{active2:isVoice}"
      ></em></span>
    </div>
    <div class="name">{{ id }}</div>
    <input type="range" @input="change($event)" >
    <div class="bank_btn">
      <p>Bank</p>
      <span class="bank"
      @click="toggleMusicStyle"
      ><em
      :class="{active2:isbank}"
      ></em></span>
    </div>
  </div>
</template>

<script>


export default {
  props:["id"],
  data(){
    return{
      isVoice:true,
      isbank:false,
    }
  },
  methods:{
    toggleVoice(){
       if(this.isVoice){
          this.isVoice=false;
          this.$emit("voiceOnOff",this.isVoice);
       }else{
          this.isVoice=true;
          this.$emit("voiceOnOff",this.isVoice);
       }
    },
    toggleMusicStyle(){
        if(this.isbank){
          this.isbank=false;
          this.$emit("musicStyle",this.isbank);
        }else{
          this.isbank=true;
          this.$emit("musicStyle",this.isbank);
        }
    },
    change(e){
      this.$emit("changeVolume", e.target.value);
    }
  },
  created(){
  },
}
</script>

<style lang="scss">
     .right{
            margin: 100px auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            .power_btn{
                width: 240px;
                height: 130px;
                display: flex;
                flex-direction: column;
                align-items: center;
                margin-bottom: 10px;
                p{
                    font-size: 30px;
                    text-align: center;
                    font-weight: 900;
                }
                span{
                    width: 100px;
                    height: 40px;
                    text-align: center;
                    background: #000000;
                    em{
                        width: 45px;
                        height: 30px;
                        display: block;
                        background: #f2a514;
                        cursor: pointer;
                        margin-top: 5px;
                        margin-left: 5px;
                    }
                }
            }
            .name{
                font-size: 40px;
                font-weight: 900;
                margin-bottom: 20px;
                width: 300px;
                height: 100px;
                background: #6b6b6b;
                line-height: 100px;
                text-align: center;
                margin-bottom: 60px;
            }
            input[type=range]{
                margin-bottom: 20px;
                -webkit-appearance: none;
                width: 350px;
                height: 10px;
                background: black;
                outline: none;  
                margin-bottom: 20px;
            }
            input[type=range]::-webkit-slider-thumb {
                -webkit-appearance: none;
                height: 45px;
                width: 10px;
                margin-top: -5px; /*使滑块超出轨道部分的偏移量相等*/
                background: blue; 
                border: solid 0.125em rgba(205, 224, 230, 0.5); /*设置边框*/
                box-shadow: 0 .125em .125em #3b4547; /*添加底部阴影*/
            }
            .bank_btn{
                width: 240px;
                height: 130px;
                display: flex;
                flex-direction: column;
                align-items: center;
                p{
                    font-size: 30px;
                    text-align: center;
                    font-weight: 900;
                }
                span{
                    width: 100px;
                    height: 40px;
                    text-align: center;
                    background: #000000;
                    em{
                        width: 45px;
                        height: 30px;
                        display: block;
                        background: #f2a514;
                        cursor: pointer;
                        margin-top: 5px;
                        margin-left: 5px;
                    }
                }
            }
        }
.active2{
    transform: translate(95%);
}
</style>