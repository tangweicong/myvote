<template>
	<view class="content">
		<view v-for="(item, index) in voteArr" :key="index">
      <text>{{item.title}}</text>
    </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				voteArr: [
          {
            id: 1,
            title: '1'
          },
          {
            id: 2,
            title: '2'
          }
        ]
			}
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
	
</style>
