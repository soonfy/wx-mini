<template>
  <div class="container">
    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <div>
      <div class="title">
        <label>测试用例</label>
        <span>更多 ></span>
      </div>
      <div class="list">
        <div v-for="(item,key) in list" :key="key" class="item">
          <a :href="item.href">{{item.name}}</a>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      userInfo: {},
      list: [{
        name: 'vuex',
        href: '/pages/vuex/main'
      }, {
        name: 'wx-f2',
        href: '/pages/wx-f2/main'
      }, {
        name: 'echarts',
        href: '/pages/echarts/main'
      }, {
        name: 'fly',
        href: '/pages/fly/main'
      }, {
        name: 'dayjs',
        href: '/pages/dayjs/main'
      }, {
        name: 'exchange',
        href: '/pages/exchange/main'
      }]
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.container {
  padding: 0;
  font-size: 12px;
  color: #666;
}

.container > div {
  margin-bottom: 10px;
}

.userinfo {
  width: 60px;
  margin: 0 auto;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 20px;
}

.title {
  display: flex;
  border-bottom: #eee 1px solid;
  padding: 0 0 10px 0;
}

.title > label {
  flex: 1;
  margin: 0 0 0 10px;
  padding: 0 0 0 4px;
  border-left: #448ef6 2px solid;
}

.title > span {
  display: inline-block;
  margin: 0 10px 0 0;
}

.list {
  display: flex;
  justify-content: space-between;
  flex-flow: row wrap;
  margin: 0 10px;
}

.item {
  width: 30%;
  min-width: 70px;
  height: 20px;
  padding: 10px 0;
}

.item > a {
  text-align: center;
  border: #448ef6 1px solid;
  border-radius: 6%;
}
</style>
