<script setup>
import pagination from './pagination.vue';
</script>
<script>
  export default{
    data(){
      return{
        major:"",
        account : "",
        student_name:"",
        classname : "",
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
            <button id="find">查询</button>
          </div>

          <div class="row">
            <button id="reset">重置</button>
          </div>
        </div>
        <div class="line">
          <div class="row">
            <button id="delete">删除</button>
          </div>

          <div class="row"></div>
        </div>
      </div>
    </div>
    <div class="table">
      <div class="inner-table">
        <div class="line" id="title">
          <div class="row"> <span>账号</span>  </div>
          <div class="row"> <span>姓名</span>  </div>
          <div class="row"> <span>密码</span>  </div>
          <div class="row"> <span>学校</span>  </div>
          <div class="row"> <span>操作</span>  </div>
        </div>
        <div class="line">
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
        </div>
        <div class="line">
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
        </div>
        <div class="line">
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
          <div class="row"></div>
        </div>
      </div>
    </div>
    <div class="footer">
      <pagination id="page" />
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
.inner-table .line{
  border-bottom: #999 .1rem solid;
}
#title{
  background-color: #ccc;
  border: none;
}
.inner-table span{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  font-size: 1.25rem;
  color:#000;
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
#page{
  position: absolute;
  top: 50%;
  left: 50%;
  transform:translate(-50%,-50%);
}
</style>
