<template>
	<view class="yuanyin">
		<view class="title">
      请填写投诉原因
    </view>
    <textarea class="tousu-content" placeholder="请填写投诉内容" v-model="tousu"/>
    <view class="tousu-button">确认投诉</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tousu:''
			}
		},
		onLoad() {
      
		},
		methods: {
		}
	}
</script>

<style>
  .yuanyin {
    /* padding: 10px 0; */
  }
	.title {
    padding: 20px 0;
    font-weight: 700;
  }
  .tousu-content {
    background-color: #f5f5f5;
    padding: 10px;
    margin: 20px 0;
  }
  .tousu-button {
    background-color: #007aff;
    color: #fff;
    padding: 10px;
    text-align: center;
    margin-left: 50%;
    transform: translateX(-50%);
    border-radius: 5px;
  }
</style>
