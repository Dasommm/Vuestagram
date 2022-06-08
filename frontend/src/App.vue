<template>
  <div class="header">
    <ul class="header-button-left">
      <li @click="step = 0">Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 1" @click="step++">Next</li>
      <li v-if="step == 2" @click="publish">Upload</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <ContainerBox :dataList="dataList" :step="step" :tempUrl="tempUrl" @write="tempContent = $event" />
  <!-- <button @click="more">더보기</button> -->

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <!-- 파일 여러개 올리고 싶을때 type="file" 앞에 multiple만 붙인다.
      이미지만 선택하게 하려고 한다면 accept="image/*" 하면 되는데 근본적이지 않음. 
      필요하면 찾아볼것 -->
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>

  <!-- <div v-if="step == 0">내용0</div>
  <div v-if="step == 1">내용1</div>
  <div v-if="step == 2">내용2</div>
  <button @click="step = 0">버튼0</button>
  <button @click="step = 1">버튼1</button>
  <button @click="step = 2">버튼2</button> -->
</template>

<script>
import ContainerBox from "./components/ContainerBox";
import dataList from "./assets/dataList.js";
import axios from "axios";

//console.log(dataList);

export default {
  name: "App",
  data() {
    return {
      moreClick: 0,
      dataList: dataList,
      step: 0, //현재페이지 0이면 post, 1이면 필터화면, 2면 글쓰는 화면
      tempUrl: "",
      tempContent: "",
    };
  },
  components: { ContainerBox },
  methods: {
    more() {
      // axios.post('URL') 원하는 데이터 전송
      //요청 성공시 .then()안에 코드가 실행.
      //실패시에는 .catch()안에 코드가 실행됨.
      axios
        .get("https://codingapple1.github.io/vue/more" + this.moreClick + ".json")
        .then((result) => {
          console.log(result.data);
          this.dataList.push(result.data);
        })
        .catch((err) => {
          console.log(err);
        });
      this.moreClick++;
      if (this.moreClick > 2) {
        alert("더이상 없습니다");
      }
    },
    upload(e) {
      //e는 event와 관련한 변수
      let tempFile = e.target.files;
      this.tempUrl = URL.createObjectURL(tempFile[0]); //업로드한 이미지의 URL을 생성해준다.
      console.log(this.tempUrl);
      this.step = 1;
    },
    publish() {
      //추가된 게시물을 dataList에 추가해준다.
      var tempPost = {
        name: "Add Test",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.tempUrl,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.tempContent,
        filter: "perpetua",
      };
      this.dataList.unshift(tempPost); //array에 추가하는 문법
      this.step = 0;
    },
  },
};
</script>

<style>
/*
@import 'style.css'와 같이 외부에서 가져올 수 있다. 
*/
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
