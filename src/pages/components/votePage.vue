<template>
	<view class="vote-page-content">
    <view class="vote-page-title">
      <text class="page-title-text">{{voteObj.title}}</text>
      <image @click="share" src="/static/share.png"></image>
    </view>
    <text class="vote-page-type">{{voteObj.type === 1 ? '[单选]' : '[多选]'}}</text>
    <view class="vote-page-option" v-for="(item, index) in voteObj.options" :key="index">
      <view>
        <text class="option-text">{{item.text}}</text>
        <image v-if="index==1" class="chose" src="/static/chose.png"></image>
      </view>
      <view class="tongji">
        <text class="piaoshu">{{item.people}}票</text>
        <text class="baifenbi">{{item.baifenbi}}</text>
      </view>
    </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				voteObj: {
          title: 'jjj',
          type: 1,
          options: [
            {
              text: '1',
              baifenbi: '50%',
              people: 1,
            },
            {
              text: '2',
              baifenbi: '50%',
              people: 1
            }
          ],
          time: '2021-05-09 12:00:00'
        }
			}
		},
		onLoad() {
     
		},
		methods: {
      share() {
        console.log('shrrrrr')
        uni.share({
            provider: "weixin",
            scene: "WXSceneSession",
            type: 0,
            href: "http://uniapp.dcloud.io/",
            title: "小程序分享",
            summary: "我正在使用这个小程序进行投票，快来一起投票吧",
            success: function (res) {
                console.log("success:" + JSON.stringify(res));
            },
            fail: function (err) {
                console.log("fail:" + JSON.stringify(err));
            }
        });
      }
		}
	}
</script>

<style>
.vote-page-content {
  width: 100%;
  
}
	image {
    width: 40px;
    height: 40px;
  }
  .chose {
    height: 30px;
    width: 30px;
    margin-left: 20px;
  }
  .vote-page-type {
    color: #007aff;
    margin-left: 10px;
  }
  .vote-page-title {
    display: flex;
    justify-content: space-between;
    padding: 15px 15px 0 15px;
  }
  .page-title-text {
    font-weight: 700;
  }
  .vote-page-option {
    margin: 10px 0;
    background-color: #f5f5f5;
    display: flex;
    justify-content: space-between;
    /* line-height: 100%; */
    padding: 10px;
  }
  .tongji {
    margin-right: 20px;
  }
  .piaoshu {
    padding: 0 10px;
  }
  .baofenbi {
    padding: 0 10px;
  }
</style>
