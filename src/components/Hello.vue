<template>
<div class="main">
  <div class="frame-container">
    <div class="frame">
      <transition name="fade">
        <img v-show="showPlus" src="../assets/add.svg" />
      </transition>
      <input type="file" ref="file" @change="filesChange($event);" accept="image/*" />
      <canvas id="canvas"></canvas>
    </div>
  <div class="cities">
    <div class="city" v-bind:class="{ active: city === 'Baghdad' }" @click="setCity('Baghdad')">بغداد</div>
    <div class="city" v-bind:class="{ active: city === 'Karbala' }" @click="setCity('Karbala')">كربلاء</div>
    <div class="city" v-bind:class="{ active: city === 'Mosul' }" @click="setCity('Mosul')">موصل</div>
    <div class="city" v-bind:class="{ active: city === 'Basra' }" @click="setCity('Basra')">بصرة</div>
  </div>
    <div class="options">
      <div class="reload" @click="reload()"><img src="../assets/reload.svg" width="20px" height="20px"  alt=""/></div>
      <a class="download" id="download" :disabled="canDownload == false">احفظ الصورة منا</a>
    </div>
    <footer>
      developed by 
      <a style="text-decoration: none;  font-weight: bold; color:grey;" href="https://fb.com/solocreativestudio" target="_blank">
        <!-- <img src="./assets/solo.svg" alt=""> -->
        SoloStudio.co
      </a>
    </footer>
  </div>
  <canvas id="canvas2"></canvas>
  <img id="baghdad" src="../assets/baghdad.png" alt="">
  <img id="basra" src="../assets/basra.png" alt="">
  <img id="mosul" src="../assets/mosul.png" alt="">
  <img id="karbala" src="../assets/karbala.png" alt="">
  <!-- <img id="others" src="../assets/iraq.png" alt=""> -->
