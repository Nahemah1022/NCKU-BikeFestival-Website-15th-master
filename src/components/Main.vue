<template lang="pug">
  div(class="main_page")
    div(class="news_top_bar_pc")
      div(class="news_top_bar_layout" @click="scroll()")
        router-link(class="top_logo" to="/")
        div(class="top_bar")
          router-link(tag="label" v-for="(text, index) of menuText" v-bind:key="text" v-bind:to="'/' + urlText[index]" v-if="pc") {{text}}
          label(@click="openTab('https://docs.google.com/forms/d/e/1FAIpQLSdBW8m8SVm5YqwtsOGWAaMYwOWiMJ_RbjZTNMq4dJYYWCg85Q/viewform'); list = false;" v-if="pc") 我要報名
    div(class="intro_layout")
      div(class="intro_layout1")
        div(class="test")
          div(class="intro_film")
            div(class="black1")
              div(class="white_block" v-for="(block, i) of 16")
            div(class="black2")
              div(class="white_block" v-for="(block, i) of 16")
          div(class="intro_menu")
            div(class="intro_menu_l")
              router-link(tag="button" v-bind:to="'/activity'" ) 活動<br>介紹
              router-link(tag="button" v-bind:to="'/department'") 科系<br>資訊
              router-link(tag="button" v-bind:to="'/live'") 影片<br>專區
            div(class="intro_menu_r")
              button(tag="button" @click="openTab('https://docs.google.com/forms/d/e/1FAIpQLSdBW8m8SVm5YqwtsOGWAaMYwOWiMJ_RbjZTNMq4dJYYWCg85Q/viewform'); list = false;" v-if="pc") 我要<br>報名
              router-link(tag="button" v-bind:to="'/column'") 主題<br>專欄
              router-link(tag="button" v-bind:to="'/sponsor'") 合作<br>單位
      div(class="intro_layout2")
        div(class="show_info1")
        div(class="show_info2")
</template>

<script>
//  import axios from 'axios'
export default {
  created () {
    window.addEventListener('resize', this.windowSizeChange)
  },
  destroyed () {
    window.removeEventListener('resize', this.windowSizeChange)
  },
  data: function () {
    return {
      menuText: [ '活動介紹', '科系資訊', '主題專欄', '合作單位'],
      urlText: ['activity', 'department', 'column', 'sponsor'],
      list: false,
      pc: this.isPC(),
      currentIndex: -1,
      loader: null
    }
  },
  mounted: async function () {
    this.pc = this.isPC()
    this.setBarHeight()
    setInterval(this.timeCounter, 1000)
    this.numberDom1 = document.querySelector('#news_number_1')
    this.numberDom2 = document.querySelector('#news_number_2')
    this.timeCounter()
    this.loader = this.$loading.show()
    this.loader.hide()
  },
  methods: {
    windowSizeChange: function (event) {
      if (window.innerWidth > 599) {
        this.pc = true
      } else {
        this.pc = false
      }
    },
    openTab: function (url) {
      window.open(url, '_blank')
    },
    isPC: function () {
      var userAgentInfo = navigator.userAgent
      var Agents = ['Android', 'iPhone', 'SymbianOS', 'Windows Phone', 'iPad', 'iPod']
      var flag = true
      for (var v = 0; v < Agents.length; v++) {
        if (userAgentInfo.indexOf(Agents[v]) > 0) {
          flag = false
          break
        }
      }
      return flag
    },
    timeCounter: function () {
      const timeStr = '2019/1/26 00:00'
      const startDate = new Date()
      const endDate = new Date(timeStr)
      const spantime = (endDate - startDate) / 1000
      const day = Math.floor(spantime / (24 * 3600))
      if (spantime > 0) {
        let number = require(`../assets/number_${Math.floor(day / 10)}.svg`)
        this.numberDom1.style.setProperty('background-image', `url(${number})`)
        number = require(`../assets/number_${Math.floor(day % 10)}.svg`)
        this.numberDom2.style.setProperty('background-image', `url(${number})`)
      }
    },
    parseTimestamp: function (timestamp) {
      const time = new Date(timestamp._seconds * 1000)
      const str = `${time.getFullYear()}/${time.getMonth() + 1}/${time.getDate()}`
      return str
    }
  }
}
</script>

