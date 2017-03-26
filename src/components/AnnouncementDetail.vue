<template>

  <div>

    <scroller height="-120" lockX=false scrollbarY=true>
      <div class="div-padding">

        <swiper :list="list" :min-moving-distance="20" auto="" direction="horizontal" height="200px"></swiper>



        <table  style="padding:30px 0px 0px 0px;">
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

        <a>传递过来的id为{{id}}</a>
        <li v-for="item in datas">
          {{item.latitude}}
        </li>


      </div>
    </scroller>



    <div class="css-auto" >
      <table height="100%" width="100%">
        <tr>
          <td align="left" style="padding:0px 0px 0px 15px;">
            <a>教师版</a>
          </td>
          <td align="right" style="padding:0px 15px 0px 0px;"  >
            <x-button type="primary"  action-type="button"   @click.native="toDownload()">下载</x-button>
          </td>
          <td align="left" style="padding:0px 0px 0px 15px;">
            <a>家长版</a>
          </td>
          <td align="right" style="padding:0px 15px 0px 0px;" >
            <x-button type="primary"  action-type="button"   @click.native="toDownload()">下载</x-button>
          </td>
        </tr>
      </table>
    </div>
  </div>

</template>

<script>
import Vue from 'vue';
//import Swiper from 'vux';
import { Group, Cell, Tab, TabItem, Swiper, SwiperItem, Card, Scroller ,XButton} from 'vux'


export default {
  datas:'',
  name: 'AnnouncementDetail',
  data () {
    return {
      msg: 'ParentsCycle',
      datas:'',
      list: [{
        url: 'http://www.baidu.com',
        img: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1489388986814&di=b1e6c9b10e2f622cb2702df59e0fd009&imgtype=0&src=http%3A%2F%2Fpic1.5442.com%3A82%2F2015%2F0409%2F01%2F15.jpg%2521960.jpg',
        title: '如何手制一份秋意的茶？'
      }, {
        url: 'http://www.baidu.com',
        img: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1489388986813&di=ed1de05af89e6a6b95597d49a1105a12&imgtype=0&src=http%3A%2F%2Fpic.58pic.com%2F58pic%2F17%2F14%2F25%2F43Y58PICfJB_1024.jpg',
        title: '茶包VS原叶茶'
      }, {
        url: 'http://www.baidu.com',
        img: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1489388986813&di=4aac1d6a4d6bfa16a10210c4ffb98e31&imgtype=0&src=http%3A%2F%2Fwww.pp3.cn%2Fuploads%2F20120713j%2F867.jpg',
        title: '播下茶籽，明春可发芽？'
      }],
      id:'',
      schoolname:'test schoolname',
      schoolphone:'test schoolphone',
      schooladdress:'test schooladdress',
      title:'test tile',
      content:'test content hksdjfklsdjfksldfjskli   jssss         dsfsf          sdfsdf              niininisdfsdf     sdfsdfs '
    }
  },components:{
    Group,
    Cell,
    Tab,
    TabItem,
    Swiper,
    SwiperItem,
    Card,
    Scroller,
    XButton
  },mounted() {
    var url;
    //http://localhost:8080/#/?id=8879
//    url = "http://123.206.43.102:8080/support/announcement/announcementList";
    // url = "http://yestp.com/api/attendance/getAllLocation";
      url = "http://localhost:8081/attendance/getAllLocation";


      this.$http.jsonp(url)
        .then(function (response) {
          console.log(response)
          this.datas = response.data.obj;
      }, function (response) {
          // error callback
        console.log('failed')
      });

      this.id = this.$route.query.id;
      console.log("the id" + this.$route.query.id + " the name:" + this.$route.query.name);
      console.log("hah finish");

  },methods: {
        toDownload: function() {
            alert("下载");
            console.log("will download");
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
  float:left;
  background:#F00;
}

.title-text-size {
    font-size:25px
}

.css-auto{margin:0 auto;width:100%;height:60px;position:static;bottom:0px;background:#3C3C3C;display:block;}

.div-padding {
  padding-right: 10px;
  padding-left: 10px;
  padding-bottom: 300px;

}

</style>
