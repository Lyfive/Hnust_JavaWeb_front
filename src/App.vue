<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Home from "./components/Home.vue"
import StudentList from "./components/StudentList.vue"
import TeacherList from "./components/TeacherList.vue"
</script>
<script>

export default {
  data() {
    return {
      isShow: "none",
      picture: "src/assets/left.png",
      show_id: [true, false, false],
      showing_id: 0,
      user: {
        user_name: "张三",
        user_type: "院级管理员",
        user_num: 123456,
        college: "计算机科学与工程学院",
        isadmin: true,
      },
      system_message: {
        student_count: 1245,
        teacher_count: 1245,
        course_count: 52,
        courses_count: 62,
        class_count: 124,
        major_count: 10,
      },
    }
  },
  methods: {
    hiddle() {
      if (this.isShow == "none") {
        this.isShow = "block";
        this.picture = "src/assets/down.png";
      } else {
        this.isShow = "none";
        this.picture = "src/assets/left.png";
      }
    },
    onStudentList() {
      this.show_id[this.showing_id] = false;
      this.show_id[1] = true;
      this.showing_id = 1;
    },
    onTeacherList() {
      this.show_id[this.showing_id] = false;
      this.show_id[2] = true;
      this.showing_id = 2;
    },
    onHome() {
      this.show_id[this.showing_id] = false;
      this.show_id[0] = true;
      this.showing_id = 0;
    },
  },
  created() {
    axios.get("//127.0.0.1:8080/", {
      id: "LyFive",
    })
      .then(res => {
        console.log(res)
        if (res.status == 200) {
          console.log(this.$data.user)
          this.$data.user = res.data.user;
          this.$data.system_message = res.data.message;
        } else {
          alert("服务请求错误！")
        }
      })
      .catch(err => {
        console.error(err);
      })
  }
}
import axios from 'axios'

