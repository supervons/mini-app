<template>
  <van-row>
    <van-row>
      <van-col span="8">span: 8</van-col>
      <van-col span="8">span: 8</van-col>
      <van-col span="8">span: 8</van-col>
    </van-row>
    <van-row>
      <van-col span="8">
        <van-tag type="danger">标签</van-tag>
      </van-col>
      <van-col span="8">
        <van-tag type="primary">标签</van-tag>
      </van-col>
      <van-col span="8">
        <van-tag type="success">标签</van-tag>
      </van-col>
    </van-row>

    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>
    <button open-type="getUserInfo" lang="zh_CN" bindgetuserinfo="onGotUserInfo">获取用户信息</button>
    <van-button type="default" @click="showaToast">默认按钮</van-button>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" v-model="userName" placeholder="用户名" />
      <input type="text" class="form-control" v-model.lazy="passWord" placeholder="密码" />
      <van-button type="primary" @click="login">登录</van-button>
    </form>
  </van-row>
</template>

<script>
import card from '@/components/card'

export default {
  mpType: 'page',

  data () {
    return {
      motto: 'Hello World',
      userName: '',
      passWord: '',
      userInfo: {}
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '/packageA/logs'
      this.$router.push(url)
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      // eslint-disable-next-line
      console.log('clickHandle:', msg, ev)
    },
    showaToast () {
      // api 访问测试
      wx.showToast({
        title: '点击成功',
        icon: 'warn',
        duration: 2000
      })
      console.log(JSON.stringify(this.userInfo))
    },
    login () {
      // api 访问测试
      this.$fly.request({
        method: 'post', // post/get 请求方式
        url: '/user/loginAction',
        body: { loginId: this.userName, passWord: this.passWord }
      }).then(res => {
        if (res.code === 'success') {
          wx.showToast({
            title: '登录成功',
            icon: 'success',
            duration: 2000
          })
        } else {
          wx.showToast({
            title: res.msg,
            icon: 'none',
            duration: 2000
          })
        }
      })
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}


.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
