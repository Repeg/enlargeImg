<template>
  <div class="layout-mgt-30">
    <div class='tip' v-show='tip1'>不能再放大了哦！</div>
    <div class='tip' v-show='tip2'>不能再缩小了哦！</div>
    <div class='tip' v-show='tip3'>前面已经没有了！</div>
    <div class='tip' v-show='tip4'>已经是最后一张了哦！</div>
    <div v-for="(item,index) in data">
        <img :src="item.path" @click="enlargeImg(item.path,index)" class="smallImg">
    </div>
    <div v-if="largeContainer" class="largeContainer">
      <div class="fl sideClick">
        <div @click="prevImg">
          <img src="../assets/left_arrow.png" class="clickArrow">
        </div>
      </div>
      <div class="box-image-wrapper fl">
        <img :src="enlargeImgUrl" class='mainImg' :style='{maxWidth: mWidth,width: widthImg}' :class="{rotate90:rotate==1,rotate180:rotate==2,rotate270:rotate==3,rotate0:rotate==0}" @click="enSmallImg"><br>
      </div>
      <div class="fr sideClickR">
        <div @click="nextImg">
          <img src="../assets/right_arrow.png" class="clickArrow">
        </div>
      </div>
    </div>
    <div class='bottom' v-if="largeContainer">
      <img src="../assets/large.png" class='rotate' @click="largeImg">
      <img src="../assets/small.png" class='rotate' @click="smallImg">
      <img src="../assets/circle.png" class='rotate' @click="rotateImg">
      <img src="../assets/circle1.png" class='rotate' @click="rotateImgBack">
    </div>
  </div>
</template>

<script>
export default {
  name: 'enlargeImg',
  data(){
    return{
      largeContainer:false,
      enlargeImgUrl:'',
      imageIndex:'',
      preImgUrl:'',
      nextImgUrl:'',
      rotate:0,
      tip1: false,
      tip2: false,
      tip3: false,
      tip4: false,
      mWidth: '50%',
      widthImg: '50%'
    }
  },
  props:{
    "data":{
      type:Array,
    }
  },
  watch:{
    tip1(res){

    }
  },
  methods:{
    enlargeImg(url,i){
      this.largeContainer=true
      this.enlargeImgUrl = url
      this.imageIndex = i
    },
    rotateImg(){
      if(this.rotate==0){
        this.rotate=1;
      }else if(this.rotate==1){
        this.rotate=2;
      }else if(this.rotate==2){
        this.rotate=3;
      }else{
        this.rotate=0;
      }
    },
    rotateImgBack(){
      if(this.rotate==0){
        this.rotate=3;
      }else if(this.rotate==1){
        this.rotate=0;
      }else if(this.rotate==2){
        this.rotate=1;
      }else{
        this.rotate=2;
      }
    },
    largeImg(){
      if(this.mWidth=='100.0%'){
        this.tip1 = true
        setTimeout(()=>{
          this.tip1 = false
        },1500)
      }else{
        this.mWidth = parseFloat(this.mWidth) + 10
        this.widthImg = parseFloat(this.widthImg) + 10
        this.mWidth=Number(this.mWidth).toFixed(1)
        this.mWidth+="%"
        this.widthImg=Number(this.widthImg).toFixed(1)
        this.widthImg+="%"
      }
    },
    smallImg(){
      if(this.mWidth=='10.0%'){
        this.tip2 = true
        setTimeout(()=>{
          this.tip2 = false
        },1500)
      }else{
        this.mWidth = parseFloat(this.mWidth) - 10
        this.widthImg = parseFloat(this.widthImg) - 10
        this.mWidth=Number(this.mWidth).toFixed(1)
        this.mWidth+="%"
        this.widthImg=Number(this.widthImg).toFixed(1)
        this.widthImg+="%"
      }
    },
    enSmallImg(){
      this.largeContainer=false
      this.mWidth = '50%'
      this.widthImg = '50%'
      this.rotate = 0;
    },
    prevImg(){
      this.mWidth = '50%'
      this.widthImg = '50%'
      if(this.imageIndex==0){
        this.tip3 = true
        setTimeout(()=>{
          this.tip3 = false
        },1500)
      }else{
        this.enlargeImgUrl = this.data[this.imageIndex-1].path
        this.imageIndex = this.imageIndex-1
      }
    },
    nextImg(){
      this.mWidth = '50%'
      this.widthImg = '50%'
      if(this.imageIndex==this.data.length-1){
        this.tip4 = true
        setTimeout(()=>{
          this.tip4 = false
        },1500)
      }else{
        this.enlargeImgUrl = this.data[this.imageIndex+1].path
        this.imageIndex = this.imageIndex+1
      }
    }
  }
}
</script>

<style>
.largeContainer{
  top: 0;
  right: 0;
  left: 0;
  position: fixed;
  width: 100%;
  height: -webkit-fill-available;
  height: fill-available;
  background-color: rgba(55,55,55,0.9);
  z-index: 22;
  overflow: auto;
  box-sizing: border-box;
}
.box-image-wrapper{
  top: 0;
  position: fixed;
  width: 100%;
  height: -webkit-fill-available;
  height: fill-available;
  z-index: 33;
  text-align: center;
  overflow-y: auto;
  display: flex;
  padding-bottom: 60px;
}
.layout-mgt-30{
  margin-top: 30px;
}
.mainImg{
  cursor: pointer;
  position: relative;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}
.largeImg60{
  max-width: 60%;
  width: 60%;
}
.largeImg70{
  max-width: 70%;
  width: 70%;
}
.largeImg80{
  max-width: 80%;
  width: 80%;
}
.largeImg90{
  max-width: 90%;
  width: 90%;
}
.largeImg100{
  max-width: 100%;
  width: 100%;
}
.smallImg{
  height:80px;
  width:80px;
  float:left;
  margin-left: 20px;
  cursor: pointer;
}
.sideClick{
  height:100%;
  width:6%;
  cursor: pointer;
}
.sideClickR{
  height:100%;
  width:6%;
  cursor: pointer;
}
.sideClick div{
  position: fixed;
  z-index: 44;
  background-color: rgba(40,40,40,0.8);
  height: 75px;
  width: 60px;
  top: 0;
  bottom: 0;
  margin: auto;
  margin-left: 20px;
}
.sideClickR div{
  position: fixed;
  z-index: 44;
  background-color: rgba(40,40,40,0.8);
  height: 75px;
  width: 60px;
  top: 0;
  bottom: 0;
  margin: auto;
  right: 20px;
}
.clickArrow{
  width:50%;
  margin-top: 10px;
}
.rotate0{
  transform: rotate(0deg); 
}
.rotate90{
  transform: rotate(90deg); 
}
.rotate180{
  transform: rotate(180deg); 
}
.rotate270{
  transform: rotate(270deg); 
}
.fr{
  float: right;
}
.fl{
  float:left;
}
.rotate{
  height: 30px;
  cursor: pointer;
}
.rotateR{
  height: 30px;
  cursor: pointer;
  transform:rotateY(180deg);
}
.bottom{
  width: 100%;
  position:fixed;
  z-index:55;
  bottom:0;
  padding: 15px 0;
  margin-left: -8px;
  background-color: #464646;
}
.tip{
  position: fixed;
  top: 200px;
  margin: auto;
  left: 0;
  right: 0;
  background-color: #888;
  color: #fff;
  height: 30px;
  font-size: 14px;
  line-height: 30px;
  width: 150px;
  text-align: center;
  padding: 0 5px;
  border-radius: 6px;
  z-index: 100;
}
</style>
