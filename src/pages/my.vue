<template>
  <van-row>
    <van-notice-bar
      left-icon="volume-o"
      text="国造智能有限公司致力于软件行业多年，期待与您的合作。"
    />
    <div class="userinfo">
      <open-data type="userAvatarUrl"></open-data>
      <open-data type="userNickName"></open-data>
    </div>
    <button open-type="getUserInfo" lang="zh_CN" bindgetuserinfo="onGotUserInfo">获取用户信息</button>
  </van-row>
</template>

<script>
import card from '@/components/card'

export default {
  components: {
    card
  },
  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  },
  data () {
    return {
      userInfo: {}
    }
  },
  methods: {
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
    }
  }
}
</script>

<style>
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
</style>
