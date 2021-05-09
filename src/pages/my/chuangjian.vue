<template>
	<view class="chuangjian-content">
		<view class="pre-vote" v-for="(item, index) in voteArr" :key="index" @click="openButtons(index)">
      <text class="title-text">{{item.title}}</text>
      <view v-if="showButtons && editIndex === index" class="buttons">
        <view class="edit button" @click="edit">
          <image src="/static/edit.png"></image>
          <text>编辑</text>
        </view>
        <view class="delete button" @click="shanchu">
          <image src="/static/delete.png"></image>
          <text>删除</text>
        </view>
        <view class="check button" @click="check">
          <image src="/static/chakan.png"></image>
          <text>查看</text>
        </view>
        <view class="share button" @click="share">
          <image src="/static/share.png"></image>
          <text>转发</text>
        </view>
      </view>
    </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
        showButtons: false,
        editIndex: 0,
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
      openButtons(index) {
        this.editIndex = index;
        this.showButtons = !this.showButtons;
      },
      edit() {},
      shanchu() {},
      share() {},
      check() {}
		}
	}
</script>

<style>
  image {
    width: 30px;
    height: 30px;
  }
	.chuangjian-content {
    background-color: #f5f5f5;
    padding: 5px 0;
  }
  .pre-vote {
    padding: 15px 5px;
    border-bottom: 2px solid #fff;
  }
  .title-text {
    padding: 10px 5px;
  }
  .button {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0 35px;
    /* color: #1296db; */
    font-size: 15px;
  }
  .buttons {
    display: flex;
    justify-content: center;
  }
</style>
