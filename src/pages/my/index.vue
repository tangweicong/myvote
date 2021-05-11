<template>
	<view class="content">
      <!-- <chuangjian /> -->
      <view class="title">
        <view v-for="(item, index) in titleArr" :key="index" class="alltitle" @click="changeIndex(index)">
          <text :class="{textColor: activeIndex == index}">{{item}}</text>
        </view>
      </view>
      <template>
        <view>
          <component :is="currentComponents"></component>
        </view>
      </template>
	</view>
</template>

<script>
import chuangjian from './chuangjian';
import shenhe from './shenhe';
import faqi from './faqi';
const compConfig = {
  0: chuangjian,
  1: shenhe,
  2: faqi
}
	export default {
		data() {
			return {
				title: 'Hello',
        titleArr: ['我的投票', '我参与的', '审核'],
        activeIndex:0,
        swiperIndex: 0,
        indicatorDots: true,
        currentComponents: compConfig[0],
      }
		},
		onLoad() {
		},
		methods: {
      handleClickSlide(index) {
        this.activeIndex = index;
      },
      changeIndex(index) {
        this.activeIndex = index;
        this.currentComponents = compConfig[index]
      }
		}
	}
</script>

<style>
	.title {
    display: flex;
    padding: 20px 10px;
    align-items: center;
    justify-content: center;
  }
  .alltitle {
    margin: 0 20px;
  }
  .textColor {
    color: #3cc51f;
  }
</style>
