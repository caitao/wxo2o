<template>
  <div class="index">
    <div class="search">
        <van-search
          :value="value"
          placeholder="请输入搜索关键词"
          use-action-slot
          bind:change="onChange"
          bind:search="onSearch"
          label="地址"
          shape="round"
        >
          <view slot="action" :tap="onSearch">搜索</view>
        </van-search>
    </div>
    <div class="category">
      <van-tabs :active="active"
              @change="onChange">
      <van-tab title="首页">
        <div class="swiper">
          <swiper class="swiper-container" indicator-dots="true" autoplay="true" interval="3000" circular="true" duration="500">
            <block v-for="(item, index) in banner " :key="index">
              <swiper-item class="swiper-item">
                <image :src="item.image_url" class="slide-image" />
              </swiper-item>
            </block>
          </swiper>
        </div>
      </van-tab>
      <van-tab title="女装">
        <van-tabs :active="active"  @change="onChangeSortMethod">
          <van-tab title="综合"></van-tab>
          <van-tab title="销量"></van-tab>
          <van-tab title="新品"></van-tab>
          <van-tab title="价格"></van-tab>
        </van-tabs>
      </van-tab>
      <van-tab title="男装">男装</van-tab>
      <van-tab title="童装">童装</van-tab>
      <van-tab title="运动">运动</van-tab>
     </van-tabs>
    </div>

  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      banner: [
        {
          category: 'woman_up',
          image_url: 'https://s4.lativ.com/i/ProductShow/43016_1P29_1180X557_190723_CN.jpg'
        },
        {
          category: 'woman_up',
          image_url: 'https://s1.lativ.com/i/ProductShow/40431_2P8D_1180X557_190722_CN.jpg'
        },
        {
          category: 'child_up',
          image_url: 'https://s4.lativ.com/i/ProductShow/41252_1P85D_1180X557_190722_CN.jpg'
        }
      ],
      tabList: ['综合', '销量', '新品', '价格'],
      active: 0,
      value: ''
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    // let app = getApp()
  },

  onSearch (event) {
    if (this.data.value) {
      wx.showToast({
        title: '搜索：' + this.data.value,
        icon: 'none'
      })
    }
  },
  onChange (event) {
    // 代码搞这里
    console.log(event)
    // 选择的索引
    console.log(event.mp.detail.index)
    // 标题
    console.log(event.mp.detail.title)
    console.log(this.active)
    // 最好手动赋值一下,要不值不是最新的
    this.active = event.mp.detail.index
    console.log(this.active)
  },

  onChangeSortMethod (event) {
    // 代码搞这里
    console.log(event)
    // 选择的索引
    console.log(event.mp.detail.index)
    // 标题
    console.log(event.mp.detail.title)
    console.log(this.active)
    // 最好手动赋值一下,要不值不是最新的
    this.active = event.mp.detail.index
    console.log(this.active)
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

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}

.swiper-item{
  width: 100%;
  display: block;
  height: 200px;
}

.swiper{
    height: 400rpx;
    width: 100%;
}

swiper-item image {
    height: 100%;
    width: 100%;
    display: inline-block;
    overflow: hidden;
}
</style>
