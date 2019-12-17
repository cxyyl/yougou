<template>
  <div>
    <view class="top">
      <view class="search">
        <icon class="searchIcon"
              type="search"
              size="18">
        </icon>
        <text class="searchbar">搜索</text>
      </view>
    </view>
    <swiper class="swiper"
            indicator-dots
            indicator-color='rgba(255,255,255,0.3)'
            indicator-active-color='#fff'
            autoplay
            circular>
      <block v-for="item in swiperList"
             :key="item.goods_id">
        <swiper-item>
          <image class="swiperimg"
                 mode="aspectFill"
                 :src="item.image_src"></image>
        </swiper-item>
      </block>
    </swiper>
    <!-- 获取分类列表 -->
    <view class="list">
      <img class="imgList"
           v-for="(item,index) in list"
           :key="index"
           :src="item.image_src"
           alt="">
    </view>
    <!-- 楼层结构 -->
    <view v-for="(item,index) in moreList" :key="index" class='floorimg'>
      <view class="floor_top">
        <img class="img_top"
             :src="item.floor_title.image_src"
             alt="">
      </view>
      <view class="floor_bottom-r">
        <img class="fristimg"
             :src="item.product_list[0].image_src"
             alt="">
        <view class="floor_bottom-l">
          <img class="diffImg"
               :src="item.product_list[1].image_src"
               alt="">
          <img class="diffImg"
               :src="item.product_list[2].image_src"
               alt="">
          <img class="diffImg"
               :src="item.product_list[3].image_src"
               alt="">
          <img class="diffImg"
               :src="item.product_list[4].image_src"
               alt="">
        </view>
      </view>
    </view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      swiperList: [],
      list: [],
      moreList: []
    }
  },
  onLoad () {
    // 轮播图请求
    wx.request({
      url: 'https://www.uinav.com/api/public/v1/home/swiperdata',
      data: 'data',
      method: 'GET',
      dataType: 'json',
      success: res => {
        // console.log(res)
        this.swiperList = res.data.message
      }
    })
    // 获取分类列表
    wx.request({
      url: 'https://www.uinav.com/api/public/v1/home/catitems',
      data: 'data',
      method: 'GET',
      dataType: 'json',
      success: res => {
        // console.log(res)
        this.list = res.data.message
      }
    })
    // 获取楼层数据
    wx.request({
      url: 'https://www.uinav.com/api/public/v1/home/floordata',
      data: 'data',
      method: 'GET',
      dataType: 'json',
      success: res => {
        // console.log(res.data.message)
        this.moreList = res.data.message
      }
    })
  }
}
</script>

<style lang='less' >
.top {
  height: 100rpx;
  width: 100%;
  background-color: #eb4450;
  display: flex;
  align-items: center;
  justify-content: center;
  .search {
    width: 100%;
    height: 60rpx;
    margin: 0 16rpx;
    // border: 1px solid #eb4450;
    background-color: white;
    border-radius: 10rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #bbb;
    .searchbar {
      margin-left: 16rpx;
      font-size: 30rpx;
    }
  }
}
.swiper {
  width: 100%;
  height: 340rpx;
  .swiperimg {
    width: 100%;
    height: 340rpx;
  }
}
.list {
  height: 194rpx;
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  .imgList {
    width: 128rpx;
    height: 140rpx;
  }
}
//  <!-- 楼层样式 -->
.floorimg {
  width: 100%;
  margin-bottom: 20rpx;
  .floor_top {
    width: 100%;
    background-color: #f4f4f4;
    .img_top {
      width: 100%;
      height: 88rpx;
    }
  }
  .floor_bottom-r {
    margin: 20rpx 17rpx;
    display: flex;
    height: 359rpx;
    width: 100%;
    // flex-wrap: nowrap;
    .fristimg {
      width: 232rpx;
      height: 370rpx;
      margin-right: 10rpx;
    }
    .floor_bottom-l {
      flex: 1;
      font-size: 0;
    .diffImg {
      width: 232rpx;
      height: 180rpx;
      margin: 0 10rpx 10rpx 0;
    }
  }
  }
}
</style>