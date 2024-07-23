<template>
  <div class="box">
    <div class="con">
      <!-- 左部插件 -->
      <MyLeft
      :list="list"
      :isVoice="isVoice"
      :isbank="isbank"
      :volume="volume"
      @lookId="handleLookId"
      ></MyLeft>
      <!-- 右部插件 -->
      <MyRight
      :id="id"
      :isVoice="isVoice"
      @voiceOnOff="handlevoiceOnOff"
      @musicStyle="handlemusicStyle"
      @changeVolume="handlechangeVolume"
      ></MyRight>
    </div>
  </div>
</template>

<script>
import MyLeft from './components/MyLeft.vue';
import MyRight from './components/MyRight.vue';
import axios from 'axios'

export default {
  data() {
    return {
      list: [],
      id: '',
      isVoice: true,
      isbank: false,
      volume:1,
    }
  },
  methods: {
    handleLookId(id){
      this.id = id;
    },
    handlevoiceOnOff(val){
      this.isVoice =val
    },
    handlemusicStyle(val){
      this.isbank = val
    },
    handlechangeVolume(val){
      this.volume = val
    }
  },
  components: {
    MyLeft,
    MyRight
  },
  async created(){
    const res = await axios.get('https://zyxcl.xyz/exam_api/music/list')
    this.list = res.data.value
    console.log('created',this.list)
  },
  mounted(){
    console.log('mounted',this.volume)
  }
}
</script>

<style lang="scss">
.box{
    width: 1000px;
    height: 600px;
    margin: 95px auto;
    background: #b3b3b3;
    border: 8px solid #f2a514;
    .con{
      display: flex;
    }
}
</style>
