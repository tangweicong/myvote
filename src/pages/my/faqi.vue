<template>
	<view class="content">
		<!-- <image class="logo" src="/static/png.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view> -->
    <!-- <success /> -->
    <guanliyuanshenhe />
	</view>
</template>

<script>
  import success from '../components/success'
  import guanliyuanshenhe from '../components/guanliyuanshenhe'
	export default {
		data() {
			return {
				title: '发起'
			}
		},
    components: {
      success,
      guanliyuanshenhe
    },
		onLoad() {
      
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
