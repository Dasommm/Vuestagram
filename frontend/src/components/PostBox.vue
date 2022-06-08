<template>
  <div class="post">
    <div class="post-header">
      <div class="profile" :style="{ backgroundImage: `url(${dataList.userImage})` }"></div>
      <span class="profile-name">{{ dataList.name }}</span>
    </div>
    <div class="post-body" :style="{ backgroundImage: `url(${dataList.postImage})` }"></div>
    <div class="post-content">
      <p>{{ dataList.likes }} Likes</p>
      <p>
        <strong>{{ dataList.name }}</strong> {{ dataList.content }}
      </p>
      <p class="date">{{ dataList.date }}</p>
    </div>
  </div>
</template>

<script>
import dataList from "../assets/dataList";
console.log(dataList);
export default {
  data() {
    return {};
  },
  props: {
    dataList: Object,
  },
};
</script>

<style>
.post {
  width: 100%;
}
.profile {
  background-image: url("https://placeimg.com/100/100/arch");
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  background-image: url("https://placeimg.com/640/480/animals");
  height: 450px;
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
}
</style>
