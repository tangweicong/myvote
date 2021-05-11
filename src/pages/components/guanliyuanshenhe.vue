<template>
		<!-- <image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view> -->
    <!-- <tousu /> -->
    <view class="vote-page-content">
        <view class="pretousu" v-for="(item, index) in tousuArr" :key="index"> 
          <view class="userinfo">
            <text>用户信息:</text>
            <text class="username color">{{item.username}}</text>
          </view>
          <view class="voteinfo">
            <text>投票信息:</text>
            <text class="tousuinfo color">{{item.vote}}</text>
          </view>
          <view class="reason"> 
            <text>投诉原因:</text>
            <text class="tousureason color">{{item.tousuContent}}</text>
          </view>
        </view>
    </view>
   

</template>

<script>
import tousu from '../components/tosu'
import votePage from '../components/votePage'
	export default {
		data() {
			return {
				title: '审核',
        tousuArr: [
          {
            vote: '123',
            username: 'gg',
            tousuContent: '投票投诉',
          },
          {
            vote: '456',
            username: 'xx',
            tousuContent: '投诉投诉',
          }
        ],
			}
		},
    components: {
      tousu,
      votePage,
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
	.pretousu {
    margin: 20px 0;
    padding: 10px;
    background-color: #f5f5f5;
    width: 100%;
  }
  .vote-page-content {
      width: 100%;
      padding: 5px;
    }
    .userinfo {
      display: flex;
      justify-content: space-between;
    }
    .username {
      margin-right: 30px;
    }
    .voteinfo {
      margin: 10px 0;
       display: flex;
      justify-content: space-between;
    }
    .tousuinfo {
      margin-right: 30px;
    }
    .reason {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .tousureason {
      background-color: #fafafa;
      padding: 20px 10px;
      margin: 10px 0;
      border: 3px solid #fafafa;
    }
    .color {
      color: #1296db;
    }
</style>
