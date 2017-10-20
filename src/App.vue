<template>
<div id="app">
  <main>
    <header>
      <div class="logo"><img src="./assets/logo.svg" width="120px"></div>
      <div class="slogan"><div class="title-small">خل نعرف</div><div class="title-large">جميل.</div></div>
    </header>
    <div class="note">
هي حملة لحدث بيهانس الابداعي لهذا السنة. اللي راح يصير يوم ٢٨ من الشهر الحالي. هدف الحملة هو البحث عن الجميل , اللي موجود بداخل كل واحد بينه, موجود بداخل كل شركة او مؤسسة. <br>
كن حملة البحث عن جميـل مفتاحها هو السؤال.السؤال راح يخلينه نعرف التفاصيل اللي توضح الصورة وتختصر الطريق حتى نشوف جميل  .<!--       كلشي حوالينا بيه قصة.. <br>
      وبكل قصة اكو تفاصيل، اكو معاناة وفشل ونجاح، ..اكو جميل..
      حتى نعرف جميل هاي القصة و تترتب تفاصيلها   لازم نسأل
      ليش، شلون، شنو..؟
      السؤال هو الباب اللي يخلينا نعرف كل جميل.
 -->    </div>

    <article>
      <router-view></router-view>
    </article>

  </main>
  <div class="side">
    <div><div class="title-small">خل نعرف</div><div class="title-large">جميل.</div></div>
    <div class="copy">
هي حملة لحدث بيهانس الابداعي لهذا السنة. اللي راح يصير يوم ٢٨ من الشهر الحالي. هدف الحملة هو البحث عن الجميل , اللي موجود بداخل كل واحد بينه, موجود بداخل كل شركة او مؤسسة.<br> <br>كن حملة البحث عن جميـل مفتاحها هو السؤال.السؤال راح يخلينه نعرف التفاصيل اللي توضح الصورة وتختصر الطريق حتى نشوف جميل.
<!--       كلشي حوالينا بيه قصة.. <br>
      وبكل قصة اكو تفاصيل، اكو معاناة وفشل ونجاح، ..اكو جميل..
      حتى نعرف جميل هاي القصة و تترتب تفاصيلها   لازم نسأل
      ليش، شلون، شنو..؟
    السؤال هو الباب اللي يخلينا نعرف كل جميل.     -->

  </div>
    <div class="hashtag">
      <img  src="./assets/hashtag.svg" alt="">
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>



.c {
  width: 80%;
}



html{
  width: 100%;
  height: 100%;
  margin:0 !important;
  padding: 0 !important;
}

* {
  margin:0;
  padding: 0;
}

body {
  margin:0 !important;
  padding: 0 !important;
  font-family: noor;
  margin: 0;
  background-color: #F1F2F2;
  width: 100vw;
  height: 100vh;
  display: flex;
}

#app {
  display: flex;
  width: 100%;
  height: 100%;
}

main {
  flex: 8;
  display: flex;
  flex-direction: column;
}


.note {
  display: none;
  font-family: KohinoorArabic-Regular;
  font-size: 0.7rem;
  text-align: right;
  direction: rtl;
  padding:25px 50px 25px 50px;
  background: #003cc9;
  color: white;
}



.side {
  direction: rtl;
  flex: 4;
  background-color: #003cc9;
  color: white;
  font-family: noor;
  padding: 50px !important;
  position: relative;
}

.side .hashtag {
  position: absolute;
  bottom: 40px;
  font-size: 0.9rem;
  font-weight: bold;
}

.side .title-small {
  font-size: 35px;
  font-family: noor-light;
}


.side .title-large {
  font-size: 80px;
  font-family: noor-bold;
}

.side .copy {
  padding-top:100px;
  font-family: KohinoorArabic-Regular;
  font-size: 0.9rem;
}

header {
  padding-left: 50px;  
  height: 110px;
  display: flex;
  padding-top: 50px;
}


article {
  flex:8;
  height: 100%;
}

footer {
  color:grey !important;
  position: absolute;
  bottom: 50px;
  left: 50px;
  font-family: JannaLT-Regular!important;
  color:black;
  font-size: 14px;
}

.slogan {
  display: none;
  text-align: right;
  direction: rtl;
  color: #003cc9;
}


.slogan .title-small {
  font-size: 35px;
  font-family: noor-light;
}


.slogan .title-large {
  font-size: 80px;
  font-family: noor-bold;
}



@media (max-width: 950px) { 
  .side .title-large {
    font-size: 60px;
  }
  .side .title-small {
    font-size: 25px;
  }

  .side .copy {
    font-size: 0.8rem;
  }
}



@media (max-width: 900px) { 
  .side {
    padding:25px !important;
  }

  header {
    padding-left:25px;
    padding-top:25px;
  }

  footer {
    color: grey;
    position: absolute;
    bottom: 25px;
    left: 25px;
    font-family: JannaLT-Regular!important;
    color:black;
    font-size: 12px;
  }
  
  .side .hashtag {
    position: absolute;
    bottom: 40px;
    font-size: 1rem;
    font-weight: bold;
  }
  

}

@media (max-width: 750px) { 
  .side {
    padding:25px !important;
  }
  .side .title-large {
    font-size: 60px;
  }
  .side .title-small {
    font-size: 25px;
  }
  .side .copy {
    font-size: 0.9rem;
  }
}

@media (max-width: 700px) { 

  footer {
    display: none;
  }
  #app {
    display: block;
    width: 100%;
    height: 100%;
  }
  .side {
    display: none;
  }

.slogan .title-small {
  font-size: 20px;
  font-family: noor-light;
}

.slogan .title-large {
  font-size: 50px;
  font-family: noor-bold;
}


  header {
    padding-left: 25px;  
    height: 110px;
    display: flex;
    padding-top: 25px;
    padding-right: 25px;
  }

  .slogan, .logo {
    flex:1;
  }

  .slogan, .note {
    display: block;
  }
}






@media (max-width: 400px) { 
footer {
  position: absolute;
  bottom: -30px;
  left: calc(50% - 80px);
  font-family: JannaLT-Regular!important;
  color:black;
  font-size: 12px;
}

.slogan .title-small {
  font-size: 20px;
  font-family: noor-light;
}

.slogan .title-large {
  font-size: 50px;
  font-family: noor-bold;
}

header {
  padding-left: 25px;  
  height: 110px;
  display: flex;
  padding-top: 25px;
}


}

</style>
