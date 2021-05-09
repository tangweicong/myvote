<template>
	<view class="content">
    <view class="danxuan">
      <view class="image"> 
        <image class="logo" src="/static/danxuan.png"></image>
      </view>
      <view @click="danxuan">
        <text class="title">单选投票</text>
      </view>
    </view>
		<view class="duoxuan bgc">
      <view  class="image"> 
        <image class="logo" src="/static/duoxuan.png"></image>
      </view>
      <view @click="duoxuan">
        <text class="title">多选投票</text>
      </view>
    </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {
      // this.test();
		},
		methods: {
      test() {
        uni.request({
          url: 'http://192.168.1.115:9998/app_user/test', //仅为示例，并非真实接口地址。
          data: {
              text: ''
          },
          success: (res) => {
              console.log(res.data, 'datatatt');
          }
        });
      },
      danxuan() {
        console.log('danxuan');
        uni.switchTab({
            url: '/pages/vote/index',
            success: () => {
              console.log('123')
            }
        });
      },
      duoxuan() {
        console.log('duoxuan');
        uni.switchTab({
            url: '/pages/vote/index',
            success: () => {
              console.log('123')
            }
        });
      }
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
  .image {
    padding: 0 10px;
  }
	.logo {
		height: 200rpx;
		width: 200rpx;
    margin: 130rpx auto;
		/* margin: 200rpx auto 50rpx auto; */
	}

	.title {
    padding: 15rpx 50rpx;
    background-color: #1296db;
		font-size: 36rpx;
		color: #fff;
	}
</style>