</div>
</template>
<script>
import {saveAs} from 'file-saver'
import smartcrop from 'smartcrop'
export default {
  mounted: function () {
    const self = this
    // let canvas = document.getElementById('canvas')
    let ctx = document.getElementById('canvas').getContext('2d')
    ctx.font = '20px Georgia'
    ctx.fillText('Hello World!', 400, 400)
    function downloadCanvas (link, canvasId, filename) {
      const canvas = document.getElementById(canvasId)
      canvas.toBlob(blob => saveAs(blob, 'Jameel.png'))
    }
    document.getElementById('download').addEventListener('click', function () {
      if (!self.$data.canDownload) return
      downloadCanvas(this, 'canvas', 'behance.png')
    }, false)
  },
  methods: {
    setCity: function (city) {
      this.$data.city = city
    },
    reload: function () {
      let self = this
      let canvas = document.getElementById('canvas')
      let ctx = document.getElementById('canvas').getContext('2d')
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      self.$data.showPlus = true
    },
    filesChange: function (e) {
      if (!e.target.files.length) {
        return
      }
      let self = this
      self.$data.canDownload = false
      let canvas = document.getElementById('canvas')
      let canvas2 = document.getElementById('canvas2')
      let ctx = document.getElementById('canvas').getContext('2d')
      let ctx2 = document.getElementById('canvas2').getContext('2d')

      let city
      switch (this.$data.city) {
        case 'Baghdad':
          city = document.getElementById('baghdad')
          break
        case 'Basra':
          city = document.getElementById('basra')
          break
        case 'Mosul':
          city = document.getElementById('mosul')
          break
        case 'Karbala':
          city = document.getElementById('karbala')
          break
        case 'Others':
          city = document.getElementById('others')
          break
        default:
          city = document.getElementById('baghdad')
      }

      let options = {debug: false, width: 800, height: 800}
      canvas.width = options.width
      canvas.height = options.height
      canvas2.width = options.width
      canvas2.height = options.height
      var img = new Image()
      img.src = URL.createObjectURL(e.target.files[0])
      img.onload = function () {
        self.$data.canDownload = true
        smartcrop.crop(img, options, function (result) {
          let crop = result.topCrop
          ctx.drawImage(img, crop.x, crop.y, crop.width, crop.height, 0, 0, canvas.width, canvas.height)
          ctx2.drawImage(img, crop.x, crop.y, crop.width, crop.height, 0, 0, canvas2.width, canvas2.height)

          let tileSize = 266.6666666667
          // twin
          ctx.drawImage(canvas2, 0, 0, tileSize, tileSize, tileSize * 2, tileSize, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize * 2, tileSize, tileSize, tileSize, 0, 0, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize * 2, 0, tileSize, tileSize, tileSize, tileSize, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize, tileSize, tileSize, tileSize, tileSize * 2, 0, tileSize, tileSize)
          ctx.drawImage(canvas2, 0, tileSize * 2, tileSize, tileSize, tileSize, 0, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize, 0, tileSize, tileSize, 0, tileSize * 2, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize, tileSize * 2, tileSize, tileSize, tileSize * 2, tileSize * 2, tileSize, tileSize)
          ctx.drawImage(canvas2, tileSize * 2, tileSize * 2, tileSize, tileSize, tileSize, tileSize * 2, tileSize, tileSize)
          ctx.drawImage(city, 0, 0, 319, 319, 0, tileSize * 2, tileSize, tileSize)
          self.$data.showPlus = false
        })
      }
    }
  },
  data () {
    return {
      city: 'Baghdad',
      showPlus: true,
      canDownload: false
    }
  },
  watch: {
    city: function (val) {
      if (this.$data.showPlus === true) {
        return false
      }
      let self = this
      // let canvas = document.getElementById('canvas')
      let ctx = document.getElementById('canvas').getContext('2d')
      let city
      switch (this.$data.city) {
        case 'Baghdad':
          city = document.getElementById('baghdad')
          break
        case 'Basra':
          city = document.getElementById('basra')
          break
        case 'Mosul':
          city = document.getElementById('mosul')
          break
        case 'Karbala':
          city = document.getElementById('karbala')
          break
        case 'Others':
          city = document.getElementById('others')
          break
        default:
          city = document.getElementById('baghdad')
      }
      let tileSize = 266.6666666667
      ctx.drawImage(city, 0, 0, 319, 319, 0, tileSize * 2, tileSize, tileSize)
      self.$data.showPlus = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >
  
html{
  width: 100%;
  height: 100%;
}

* {
  margin: 0;
  padding: 0;
}






  .main {
    font-family: noor;
    /*display: flex;*/
    height: 100%;
    display: flex;
  }

  .options {
    display: flex;
    margin: 30px 0px;
    align-items: space-around;
    align-content: space-around;
    position: absolute;
    left: 50px;
  }



  #canvas {
    width: 100%;
    height: 100%;
  }

  #canvas2, #baghdad, #mosul, #karbala, #others, #basra {
    display: none;
  }
  
  .frame-container{
    flex:1;
    position: relative;
    height: 100%;
  }

  .frame {
    left: 50px;
    position: absolute;
    border:2px  #002E5B dashed;
    height: 300px;
    width: 300px;
    background-color: #DEE4EA;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #476787;
    position: relative;
    text-align: center;
  }


  .frame img {
    margin: 0px;
    padding: 0px;
    width: 50%;
    height: 80%;
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 120px;
  } 

  .cities {
    display: flex;
    flex-direction: column;
    left: 380px;
    position: absolute;
    top:0px;
  }

  .city {
    border:1px solid #E8E8E8;
    background: white;
    border-radius: 25px;
    color:#191919;
    width: 100px;
    height: 35px;
    display: flex;
    margin-bottom: 51px;
    align-items: center;
    justify-content: center;
  }

  .city:hover {
    border:1px solid #0057FF;
    background-color: #0057FF;
    color: white;
    font-weight: bold;
    transition: all 0.3s;
    cursor: pointer;
  }

  .active {
    border:1px solid #0057FF;

    background-color: #0057FF;
    color: white;
    font-weight: bold;
  }

  .desc {
    padding-right: 100px;
    /*padding-left: 100px;*/
    font-family: tahoma;
    font-size:13px;
    color: #0e0e0e;
    flex:1;
    direction: rtl;
    /*margin: auto;*/
    /*padding: 10% 0% 10% 0%;*/
  }
  
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0
}


  .reload {
    border:1px solid #000;
    border-radius: 50%;
    padding:10px;
    display: flex;
    justify-content: center;
    align-items: center;
    /*margin: auto;*/
  }

  .reload:hover {
    border:1px solid #003cc9;
    color: white;
    transition: all 0.3s;
  }

  .download[disabled] {
    border:1px solid #333;
    background: #eee;
    color: #ccc;
  }
  .download[disabled]:hover  {
    border:1px solid #333;
    background: #eee;
    color: #ccc;
  }
  .download:hover {
    cursor: pointer;
    border:1px solid #04AC11;
    background: transparent;
    color: #04AC00;
  }

  .download {
    border:1px solid #04AC00;
    background-color: #04AC00;
    color: white;
    border-radius: 25px;
    margin-left:10px;
    /*margin: auto;*/
    display: flex;
    align-items: center;
    justify-content: space-around;
    /*padding:10px 40px 10px 40px;*/
    width: 180px;
    font-weight: bold;
    text-decoration: none;
    transition: all 0.3s;
  }



  input[type="file"] {
    height: 100%;
    width: 100%;
    position: absolute;
    opacity: 0;
    cursor:pointer;
  }