</script>
<template>
  <div class="head">
    <div id="head-left" v-on:click="onHome">
      <div id="head-content">
        <span style="font-size:1.5rem;line-height:1.5rem">湖南科技大学</span>
        <span style="font-size:1.125rem;line-height:1.125rem">出卷系统</span>
      </div>
    </div>
    <div id="head-right">
      <div class="system-operator">
        <div class="pip">
          <img src="./assets/head.jpg" alt />
          <span>刷新</span>
        </div>
        <div class="pip">
          <img src="./assets/head.jpg" alt />
          <span>退出</span>
        </div>
      </div>
    </div>
  </div>
  <div class="mid">
    <div class="menu">
      <div class="user">
        <div class="inner-center">
          <div class="head-pic">
            <img src="./assets/head.jpg" alt />
          </div>
          <div class="user-name">
            <span>{{ user.user_type }}</span>
            <span>{{ user.user_name }}</span>
          </div>
        </div>
      </div>
      <div class="inner-menu">
        <ul>
          <li>
            <div class="link" v-on:click="hiddle">
              <img src="./assets/head.jpg" alt class="ico" />
              <span>用户管理</span>
              <img :src="picture" alt class="close" />
            </div>
            <ul :style="{ display: isShow }">
              <li v-on:click="onStudentList">
                <div class="hiddle-menu">学生列表</div>
              </li>
              <li v-on:click="onTeacherList">
                <div class="hiddle-menu">老师列表</div>
              </li>
              <li>
                <div class="hiddle-menu">批量导入</div>
              </li>
              <li>
                <div class="hiddle-menu">发布通知</div>
              </li>
              <li>
                <div class="hiddle-menu">审核注册</div>
              </li>
            </ul>
          </li>
          <li>
            <div class="link">
              <img src="./assets/head.jpg" alt class="ico" />
              <span>课程管理</span>
              <img src="./assets/left.png" alt class="close" />
            </div>
          </li>
          <li>
            <div class="link">
              <img src="./assets/head.jpg" alt class="ico" />
              <span>课程组管理</span>
              <img src="./assets/left.png" alt class="close" />
            </div>
          </li>
          <li>
            <div class="link">
              <img src="./assets/head.jpg" alt class="ico" />
              <span>班级管理</span>
            </div>
          </li>
          <li>
            <div class="link">
              <img src="./assets/head.jpg" alt class="ico" />
              <span>专业管理</span>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div class="content">
      <Home v-show="show_id[0]" :user="user" :message="system_message" />
      <StudentList v-show="show_id[1]" />
      <TeacherList v-show="show_id[2]" />
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  background-color: rgb(241, 242, 243);

  font-family: "SimiHei";
}
#app {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  height: 60rem;
  width: 78rem;
}
.head {
  position: relative;
  width: 100%;
  height: 10%;

  background: radial-gradient(
      ellipse farthest-side at 76% 77%,
      rgba(245, 228, 212, 0.25) 4%,
      rgba(255, 255, 255, 0) calc(4% + 1px)
    ),
    radial-gradient(circle at 76% 40%, #fef6ec 4%, rgba(255, 255, 255, 0) 4.18%),
    linear-gradient(135deg, #ff0000 0%, #000036 100%),
    radial-gradient(ellipse at 28% 0%, #ffcfac 0%, rgba(98, 149, 144, 0.5) 100%),
    linear-gradient(180deg, #cd6e8a 0%, #f5eab0 69%, #d6c8a2 70%, #a2758d 100%);
  background-blend-mode: normal, normal, screen, overlay, normal;
}
#head-left {
  position: absolute;
  left: 0%;
  height: 100%;
  width: 18%;
  cursor: pointer;
}
#head-content {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
#head-right {
  position: absolute;
  right: 0%;
  height: 100%;
  width: 82%;
}
.system-operator {
  position: absolute;
  right: 5%;
  top: 50%;
  transform: translateY(-50%);
  width: 18%;
  display: flex;
  flex-direction: row;
}
.pip {
  width: 100%;
  color: #666;
}
.pip img {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
  display: inline-block;
  width: 1rem;
}
.pip span {
  display: inline-block;
  font-size: 1rem;
  line-height: 1rem;
  margin-left: 0.5rem;
}
.mid {
  position: absolute;
  height: 90%;
  width: 100%;
}
.menu {
  position: absolute;
  bottom: 0%;
  height: 100%;
  width: 18%;
  background-color: #fff;
}

.user {
  position: relative;
  height: 15%;
  width: 100%;
  border-bottom: #999 1px inset;
}

.inner-menu {
  position: relative;
  width: 100%;
  height: 85%;
  font-size: 1.125rem;
}

.inner-menu ul {
  position: relative;
  display: block;
  list-style-type: none;
}
.inner-menu ul li {
  display: list-item;
  margin-top: 3rem;
}
.link {
  position: relative;
  display: block;
  left: 2.3125rem;
  height: 2.3125rem;
  width: 80%;
  color: #666;
  line-height: 2.3125rem;
}
.link span {
  position: absolute;
  bottom: 0;
  display: inline-block;
  height: 100%;
  white-space: nowrap;
  margin-left: 1rem;
}
.link .ico {
  display: inline-block;
  width: 2.3125rem;
}

.link + ul li {
  margin-top: 1rem;
}
.hiddle-menu {
  margin-left: 6rem;
  height: 2rem;
  line-height: 2rem;
  font-size: 1.125rem;
  border-radius: 1.0625rem;
  text-align: center;
  color: #666;
  background-color: #fff;
}
.hiddle-menu:hover {
  color: #000;
  background-color: pink;
  cursor: pointer;
}
.close {
  position: absolute;
  top: 50%;
  right: 1rem;
  transform: translateY(-50%);
  width: 1.5rem;
}
.inner-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
}
.head-pic {
  position: absolute;
  height: 100%;
  width: 30%;
}
.head-pic img {
  position: absolute;
  left: 50%;

  transform: translateX(-50%);
  height: 75%;
  border-radius: 50%;
}
.user-name {
  position: absolute;
  right: 0%;
}
.user-name span {
  margin-top: 1rem;
  display: block;

  font-size: 1.125rem;
  text-align: center;
  color: #000;
}

.content {
  position: absolute;
  left: 18%;
  width: 82%;
  height: 100%;
  background: radial-gradient(
      ellipse farthest-side at 76% 77%,
      rgba(245, 228, 212, 0.25) 4%,
      rgba(255, 255, 255, 0) calc(4% + 1px)
    ),
    radial-gradient(circle at 76% 40%, #fef6ec 4%, rgba(255, 255, 255, 0) 4.18%),
    linear-gradient(135deg, #ff0000 0%, #000036 100%),
    radial-gradient(ellipse at 28% 0%, #ffcfac 0%, rgba(98, 149, 144, 0.5) 100%),
    linear-gradient(180deg, #cd6e8a 0%, #f5eab0 69%, #d6c8a2 70%, #a2758d 100%);
  background-blend-mode: normal, normal, screen, overlay, normal;
}
</style>