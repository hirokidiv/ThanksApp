<template>
  <div class="main-box">
    <div class="main-header">
      <div class="main-header-left">
        受け取ったサプライズサンクス
        <img class="send-img" src="~zibunno.png" alt="zibunno.png">
      </div>
      <div class="main-header-right">
        <div class="back">
        </div>
        <div class="month">
          前の月
        </div>
        <div class="select-month">
          3月
        </div>
        <div class="month">
          次の月
        </div>
        <div class="next">
        </div>
      </div>
    </div>
    <div class="messages-box">
      <transition-group enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutUp" appear>
        <li v-for="(thank, index) in thanks" :key="thank.id" class="message-box">
          <a href="#" class="thank-show-link">
            <div class="icon">
              <img class="logo" src="~person.png">
            </div>
            <div class="receiver-box">
              <div class="receiver-name">
                {{ senders[index]}}  さん
              </div>
              <div class="receiver-message">
                {{thank.text}}
              </div>
            </div>
            <div class="message-status">
              未開封
            </div>
          </a>
        </li>
      </transition-group>
    </div>
    <div class="main-footer">
      <a href="/">
        <div class="main-footer-left">
          戻る
        </div>
      </a>
      <div class="main-footer-right">
        <div class="back">
        </div>
        <div class="month">
          前へ
        </div>
        <div class="select-month">
          {{thanks.length}}件中 1-{{thanks.length}}件
        </div>
        <div class="month">
          次へ
        </div>
        <div class="next">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import 'person.png';
import 'send.png';
import 'zibunno.png';


export default {
  data: function(){
    return{
      thanks: [],
      senders: []
    }
  },
  created() {
    var url = location.pathname + ".json"
    axios
      .get(url)
      .then(response => {
        var thanks = response.data.receive_thanks
        this.$data.thanks = thanks
        this.$data.senders = response.data.senders

        // 詳細ページに飛ぶためのリンク
        // var array = []
        // thanks.forEach(thank => {
        //   var url = "/thanks/" + thank.id + "/edit"
        //   array.push(url);
        // });
        // this.sidebarThanks.editUrls = array
      });
  }
}
</script>

<style scoped>
.main-box {
  height: calc( 100vh - 100px);
  width: 800px;
  margin: auto;
}

.main-header {
  height: 120px;
}

.main-header-left {
  height: 50px;
  width: 370px;
  position: relative;
  background: #FFC152;
  border-radius: 5px;

  font-family: Noto Sans CJK JP;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
  line-height: 50px;

  text-align: center;
  letter-spacing: 0.05em;

  color: #FFFFFF;
}

.send-img {
  height: 100px;
  width: 100px;
  position: absolute;
  top: -35px;
  right: -50px;
}

.main-header-right {
  display: flex;
  height: 50px;
  width: 370px;
  margin: 10px 0 0 430px;
  border-radius: 5px;
}

.back {
  width: 0px;
  height: 0px;
  margin-left: 155px;
  border-top: 10px solid transparent;
  border-right: 10px solid;
  border-bottom: 10px solid transparent;
}

.month {
  margin: 0 20px;
  font-size: 14px;
}

.select-month {
  font-family: Noto Sans CJK JP;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 20px;
  /* identical to box height */

  text-align: center;
  letter-spacing: 0.05em;
}

.next {
  width: 0px;
  height: 0px;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 10px solid;
}
.messages-box {
  border: 1px solid #555555;
  box-sizing: border-box;
}

.message-box {
  display: flex;
  height: 120px;
  border: 1px dashed #555555;
  background: #FFFFFF;
}

.icon {
  width: 200px;
}

.receiver-box {
  width: calc(100% - 230px);
  padding: 5px 5px;
}

.message-status {
  width: 30px;
  text-align: center;
  border-left: dotted 2px black;
  background-color: #FFC967;
  padding-top: 25px;
}


.receiver-name {
  font-family: Noto Sans CJK JP;
  font-style: normal;
  font-weight: normal;
}

.receiver-message {
  padding-top: 3px;
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  text-overflow: ellipsis;
  word-break: break-word;
  overflow: hidden;
  height: 80px;
}

.logo {
  height: 80px;
  width: 80px;
  margin: 10% 30%;
}

.thank-show-link {
  display: flex;
  width: 100%;
}

.main-footer {
  height: 120px;
  margin-top: 30px;
  position: relative;
}

.main-footer-left {
  width: 120px;
  height: 40px;
  position: absolute;
  border-radius: 40px;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  background: #C4C4C4;
  color: #fff;
  margin-right: 200px;
  text-align: center;
  line-height: 40px;
}

.main-footer-right {
  display: flex;
  height: 50px;
  width: 500px;
  border-radius: 5px;
  position: absolute;
  right: -70px;
}

</style>
