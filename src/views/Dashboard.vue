<template>
  <div class="outer">
    <div class="container">
      <div class="headerContent">
        <a-input-search placeholder="搜索" style="width: 200px" />
      </div>
      <div class="main">
        <div class="side">
          <div class="side-item">
            <div style="margin-right: 10px;">#</div>
            <div>技术分享</div>
          <!-- 用户成功登陆后的样式 -->
          <div v-if="!messageFlag" class="side-item">
            <div id="user-id">{{ username }}</div>
            <a-button size="small" @click="logout">注销</a-button>
          </div>
          <div class="side-item">
            <div style="margin-right: 10px;">#</div>
            <div>全体</div>
          <!-- 用户没有登陆的样式 -->
          <div v-if="messageFlag" class="side-item">
            <a-input
              v-model:value="username"
              placeholder="请输入用户名"
              size="small"
              style="width: 120px; margin-bottom: 5px"
            />
            <a-button size="small" @click="firstLogin">请先登陆</a-button>
          </div>
        </div>
        <div class="mainContent">
          <div class="chat-message">
            <div class="chat-message-body" v-for="(item, index) in messageArr" :key="index">{{ item }}</div>
            <div
              class="chat-message-body"
              v-for="(item, index) in messageArr"
              :key="index"
            >
              {{ item }}
            </div>
          </div>

          <div class="sendContent">
            <a-input class="sendInput" v-model:value="messageContent" @keyup.enter="sendMessage" placeholder="请输入发送内容" />
            <a-button type="primary" @click="sendMessage">Send</a-button>
            <a-input
              class="sendInput"
              v-model:value="messageContent"
              @keyup.enter="sendMessage"
              placeholder="请输入发送内容"
              :disabled="messageFlag"
            />
            <a-button
              type="primary"
              @click="sendMessage"
              :disabled="messageFlag"
              >Send</a-button
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { ref } from "vue";
// import { IMClient } from 'yzim'

// 收集用户输入框的信息
let messageContent = ref<String>('')
let messageContent = ref<String>("");
// 将用户的所有输入内容整理成一个数组
let messageArr = ref<String[]>([])
let messageArr = ref<String[]>([]);
// 设置一个禁用输入框的标识符
let messageFlag = ref<boolean>(true);
// 收集用户名
let username = ref<String>("");

// 发送信息的事件
function sendMessage() {
  messageArr.value.push(messageContent.value)
  messageContent.value = ''
  messageArr.value.push(messageContent.value);
  messageContent.value = "";
}

// "请先登陆"按钮的处理事件
function firstLogin() {
  messageFlag.value = false;
}

// "注销"按钮的处理事件
function logout() {
  // 清空用户名信息
  username.value = "";
  // 重置messageFlag值
  messageFlag.value = true;
  // 重置收集用户信息的数组
  messageArr.value = [];
}
</script>

<style scoped>
.outer {
  height: 100vh;
  display: grid;
  place-items: center;
}

.container {
  width: 750px;
  height: 560px;
  border: 2px solid black;
  position: relative;
  background-color: #5d3d5e;
}

.headerContent {
  height: 50px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main {
  display: flex;
  flex-direction: row;
}

.side {
  height: 510px;
  width: 150px;
  color: #b8a5b8;
  font-size: 15px;
  display: flex;
  flex-direction: column;
  justify-content: left;
  padding-left: 30px;
}

.side-item {
  display: flex;
  flex-direction: row;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

#user-id {
  font-size: 20px;
  font-weight: bold;
}

.mainContent {
  width: 596px;
  height: 507px;
  padding: 20px;
  background-color: white;
  position: relative;
}

.sendContent {
  display: flex;
  flex-direction: row;
  align-items: center;
  bottom: 5px;
  width: 558px;
  height: 50px;
  position: absolute;
  bottom: 0;
}

.sendInput {
  margin-right: 6px;
}

.chat-message {
  display: flex;
  flex-direction: column;
  padding: 10px;
}

.chat-message-sender {
  font-weight: bold;
}

.chat-message-body {
  margin: 5px 0;
}

.chat-message-time {
  font-size: 12px;
  color: #666;
}
</style></style>
</style>
