<template>
  <van-row>
    <van-row>
      <swiper :indicator-dots="indicatorDots"
              autoplay="true" :interval="interval" :duration="duration">
        <swiper-item
          v-for="item in images"
          :key="item.key">
          <image style="width: 100%; background-color: #eeeeee;" mode="widthFix" :src="item.src"/>
        </swiper-item>
      </swiper>
    </van-row>
    <van-row class="about">
      <van-collapse :value="activeNames" @change="onChange" accordion>
        <van-collapse-item title="公司概况" name="1">
          公司拥有雄厚的人才资源。公司核心骨干来自于小米、闪银、中国创新支付集团等，凭借资深的行业经验，带领团队不断创新发展。公司成立至今，以其专业的平台实力、深厚的企业文化聚集了国内大批高端技术人才，不断夯实团队的技术实力基础。是获北京市政府认定的高新技术企业，拥有十余款软件著作权。经过十几年的磨砺，国造智能已成为高新科技行业的中流砥柱，凭借卓越的实力与强大的资源，不断在科技、金融领域展示出非凡的表现力与创造力。未来国造智能将继续深造科研，锐意创新，成为高新科技行业发展的助推力量。经过长时间的市场调研， 结合实践经验， 听取多位业内行家意见潜心研发。 我们引进最先进的大数据流量分析， 对用户进行精准定位， 提供最优质的系统服务。
        </van-collapse-item>
        <van-collapse-item title="联系我们" name="2">
          <view>邮箱：xxx</view>
          <view>地址：xxx</view>
          <view>电话：xxx</view>
        </van-collapse-item>
      </van-collapse>
      <button open-type="contact" bindcontact="handleContact">在线咨询</button>
    </van-row>
  </van-row>
</template>

<script>
import card from '@/components/card'

export default {
  mpType: 'page',

  data () {
    return {
      images: [
        { key: 1, src: '/static/nav/banner.png' },
        { key: 2, src: '/static/nav/banner2.png' },
        { key: 3, src: '/static/nav/banner3.png' }
      ],
      indicatorDots: true,
      autoplay: false,
      interval: 5000,
      duration: 1000,
      activeNames: ['1']
    }
  },

  components: {
    card
  },

  methods: {
    onChange (event) {
      wx.getLocation({
        type: 'wgs84',
        success: (res) => {
          console.log(res)
        }
      })
      this.activeNames = event.mp.detail
    }
  }
}
</script>

<style scoped>
.about {
  display: inline-block;
  margin-top: 20px;
  width: 100%;
}
</style>
