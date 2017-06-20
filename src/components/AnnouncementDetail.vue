<template>

  <div>

    <div class="css-auto">
      <table height="100%" width="100%">
        <tr>
          <td align="left" style="padding:0px 0px 0px 15px;">
            <a v-model="versionName">{{versionName}}</a>
          </td>
          <td align="right" style="padding:0px 15px 0px 0px;width: 8rem">
            <x-button type="primary" action-type="button" @click.native="toDownload()">下载</x-button>
          </td>
        </tr>
      </table>
    </div>

    <div style="height:60px;line-height:60px;font-size:30px;width:100%;text-align:center">父母圈</div>

    <div class="div-padding">

      <swiper :list="list" :min-moving-distance="20" auto="" direction="horizontal" height="200px"></swiper>


      <table style="padding:30px 0px 0px 0px;">
        <tr class="title-text-size">
          <td align="left">{{title}}</td>
        </tr>
        <tr>
          <td align="left">{{content}}</td>
        </tr>
        <tr>
          <td align="left" style="padding:30px 0px 0px 0px;">{{schoolname}}</td>
        </tr>
        <tr>
          <td align="left">{{schooladdress}}</td>
        </tr>
        <tr>
          <td align="left">{{schoolphone}}</td>
        </tr>
      </table>

      <!--<a>传递过来的id为{{id}}</a>-->
      <!--<br/>-->
      <!--<a>请求过来的数据为:</a>-->
      <!--<li v-for="item in datas">-->
      <!--{{item.title}}-->
      <!--</li>-->


    </div>


  </div>

</template>

<script>
  import Vue from 'vue';
  //import Swiper from 'vux';
  import {Group, Cell, Tab, TabItem, Swiper, SwiperItem, Card, Scroller, XButton} from 'vux'


  export default {
    datas: '',
    name: 'AnnouncementDetail',
    data () {
      return {
        msg: 'ParentsCycle',
        datas: '',
        list: [{
          url: '',
          img: '',
          title: ''
        }],
        id: '',
        version:-1,
        versionName:'',
        schoolname: 'test schoolname1',
        schoolphone: 'test schoolphone2',
        schooladdress: 'test schooladdress',
        title: 'test tile',
        content: 'test content '
      }
    }, components: {
      Group,
      Cell,
      Tab,
      TabItem,
      Swiper,
      SwiperItem,
      Card,
      Scroller,
      XButton
    }, mounted() {
      var url;
      url = "http://123.206.43.102:8080/support/announcement/announcementList?page=1&rows=100&announid=";
      this.id = this.$route.query.announid;
      this.version = this.$route.query.version; // 1：教师版  2:家长版
      if (parseInt(this.version) === 1) {
          this.versionName = "教师版";
      } else if (parseInt(this.version) === 2) {
          this.versionName = "家长版";
      }

      console.log("the version:" + this.versionName);

      url = url + this.id;

      this.$http.post(url)
        .then(function (response) {
          console.log(response)
          this.datas = response.data.obj;
          this.title = this.datas[0].title;
          this.content = this.datas[0].announcement;
          this.schooladdress = this.datas[0].detailedaddress;
          this.schoolphone = this.datas[0].contactnumber;
          this.schoolname = this.datas[0].schoolname;

          var imgArray = this.datas[0].imags.split(",");
          var resultArray = [];
          for (var i = 0; i < imgArray.length; i++) {
            var imgObj = {url: "", img: imgArray[i], title: ""};
            resultArray.push(imgObj);
          }
          this.list = resultArray;

        }, function (response) {

          console.log('failed')
        });

//      var locationUrl = "http://123.206.43.102:8080/support-token/announcement/announcementList?rows=1000&schoolid=69&token=eafc92a4de84975e451708ecebcba61f&type=1&page=1&id=305&";
//      this.$http.get(locationUrl)
//        .then(function (response) {
//          console.log(response)
//          this.schooladdress = response.data.msg;
//      }, function (response) {
//          // error callback
//        console.log('location request  failed')
//      });


    }, methods: {
      toDownload: function () {
        var u = navigator.userAgent;
        var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
        var isIos = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
        if (parseInt(this.version) === 1) {
          //教师版
          if (isAndroid) {
            alert("下载android1");
            window.open("http://123.207.140.176/app-school.apk");
          } else if (isIos) {
            //alert("下载ios");
            window.open("https://itunes.apple.com/cn/app/父母圈-教师版/id1219770725?mt=8");
          } else {
            window.open("http://123.207.140.176/app-school.apk");
          }
        } else if (parseInt(this.version) === 2) {
          //家长版
          if (isAndroid) {
            alert("下载android1");
            window.open("http://123.207.140.176/app-home.apk");
          } else if (isIos) {
            //alert("下载ios");
            window.open("https://itunes.apple.com/cn/app/父母圈-家长版/id1219770954?mt=8");
          } else {
            window.open("http://123.207.140.176/app-home.apk");
          }
        }


        console.log("will download");

      },
      toOtherUrl: function () {
        window.open("http://yestp.com?id=998&name=889");
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }

  .div-left {
    float: left;
    background: #F00;
  }

  .title-text-size {
    font-size: 25px
  }

  .css-auto {
    margin: 0 auto;
    width: 100%;
    height: 60px;
    position: static;
    bottom: 0px;
    background: #3C3C3C;
    display: block;
  }

  .div-padding {
    padding-right: 10px;
    padding-left: 10px;
    padding-bottom: 20px;

  }

</style>