/*
@media (min-width: 1500px) { 
  .frame{
    width: 500px;
    height: 500px;
  }
  .cities {
    left: 600px;
  }
}

@media (min-width: 1500px) { 
  .frame{
    width: 600px;
    height: 600px;
  }

  .cities {
    left: 700px;
  }
}

@media (min-width: 1700px) { 
  .frame{
    width: 700px;
    height: 700px;
  }

  .cities {
    left: 800px;
  }
}
*/

@media (max-width: 950px) { 
  .frame-container {
    padding: 0px;
  }
}


@media (max-width: 900px) { 
  .frame-container {
    padding: 0px;
  }

  .frame {
    left:25px;
  }

  .cities {
    left: 355px;
  }

  .options {
    left: 25px;
  }


}



@media (max-width: 850px) { 
  .options {
    left: 25px;
  }
  .frame {
    position: absolute;
    left: 25px;
    border:2px  #002E5B dashed;
    height: 250px;
    width: 250px;
    background-color: #DEE4EA;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #476787;
    position: relative;
    text-align: center;
  }
  
  .download {
    width:150px;
  }

  .cities {
    left: 300px;
  }

  .city {
    margin-bottom: 33px;
  }

}

@media (max-width: 750px) { 
  .cities {
    left: 270px;
  }


  .city {
    border:1px solid #E8E8E8;
    border-radius: 25px;
    width: 100px;
    height: 35px;
    display: flex;
    margin-bottom: 18px;
    align-items: center;
    justify-content: center;
    font-size: 11px;
  }

  .city:hover {
    border:1px solid #E8E8E8;
  }
  .frame-container {
    padding:0px;
  }
  .frame {
    border:2px  #002E5B dashed;
    height: 200px;
    width: 200px;
    background-color: #DEE4EA;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #476787;
    position: relative;
    text-align: center;
  }



  .reload {
    border:1px solid #000;
    border-radius: 50%;
    padding:10px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 11px;
    /*margin: auto;*/
  }

  .reload img {
    height: 10px;
    width: 10px;
  }

  .cities {
    padding:0;
    margin:0;
  }



  .frame {
    padding:0;
    margin: 0;
  }


  .download {
    border:1px solid #04AC11;

    border-radius: 25px;
    margin-left:10px;
    /*margin: auto;*/
    display: flex;
    height: 28px;
    font-size: 10px;
    align-items: center;
    justify-content: space-around;
    /*padding:10px 40px 10px 40px;*/
    width: 120px;
    font-weight: bold;
  }



}


@media (max-width: 700px) { 

  .options {
    left: calc(50% - 160px);
  }

  .city {
    width:80px;
    height: 35px;
    font-size: 12px;
  }

  .frame-container {
    padding-top:30px;
  }

  .cities {
    padding-top:30px;
    left: calc(50% + 80px);
  }

  .frame {
    left: calc(50% - 160px);
  }


}

@media (max-width: 400px) { 


  .city {
    width:80px;
    height: 35px;
    font-size: 12px;
  }

  .frame-container {
    padding:0;
    padding-top:30px;
  }

  .cities {
    padding-top:30px;
    left: calc(50% + 70px);
  }

  .frame {
    left: calc(50% - 150px);
  }



  .options {
    display: flex;
    align-items: space-around;
    align-content: space-around;
    position: absolute;
    /*left: calc(50% - 200px);*/
  }





  
  .reload {
    height: 9px;
  }
  .reload img {
    width: 10px;
  }

  .download {
    margin-left:10px;
    /*margin: auto;*/
    display: flex;
    font-size: 10px;
    height: 28px;
    align-items: center;
    justify-content: space-around;
    /*padding:10px 40px 10px 40px;*/
    width: 100px;
    font-weight: bold;
  }




}

</style>
