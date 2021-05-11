<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view> -->
    <home/>
	</view>
</template>

<script>
  import home from './home'; 
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
    components: {
      home
    },
		onLoad() {
      this.getUserInfo();
		},
		methods: {
      getUserInfo() {
        // 获取用户信息
        uni.getUserInfo({
          provider: 'weixin',
          success: function (infoRes) {
            console.log('用户昵称为：' + infoRes.userInfo.nickName);
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

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin: 200rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
