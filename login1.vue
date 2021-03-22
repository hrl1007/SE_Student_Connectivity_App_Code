<template>
  <div id="login">
    <div class="pop">
      <h2 style="color:#b6b1b7">Sign In To <span style="color:#6f4a7e">Campus</span></h2>
      <h5 style="color:#6f4a7e; font-weight: normal;">with your UCL credentials</h5>
      <div>
        <el-form :model="ruleForm"  ref="ruleForm">
          <van-field class="input" v-model="ruleForm.username"
            name="name" placeholder="Abodefg@ucl.ac.uk"
            :rules="[{ required: true, message: 'Pleas Input Username' }]"
          />
          <van-field class="input" v-model="ruleForm.password"
            type="password" name="Password" placeholder="password"
            :rules="[{ required: true, message: 'Pleas Input Password' }]"
          />

          <div style="margin-top: 5%; font-size:10px; color:#6f4a7e;  ">
            <van-checkbox v-model="checked" icon-size="16px" checked-color="#d83587">Remember Me</van-checkbox>
          </div>

          <el-form-item style="margin-top: 5%;">
            <van-button style="width:60%" @click="submitForm('ruleForm')" round native-type="submit" color="linear-gradient(to right, #e23783, #8125ac)">Log In</van-button>
            <div>
              <span @click="clearCookie" style="margin-top:5%; color: #b6b1b7;">Forgotten your passwprd?</span>
            </div>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      ruleForm: {
        username: '',
        password: ''
      },
      checked: false
    }
  },

  mounted () {
    this.getCookie()
  },

  methods: {
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          const self = this
          if (self.checked === true) {
            self.setCookie(self.ruleForm.username, self.ruleForm.password, 7)
          } else {
            console.log('fresh Cookie')
            self.clearCookie()
          }
          alert('success!')
          this.$router.push({
            name: 'main',
            params: {
              user: self.ruleForm.username,
              pwd: self.ruleForm.password
            }
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    // resetForm(formName) {
    //   this.$refs[formName].resetFields();
    // },
    setCookie (c_name, c_pwd, exdays) {
      var exdate = new Date() 
      exdate.setTime(exdate.getTime() + 24 * 60 * 60 * 1000 * exdays) 
      
      document.cookie = 'userName' + '=' + c_name + ';path=/;expires=' + exdate.toGMTString()
      document.cookie = 'password' + '=' + c_pwd + ';path=/;expires=' + exdate.toGMTString()
    },

    getCookie: function () {
      if (document.cookie.length > 0) {
        var arr = document.cookie.split('; ') 
        for (var i = 0; i < arr.length; i++) {
          var arr2 = arr[i].split('=') 
         
          if (arr2[0] === 'userName') {
            //  console.log(arr2[1])
            this.ruleForm.username = arr2[1] 
          } else if (arr2[0] === 'password') {
            // console.log(arr2[1])
            this.ruleForm.password = arr2[1]
          }
        }
        this.checked = true
      }
    },
   
    clearCookie: function () {
      this.setCookie('', '', -1) 
    }
  }
}
</script>

<style>
#login{
  background-image:url(../assets/logo.png);
  background-color: aqua;
  text-align: center;
  line-height: 24px;
  height: 100%;
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
}
.pop{
  height:50%;
  padding: 15% 15% 0 15%;
  border-radius: 25px 25px 0 0;
  background-color: white;
  animation-name: dialogSlip;
  animation-duration: 2s;
  animation-fill-mode: forwards;
}
.input{
  border: 1px solid #7d2aa0;
  border-radius:25px;
  line-height: 30px;
  margin-top: 5%
}

@keyframes dialogSlip {
  0%{
    transform: translate(0%, 200%);
    -webkit-transform: translate(0%, 200%);
    -moz-transform: translate(0%, 200%);
    -ms-transform: translate(0%, 200%);
    -o-transform: translate(0%, 200%);
  }
  100%{
      transform: translate(0%, 100%);
      -webkit-transform: translate(0%, 100%);
      -moz-transform: translate(0%, 75%);
      -ms-transform: translate(0%, 100%);
      -o-transform: translate(0%, 100%);
  }
}
</style>
