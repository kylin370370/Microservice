<template>
  <div class="my-login-box">
    <h2>Login</h2>
    <form id="loginForm">
      <div class="user-box">
        <input type="text" id="username" required="">
        <label>Username</label>
      </div>
      <div class="user-box">
        <input type="text" id="password" required="">
        <label>Password</label>
      </div>
      <a href="#" id ="submit">
        <span></span>
        <span></span>
        <span></span>
        <span></span> Submit
      </a>

      <a  href="/register" >
        <span></span>
        <span></span>
        <span></span>
        <span></span> Register
      </a>
      &nbsp
      <div>

      </div>
      <a href="/home">
        <span></span>
        <span></span>
        <span></span>
        <span></span> 直接进入主页
      </a>

    </form>
  </div>

</template>
<script>
import axios from 'axios';

export default {
  name: 'LoginPage',
  mounted() {
    const submitButton = document.getElementById('submit');
    if (submitButton) {
      submitButton.addEventListener('click', this.handleSubmit);
    }
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      // 处理提交逻辑
      const username = document.getElementById('username').value;
      const password = document.getElementById('password').value;
      console.log('Username:', username, 'Password:', password);



      axios.post('/login', {
        username: username,
        password: password
      },)
          .then(response => {
            if (response.data.code === 200) {
              this.$router.push('/home');
            } else {
              alert('用户名或密码有误');
            }
          })
          .catch(error => {
            console.error('Error:', error);
            alert('登录过程中出现问题');
          });
    }
  },
  beforeDestroy() {
    const submitButton = document.getElementById('submit');
    if (submitButton) {
      submitButton.removeEventListener('click', this.handleSubmit);
    }
  }
};
</script>
<style>
html {
  height: 100%;
}
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  background: linear-gradient(#141e30, #243b55);
}
.my-login-box {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  padding: 40px;
  transform: translate(-50%, -50%);
  background: rgba(0, 0, 0, .5);
  box-sizing: border-box;
  box-shadow: 0 15px 25px rgba(0, 0, 0, .6);
  border-radius: 10px;
}
.my-login-box h2 {
  margin: 0 0 30px;
  padding: 0;
  color: #fff;
  text-align: center;
}
.my-login-box .user-box {
  position: relative;
}
.my-login-box .user-box input {
  width: 100%;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  margin-bottom: 30px;
  border: none;
  border-bottom: 1px solid #fff;
  outline: none;
  background: transparent;
}
.my-login-box .user-box label {
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  pointer-events: none;
  transition: .5s;
}
.my-login-box .user-box input:focus ~ label,
.my-login-box .user-box input:valid ~ label {
  top: -30px;
  left: 0;
  color: #03e9f4;
  font-size: 12px;
}
.my-login-box form a {
  position: relative;
  display: inline-block;
  padding: 10px 20px;
  color: #03e9f4;
  font-size: 16px;
  text-decoration: none;
  text-transform: uppercase;
  overflow: hidden;
  transition: .5s;
  margin-top: 40px;
  letter-spacing: 4px
}
.my-login-box a:hover {
  background: #03e9f4;
  color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 5px #03e9f4, 0 0 25px #03e9f4, 0 0 50px #03e9f4, 0 0 100px #03e9f4;
}
.my-login-box a span {
  position: absolute;
  display: block;
}
.my-login-box a span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #03e9f4);
  animation: btn-anim1 1s linear infinite;
}
@keyframes btn-anim1 {
  0% {
    left: -100%;
  }
  50%,
  100% {
    left: 100%;
  }
}
.my-login-box a span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #03e9f4);
  animation: btn-anim2 1s linear infinite;
  animation-delay: .25s
}
@keyframes btn-anim2 {
  0% {
    top: -100%;
  }
  50%,
  100% {
    top: 100%;
  }
}
.my-login-box a span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(270deg, transparent, #03e9f4);
  animation: btn-anim3 1s linear infinite;
  animation-delay: .5s
}
@keyframes btn-anim3 {
  0% {
    right: -100%;
  }
  50%,
  100% {
    right: 100%;
  }
}
.my-login-box a span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #03e9f4);
  animation: btn-anim4 1s linear infinite;
  animation-delay: .75s
}
@keyframes btn-anim4 {
  0% {
    bottom: -100%;
  }
  50%,
  100% {
    bottom: 100%;
  }
}

</style>
