<script setup>
import axios from 'axios';
import pagination from './pagination.vue';
</script>
<script>
function student(id, account, name, password, school, operation) {
  this.id = id;
  this.account = account;
  this.name = name;
  this.password = password;
  this.school = school;
  this.operation = operation;
}

export default {
  data() {
    return {
      major: "",
      account: "",
      student_name: "",
      classname: "",
      st: 0,
      change: true,
      check_list: [],
      all_student: [],
    }
  },
  methods: {
    find() {
      axios.get("http://127.0.0.1:8080/student/find", {
        params: {
          major: this.major,
          account: this.account,
          name: this.student_name,
          classname: this.classname,
        }
      })   
        .then(res => {
          console.log(res)
          this.all_student = res.data.data;
          while (this.all_student.length % 4 != 0) {
            this.all_student.push(new student(0, "", "", "", "", ""));
          }
          for (let i = 0; i < 4; i++) {
            this.all_student.push(new student(0, "", "", "", "", ""));
          }
          this.init_to_check_list(this.all_student.length)
        })
        .catch(err => {
          console.error(err);
        })
    },
    del() {
      let cnt = 0;
      for (let i = 0; i < this.check_list.length; i++) {
        this.all_student[i - cnt] = this.all_student[i];
        if (this.check_list[i] && this.all_student[i].id > 0) {
          axios.delete("http://127.0.0.1:8080/student/delete", {
            params: {
              id: this.all_student[i].id,
            }
          }).then(res => {
            console.log(res)
          })
            .catch(err => {
              console.error(err);
            });
          this.check_list[i] = false;
          cnt++;
        }
      }


    },
    check(index) {
      this.check_list[this.st + index] = !this.check_list[this.st + index];
      console.log(this.check_list[this.st + index])
      return this.check_list[this.st + index];
    },
    init_to_check_list(len) {
      for (var i = 0; i < len; i++) {
        this.check_list.push(false);
      }
    },
    getPage(data) {
      console.log(data)
      if (4 * (data - 1) < this.all_student.length) {
        this.st = 4 * (data - 1);
      } else {
        this.st = this.all_student.length - 4;
      }
      console.log(this.st)
      console.log(this.all_student.length)
    }
  },
  computed: {
    student_list() {
      return this.all_student.slice(this.st, this.st + 4);
    },
  },
  created() {
    for (var i = 0; i < 4; i++) {
      this.student_list.push(new student(0, "", "", "", "", ""))
    }
  }
}
</script>
<template>
  <div class="box">
    <div class="inner-head">
      <div class="location-box">
        <span style="font-size:1.75rem;display:block;color:#333333;">学生列表</span>
        <span style="font-size:1.3125rem;display:block;color:#999999;">本日学生列表内容已经更新</span>
      </div>
    </div>
    <div class="mid">
      <div class="input-box">
        <div class="line">
          <div class="row">
            <div class="input-center-box">
              <label for="account">账号:</label>
              <input type="text" id="account" v-model="account" />
            </div>
          </div>
          <div class="row">
            <div class="input-center-box">
              <label for="name">姓名:</label>
              <input type="text" id="name" v-model="student_name" />
            </div>
          </div>
        </div>
        <div class="line">
          <div class="row">
            <div class="input-center-box">
              <label for="major">专业:</label>
              <input type="text" id="major" v-model="major" />
            </div>
          </div>
          <div class="row">
            <div class="input-center-box">
              <label for="classname">班级:</label>
              <input type="text" id="classname" v-model="classname" />
            </div>
          </div>
        </div>
      </div>
      <div class="button-box">
        <div class="line">
          <div class="row">
            <button id="find" v-on:click="find">查询</button>
          </div>

          <div class="row">
            <button id="reset">重置</button>
          </div>
        </div>
        <div class="line">
          <div class="row">
            <button id="delete" @click="del">删除</button>
          </div>

          <div class="row"></div>
        </div>
      </div>
    </div>
    <div class="table">
      <div class="inner-table">
        <div class="line" id="title">
          <div class="row">
            <span>账号</span>
          </div>
          <div class="row">
            <span>姓名</span>
          </div>
          <div class="row">
            <span>密码</span>
          </div>
          <div class="row">
            <span>学校</span>
          </div>
          <div class="row">
            <span>操作</span>
          </div>
        </div>
        <div
          class="line"
          v-for="(student, index) in student_list"
          v-bind:key="index"
          :class="{ checked: check_list[st + index] }"
          @click="check(index)"
        >
          <div class="row">
            <span>{{ student.account }}</span>
          </div>
          <div class="row">
            <span>{{ student.name }}</span>
          </div>
          <div class="row">
            <span>{{ student.password }}</span>
          </div>
          <div class="row">
            <span>{{ student.school }}</span>
          </div>
          <div class="row">
            <span>{{ student.operation }}</span>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <pagination id="page" @getPage="getPage" />
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
  height: 95%;
  width: 90%;
  background-color: #fff;

  box-shadow: -0.1rem -0.1rem 0.1rem rgb(253, 240, 196);
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
.mid {
  position: relative;
  width: 100%;
  height: 15%;
  margin-top: 1.5rem;
}
.table {
  position: relative;
  height: 44.5%;
  width: 100%;
}
.inner-table {
  position: relative;
  left: 3rem;
  height: 100%;
  width: 90%;

  display: flex;
  flex-direction: column;
}
.inner-table .line {
  border-bottom: #999 0.1rem solid;
}
.checked {
  background-color: pink;
}
#title {
  background-color: #ccc;
  border: none;
}
.inner-table span {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 1.25rem;
  color: #000;
}
.footer {
  position: relative;
  height: 22.7%;
  width: 100%;
}
.input-box {
  position: absolute;
  left: 3rem;
  width: 60%;
  height: 75%;
  display: flex;
  flex-direction: column;
}
.line {
  position: relative;
  height: 100%;
  display: flex;
  flex-direction: row;
}

.row {
  position: relative;
  width: 100%;
  display: block;
}

.input-center-box {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  height: 1.75rem;
  font-size: 1.125rem;
  line-height: 1.75rem;
}
.input-center-box input {
  position: absolute;
  left: 3rem;
  height: 1.75rem;
  width: 12rem;
  border-radius: 0.5rem;
  border: #999 0.0625rem solid;
  padding-left: 0.5rem;
  font-size: 1.25rem;
}
.button-box {
  position: absolute;
  display: flex;
  flex-direction: column;
  left: 65%;
  height: 75%;
  width: 25%;
}

.button-box button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  height: 2.5rem;
  width: 6.25rem;
  border-radius: 0.5rem;
  border: none;
  font-size: 1.25rem;
  color: #fff;
}
#find {
  background-color: rgb(255, 173, 175);
}
#delete {
  background-color: red;
}
#reset {
  color: #000;
}
#page {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
