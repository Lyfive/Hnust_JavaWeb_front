<script setup>
import { ref } from "vue"
defineProps({
  user: {},
  message: {},
})

</script>

<template>
  <div class="box">
    <div class="header">
      <div class="left">
        <div class="inner-head">
          <div class="location-box">
            <span style="font-size:1.75rem;display:block;color:#333333;">系统信息</span>
            <span style="font-size:1.3125rem;display:block;color:#999999;">本日系统信息内容已经更新</span>
          </div>
        </div>
        <div class="message">
          <div class="message-box">
            <div class="line">
              <div class="col">
                <span>学生账号数</span>
                <span>{{message.student_count}}</span>
              </div>
              <div class="col">
                <span>老师账号数</span>
                <span>{{message.teacher_count}}</span>
              </div>
              <div class="col">
                <span>课程数</span>
                <span>{{message.course_count}}</span>
              </div>
            </div>
            <div class="line">
              <div class="col">
                <span>课程组数</span>
                <span>{{message.courses_count}}</span>
              </div>
              <div class="col">
                <span>班级数</span>
                <span>{{message.class_count}}</span>
              </div>
              <div class="col">
                <span>专业数</span>
                <span>{{message.major_count}}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="right">
        <div class="inner-head">
          <div class="location-box">
            <span style="font-size:1.75rem;display:block;color:#333333;">管理员信息</span>
            <span style="font-size:1.3125rem;display:block;color:#999999;">本日管理员信息内容已经更新</span>
          </div>
        </div>
        <div class="head-picture">
          <img src="../assets/head.jpg" alt height="100%" />
        </div>
        <div class="inner-footer">
          <div
            class="flex-box"
            style="font-family:'MicrosoftYaHei-Bold';font-size:1.875rem;text-align:center;line-height:4rem;"
          >{{ user.user_name }}</div>
          <div class="flex-box">
            <div class="inner-footer-content">
              <img src="../assets/head.jpg" />
              <span>{{user.user_num}}</span>
            </div>
          </div>
          <div class="flex-box">
            <div class="inner-footer-content">
              <img src="../assets/head.jpg" style="width:2rem;" />
              <span>{{user.college}}</span>
            </div>
          </div>
          <div class="flex-box">
            <div class="inner-footer-content">
              <span style="display:inline-block;">********</span>

              <a href="#" id="password-change">修改密码</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="inner-head">
        <div class="location-box">
          <span style="font-size:1.75rem;display:block;color:#333333;">管理权限</span>
          <span style="font-size:1.3125rem;display:block;color:#999999;">本日管理权限内容已经更新</span>
        </div>
      </div>
      <div class="footer-menu">
        <div class="footer-inner-menu">
          <div class="flex-menu-box">
            <img src="../assets/head.jpg" alt />
            <span>用户管理</span>
          </div>
          <div class="flex-menu-box">
            <img src="../assets/head.jpg" alt />
            <span>课程管理</span>
          </div>
          <div class="flex-menu-box">
            <img src="../assets/head.jpg" alt />
            <span>课程组管理</span>
          </div>
          <div class="flex-menu-box">
            <img src="../assets/head.jpg" alt />
            <span>班级管理</span>
          </div>
          <div class="flex-menu-box">
            <img src="../assets/head.jpg" alt />
            <span>专业管理</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
a {
  text-decoration: none;
}
.box {
  position: absolute;
  top: 1rem;
  left: 4rem;
  height: 100%;
  width: 90%;
}
.header {
  position: relative;
  height: 53%;
  width: 100%;
}
.left {
  position: absolute;
  left: 0%;
  height: 100%;
  width: 60%;
  background-color: #fff;
}
.right {
  position: absolute;
  right: 0%;
  height: 100%;
  width: 38%;
  background-color: #fff;
}
.footer {
  position: relative;
  margin-top: 1rem;
  width: 100%;
  height: 40%;
  background-color: #fff;
}

.inner-head {
  position: relative;
  width: 100%;
  height: 7rem;
  border-bottom: #999 1px solid;
}

.location-box {
  position: absolute;
  top: 1rem;
  left: 2rem;
}

.message {
  position: relative;
  width: 100%;
  height: 75%;
}

.message-box {
  position: absolute;
  left: 14%;
  top: 14%;
  width: 72%;
  height: 72%;

  display: flex;
  flex-direction: column;
}

.line {
  position: relative;
  display: flex;
  height: 100%;
  flex-direction: row;
}

.col {
  position: relative;
  width: 100%;
}

.col span {
  display: block;
  text-align: center;
}
.col :first-child {
  font-size: 1.3125rem;
  color: #666666;
  margin-bottom: 1rem;
}
.col :last-child {
  font-size: 2.25rem;
  font-family: "MicrosoftYaHei-Bold";
  color: #333333;
}
.head-picture {
  position: relative;
  width: 100%;
  height: 15%;
}
.head-picture img {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 50%;
}

.inner-footer {
  position: relative;
  height: 60%;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.inner-footer .flex-box {
  position: relative;
  height: 100%;
}
.inner-footer-content {
  position: absolute;
  left: 30%;
  height: 2rem;
  width: 70%;
}
.inner-footer-content img {
  position: absolute;
  width: 2rem;
}

.inner-footer-content span {
  position: absolute;
  left: 3rem;
  height: 2rem;
  line-height: 2rem;
  font-size: 1rem;
  white-space: nowrap;
  color: #666666;
}
#password-change {
  position: absolute;
  display: inline-block;
  right: 3rem;
  font-size: 1rem;
  color: #3399ff;
}
.footer-menu {
  position: relative;
  width: 100%;
  height: 67.5%;
}
.footer-inner-menu {
  position: absolute;
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 80%;
}
.flex-menu-box {
  position: relative;
  width: 100%;
  margin-top: 1rem;
  margin-left: 1rem;

  margin-right: 1rem;
  background-color: rgb(235, 151, 168);
}

.flex-menu-box img {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  height: 50%;
}
.flex-menu-box span {
  position: absolute;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
  color: #fff;
  font-size: 1rem;

  white-space: nowrap;
}
</style>
