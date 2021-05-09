<template>
	<view class="content">
      <!-- <chuangjian /> -->
      <view class="title">
        <view v-for="(item, index) in titleArr" :key="index" class="alltitle" @click="changeIndex(index)">
          <text :class="{textColor: activeIndex == index}">{{item}}</text>
        </view>
      </view>
      <Swiper :options="swiperOption" ref="mySwiper" id="swipers">
        <SwiperSlide>
          <chuangjian />
        </SwiperSlide>
        <SwiperSlide>
          <shenhe />
        </SwiperSlide>
        <SwiperSlide>
          <faqi />
        </SwiperSlide>
      </Swiper>
	</view>
</template>

<script>
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/swiper-bundle.css'
import BetterScroll from 'better-scroll'
import chuangjian from './chuangjian';
import shenhe from './shenhe';
import faqi from './faqi';
let vm = null;
	export default {
		data() {
			return {
				title: 'Hello',
        titleArr: ['我的投票', '我参与的', '审核'],
        activeIndex:0,
        swiperIndex: 0,
        indicatorDots: true,
        swiperOption: {
          notNextTick: true,
          initialSlide: 0,
          speed: 800,
          //滑动方向
          direction: "horizontal",
          //小手掌抓取滑动
          grabCursor: true,
          on: {
            slideChangeTransitionEnd: function () {
              console.log(this.activeIndex);
              // console.log(vm,'vmvmvm');
              const index = this.activeIndex;
              vm.handleClickSlide(index);
              // 切换结束时，告诉我现在是第几个slide
            }
          }
        }
      }
		},
    components: {
      Swiper,
    SwiperSlide,
      chuangjian,
      shenhe,
      faqi
    },
    directives: {
    swiper: directive
  },
    computed: {
      aswiper() {
        return this.$refs.mySwiper;
      }
    },
		onLoad() {
      vm = this;
		},
		methods: {
      handleClickSlide(index) {
        this.activeIndex = index;
      },
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
      changeIndex(index) {
        const swipers = document.getElementById('swipers');
        console.log(swipers, 'swwwwww', this.aswiper)
        this.activeIndex = index;
        this.aswiper.slideTo(3, 1000, false);
        // this.$refs.mySwiper.slideTo(this.activeIndex, 400)
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
