<template>
<view class="vote-content">
  <view class="vote-form">
      <view class="vote-title">
          <input class="uni-input" focus v-model="title" placeholder="请输入投票的标题(1-15个字)"/>
      </view>
      <view class="vote-desc">
          <textarea placeholder="请填写投票内容说明(2-80个字)" v-model="desc"/>
      </view>
      <view class="vote-options">
          <!-- 选项 -->
          <!-- <view class="option"> 
            <input class="uni-input" placeholder="选项一">
          </view>
           <view class="option"> 
            <input class="uni-input" placeholder="选项二">
          </view> -->
          <view class="option" v-for="(item, index) in optionArray" :key="index">
            <text class="option-text">选项{{index}}</text>
            <input class="option-text option-value" v-model="item.value">
          </view>
          <view class="addOption">添加选项</view>
      </view>
      <view class="vote-type">
         <!-- 投票类型 -->
         <text>投票类型</text>
         <picker class="picker" @change="bindPickerChange" mode = selector :value="index" :range="getOptionArray">
           <view class="uni-input">{{typeArray[index].type}}</view>
         </picker>
      </view>
      <view class="vote-time">
         <!-- 投票时间 -->
          <view>截止日期</view>
          <picker class="date-picker" mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
              <view class="uni-input">{{date}}</view>
          </picker>
          <picker class="time-picker" mode="time" :value="endTime" start="00:00" end="23:59" @change="endTimeChange">
              <view class="uni-input">{{endTime}}</view>
          </picker>
      </view>
      <view class="vote-niming">
          <!-- 是否匿名投票 -->
          <text class="niming-text">匿名投票</text>
          <switch @change="switch1Change" class="niming-switch"></switch>
      </view>
      <view class="fabu-button" @click="fabu">
          确认发布
      </view>
    </view>
  </view>
</template>

<script>
	export default {

    data() {
        const currentDate = this.getDate({
            format: true
        })
        return {
            title: '',
            focus: false,
            desc: '',
            isNiming: false,
            date: currentDate,
            typeArray: [
              {
                type: '单选',
                value: 1
              },
              {
                type: '多选',
                value: 2,
              }
            ],
            optionArray: [
              {
                value: '',
              },
              {
                value: '',
              }
            ],
            index:0,
            endTime: '12:01',
            // time: '12:01'
        }
    },
    computed: {
      getOptionArray() {
        return this.typeArray.map((item) => {
          return item.type;
        })
      },
      startDate() {
            return this.getDate('start');
        },
        endDate() {
            return this.getDate('end');
        }
    },
    methods: {
        bindPickerChange: function(e) {
            console.log('picker发送选择改变，携带值为', e.target.value)
            this.index = e.target.value
        },
        endTimeChange: function(e) {
            console.log(e.target.value)
            this.endTime = e.target.value
        },
        switch1Change: function (e) {
            // console.log('switch1 发生 change 事件，携带值为', e.target.value)
            this.isNiming = e.target.value;
        },
        bindDateChange: function(e) {
            this.date = e.target.value
        },
        getDate(type) {
            const date = new Date();
            let year = date.getFullYear();
            let month = date.getMonth() + 1;
            let day = date.getDate();

            if (type === 'start') {
                year = year - 60;
            } else if (type === 'end') {
                year = year + 2;
            }
            month = month > 9 ? month : '0' + month;;
            day = day > 9 ? day : '0' + day;
            return `${year}-${month}-${day}`;
        },
        fabu() {
          const voteEndDate = this.date + ' ' + this.endTime;
          console.log(voteEndDate)
          let obj = {
            title: this.title,
            desc: this.desc,
            voteType: this.typeArray[this.index].value,
            isNiming: this.isNiming,
            optionArray: this.optionArray,
            // date: (new Date(this.date + ' ' + this.endTime)).getTime()
            date: this.parserDate(voteEndDate)
          };
          console.log(obj, 'ooooooooo', this.timestampToTime(this.parserDate(voteEndDate)));
        },
        parserDate(date) {
          var t = Date.parse(date)
          if (!isNaN(t)) {
            return new Date(Date.parse(date.replace(/-/g, '/'))).getTime()
          }
        },
        timestampToTime(timestamp) {
            var date = new Date(timestamp * 1);//时间戳为10位需*1000，时间戳为13位的话不需乘1000
            var Y = date.getFullYear();
            var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1);
            var D = date.getDate() < 10 ? '0' + date.getDate() : date.getDate();
            var h = date.getHours() < 10 ? '0' +date.getHours():date.getHours();
            var m = date.getMinutes() < 10 ? '0'+date.getMinutes() : date.getMinutes();
            var s = date.getSeconds() < 10 ? '0' + date.getSeconds() : date.getSeconds();
            return Y+'-'+M+'-'+D+' '+h+':'+m+':'+s;
        }
    }
}
</script>

<style>
  .vote-content {
    padding: 25px 0px;
  }
	.vote-title {
    padding: 10px;
    background-color: #f5f5f5;
  }
  .vote-desc {
    margin: 20px 0;
    padding: 10px;
    background-color: #f5f5f5;
  }
  .vote-options {
    position: relative;
    padding: 10px;
    background-color: #f5f5f5;
  }
  .option {
    padding: 10px;
    border-bottom: 3px solid #fff;
    display: flex;
    /* justify-content: space-between; */
  }
  .option-text {
    color: grey;
    font-size: 15px;
  }
  .option-value {
    margin-left: 50px;
    
  }
  .addOption {
    background-color: #007aff;
    text-align: center;
    margin: 20px 0;
    margin-left: 50%;
    height: 50px;
    line-height: 50px;
    width: 200px;
    transform: translateX(-50%);
    color: #fff;
    font-weight: 400;
    border-radius: 5px;
  }
  .vote-type {
    margin: 20px 0;
    padding: 10px;
    background-color: #f5f5f5;
    display: flex;
    justify-content: space-between;
  }
  .picker {
    margin-right: 20px;
    color: #fff;
    background-color: #007aff;
    padding: 5px 10px;
    border-radius: 5px;
  }
  .vote-time {
    padding: 10px;
    background-color: #f5f5f5;
  }
  .vote-niming {
    margin: 20px 0;
    padding: 10px;
    background-color: #f5f5f5;
    display: flex;
    justify-content: space-between;
  }
  .niming-switch {
    margin-right: 20px;
  }
  .fabu-button {
    text-align: center;
    background-color: #007aff;
    margin-left: 50%;
    transform: translateX(-50%);
    color: #fff;
    padding: 10px 0;
    border-radius: 5px;
  }
  .vote-time {
    display: flex;
    justify-content: space-between;
  }
  .time-picker {
    /* height: 500px; */
    margin-right: 20px;
  }
  .date-picker {
    margin-left: 20px;
  }
</style>