<style lang="scss" scoped>
  .main_page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    justify-content: flex-start;
    height: 100%;
    width: 100%;
    min-width: 1000px;
    background: linear-gradient(180deg, #DAD0F2 0%, #FCDBE3 100%);
  }
  .news_top_bar_pc {
    display: flex;
    flex-direction: row;
    justify-content: center;
    z-index: 100;
    background: #FCDBE3;
    width: 100%;
    height: 16vh;
    box-shadow: 0 0 3px 1px rgba(51, 51, 51, 0.5);
    .news_top_bar_layout {
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: row;
      justify-content: center;
      justify-items: center;
      align-items: center;
      align-content: center;
      .top_logo{
        width: 30%;
        height: 100%;
        margin-left: 0.5%;
        margin-right: 0.5%;
        background-image: url("../assets//logoHome_white.png");
        background-repeat: no-repeat;
        background-size: 85% 46%;
        background-position: center;
        transition: filter .8s ease;
        cursor: pointer;
          &:hover {
            filter: brightness(105%);
          }
          &:active {
            filter: brightness(80%);
          }
      }
      .top_bar{
        width: 60%;
        height: 50%;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-content: center;
        align-items: center;
        
        color: #0C3759;
        background: linear-gradient(to right, #FCDEE7 0%, #FCF4D3 100%);
        box-shadow: 0px 2px 2px 1px rgba(105, 103, 103, 0.424);
        border-radius: 147px;
        label {
          margin: 0.8vw;
          font-size: 180%;
          background-color: transparent;
          &:hover {
            filter: brightness(150%);
            font-weight: 700;
          }
          &:active {
            filter: brightness(80%);
            font-weight: 700;
          }
        }
        .active{
          font-weight: 700;
          border-bottom: 1mm solid white;
        }
      }
    }
  }
  .intro_layout {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 84vh;
    align-items: center;
    align-content: center;
    justify-items: flex-start;
    justify-content: flex-start;
    background: linear-gradient(180deg, #DAD0F2 0%, #FCDBE3 100%);
    overflow-y: scroll;
    overflow-x: hidden;
    // margin: 3vh;

    .intro_layout1{
      .test{
        display: flex;
        flex-direction: row;
        height: 100%;
        width: 100%;
        justify-items: center;
        justify-content: center;
        margin: 3vh 0 3vh 0;
        .intro_film{
          margin: 3vh 1vw 3vh 0;
          height: 70vh;
          width: 60vw;
          display: flex;
          flex-direction: column;
          justify-content: flex-start;
          justify-items: flex-start;
          border-radius: 0px;
          background-color: white;
          z-index: 100;
          .black1{
            height: 8vh;
            width: 100%;
            display: flex;
            flex-direction: row;
            justify-content: space-around;
            justify-items: center;
            align-content: center;
            align-items: center;
            background: #0C3759;
            .white_block{
              height: 60%;
              width: 2%;
              background: white;
            }
          }
          .black2{
            margin-top: 62vh;
            height: 8vh;
            width: 100%;
            display: flex;
            flex-direction: row;
            justify-content: space-around;
            justify-items: center;
            align-content: center;
            align-items: center;
            background: #0C3759;
            .white_block{
              height: 60%;
              width: 2%;
              background: white;
            }
          }
        }
        .intro_menu {
        display: flex;
        flex-direction: row;
        width: 35%;
        height: 70vh;
        justify-content: center;
        justify-items: center;
        align-content: center;
        align-items: center;
        margin: 3vh 0 3vh 1vw;
        z-index: 5;
        
        .intro_menu_l {
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          width: 50%;
          height: 100%;
          button{
            height: 170px;
            width: 170px;
            margin: 0.5vw;
            border-radius: 68px;
            border: 0px solid rgb(103, 192, 225);
            background-color: white;
            font-size: 240%;
            line-height: 67px;
            color: #769BFF;
            text-shadow: 0px 4px 4px rgba(12, 55, 89, 0.25);
            transition: filter .3s ease, border-width .2s ease, border-radius .2s ease;
            cursor: pointer;
            &:hover {
              border-width: 0.2vw;
              background-size: 90% 90%;
            }
            &:active {
              filter: brightness(50%);
            }
          }
        }
        .intro_menu_r {
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          width: 50%;
          height: 100%;
          button{
            height: 170px;
            width: 170px;
            margin: 0.5vw;
            border-radius: 68px;
            border: 0px solid rgb(103, 192, 225);
            background-color: white;
            font-size: 240%;
            line-height: 67px;
            color: #769BFF;
            text-shadow: 0px 4px 4px rgba(12, 55, 89, 0.25);
            transition: filter .3s ease, border-width .2s ease, border-radius .2s ease;
            cursor: pointer;
            &:hover {
              border-width: 0.2vw;
              background-size: 90% 90%;
            }
            &:active {
              filter: brightness(50%);
            }
          }
        }
        }
      }
    }
    .intro_layout2{
      .show_info1{
        height: 80vh;
        width: 80vw;
        margin: 4vh 0 4vh 0;
        border-radius: 49px;
        background-color: #C4C4C4;
      }
      .show_info2{
        height: 80vh;
        width: 80vw;
        margin: 4vh 0 4vh 0;
        border-radius: 49px;
        background-color: #584848;
      }
    }
  }
</style>
