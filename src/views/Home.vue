<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { getUserName } from "@/api";
import { ref } from "vue";

const username = ref("");
const password = ref("");
const usernameError = ref("");
const passwordError = ref("");
const pageData = ref("");

const onSubmit = () => {
  usernameError.value = "";
  passwordError.value = "";

  // 检查账号
  if (!username.value) {
    usernameError.value = "请输入账号";
    return;
  }
  if (!username.value.match(/^[a-zA-Z0-9]{5,8}$/)) {
    usernameError.value = "账号为5-8位数字和字母";
    return;
  }

  // 检查密码
  if (!password.value) {
    passwordError.value = "请输入密码";
    return;
  }
  if (!password.value.match(/^[a-zA-Z0-9]{5,12}$/)) {
    passwordError.value = "密码为5-12位数字和字母";
    return;
  }

  // 执行登录操作
  console.log("登录", username.value, password.value);
  // 这里可以发送请求到后端进行验证
  // getUserName().then((res) => {
  //   pageData.value = res.data;
  //   console.log("res.data", res.data);
  // });
  const { data: pageData } = useRequest(getUserName);
  console.log(pageData);
};
const login = () => {
  window.location.href = "/test";
};
</script>
<template>
  <div class="father">
    <div class="left">
       <a-carousel autoplay>
        <div><img src="../../public/images/1.png" width="100%"/></div>
        <div><img src="../../public/images/2.png"  width="100%"/></div>
        <div><img src="../../public/images/3.png"  width="100%"/></div>
      </a-carousel>
    </div>

    <form @submit.prevent="onSubmit" class="right">
      <h1 class="text" style="margin-top: 10px;">登录，即刻创造您的应用</h1>
      <div class="qqq">
        <input
          class="username"
          type="text"
          id="username"
          v-model="username"
          placeholder="账号 ："
          required
          pattern="[a-zA-Z0-9]{5,8}"
        />
        <span v-if="usernameError" class="error">{{ usernameError }}</span>
      </div>
      <div class="qqq">
        <input
          class="password"
          type="password"
          id="password"
          v-model="password"
          placeholder="密码 ："
          required
          pattern="[a-zA-Z0-9]{5,12}"
        />
        <span v-if="passwordError" class="error">{{ passwordError }}</span>
      </div>
      <div>
        <inputd
          type="checkbox"
          id="checkbox"
          v-model="checked"
          class="checkbox"
          style="margin-top: 20px;"
        />我已阅读并同意<a href="#">服务协议</a>和<a href="#">隐私政策</a>
      </div>

      <div class="dl" type="submit" @click="login">登录</div>
      <div style="margin-left: 270px;margin-top: 10px;">还未注册?<a href="#">立即注册</a></div>
    </form>
  </div>
</template>

<style>
* {
  padding: 0;
  margin: 0;
}
.father {
  display: flex;
}
.left {
  /* width: 1152px; */
  width: 30%;
  height: 700px;
  overflow: hidden;
}
.left-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.right {
  /* width: 1748px; */
  width: 60%;
  margin-top: 10px;
}
.text {
  padding-top: 200px;
  margin-left: 180px;
}
.username {
  width: 160px;
}
.password {
  width: 160px;
}
.qqq {
  padding-left: 260px;
  margin-top: 10px;
}
.dl {
  width: 300px;
  height: 55px;
  line-height: 60px;
  background-color: rgb(7, 14, 226);
  text-align: center;
  color: azure;
  border-radius: 6px;
  margin-left: 200px;
  margin-top: 20px;
  font-size: 26px;
}
.checkbox {
  margin-left: 220px;
}
:deep(.slick-slide) {
  text-align: center;
  height: 160px;
  line-height: 160px;
  background: #364d79;
  overflow: hidden;
}
:deep(.slick-slide h3) {
  color: #fff;
}
</style>
