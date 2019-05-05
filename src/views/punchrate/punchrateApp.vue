<template>
  <div>
    <div class="unit" id="self">
      <div class="number" :class="{one:curitem.rank==1}" v-if="curitem.rank==1"></div>
      <div class="number" :class="{two:curitem.rank==2}" v-if="curitem.rank==2"></div>
      <div class="number" :class="{three:curitem.rank==3}" v-if="curitem.rank==3"></div>
      <div class="number greater3" v-if="curitem.rank>3">
        <img :src="imgurl" >
      </div>
      <div class="borderbox">
        <div class="info">
          <p class="logo" :class="{lxc:curitem.islxc,crj:curitem.iscrj}">
            {{curitem.company}}
            <span class="ml20">{{curitem.smallname}}</span>
          </p>
          <p>
            <span class="w100">总人数：{{curitem.employeeCount}}人</span>
            <span class="ml50">报名人数：{{curitem.userCount}}</span>
          </p>
        </div>
        <div class="rate">
          <p>打卡率</p>
          <p>{{curitem.applyRate}}%</p>
        </div>
      </div>
    </div>
    <div id="line"></div>
    <div id="punchratelist">
      <div class="unit" v-for="(item,index) in list" :key="index">
        <div class="number"></div>
        <div class="borderbox">
          <div class="info">
            <p class="logo" :class="{lxc:item.islxc,crj:item.iscrj}">
              {{item.company}}
              <span class="ml20">{{item.smallname}}</span>
            </p>
            <p>
              <span class="w100">总人数：{{item.employeeCount}}人</span>
              <span class="ml50">报名人数：{{item.userCount}}</span>
            </p>
          </div>
          <div class="rate">
            <p>打卡率</p>
            <p>{{item.applyRate}}%</p>
          </div>
        </div>
      </div>
    </div>

    <loading :show="show1" :text="text1"></loading>
  </div>
</template>
<script>
import axios from "axios";
import Lib from "assets/js/Lib";
require("assets/css/punchrate.css");
import { Loading } from "vux";
export default {
  components: {
    Loading
  },
  data() {
    return {
      show1: false,
      text1: "数据加载中...",
      list: [],
      list: [
        {
          id: 1,
          company: "集团（含小麦、蓝海）",
          employeeCount: "284",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 2,
          company: "集团驻京",
          employeeCount: "85",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 3,
          company: "杭州外语（含预科）",
          employeeCount: "205",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 4,
          company: "浙江分公司",
          employeeCount: "299",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 5,
          company: "乐学幼教",
          employeeCount: "37",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 6,
          company: "海外投资事业部（含各地）",
          employeeCount: "77",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 7,
          company: "北京",
          employeeCount: "81",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 8,
          company: "北京外语",
          employeeCount: "33",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 9,
          company: "天津",
          employeeCount: "122",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 10,
          company: "大连",
          employeeCount: "21",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 11,
          company: "青岛（含外语）",
          employeeCount: "18",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 12,
          company: "山西（含外语）",
          employeeCount: "43",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 13,
          company: "陕西",
          employeeCount: "123",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 14,
          company: "长春",
          employeeCount: "18",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 15,
          company: "河南",
          employeeCount: "84",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 16,
          company: "沈阳",
          employeeCount: "23",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 17,
          company: "武汉",
          employeeCount: "51",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 18,
          company: "成都",
          employeeCount: "73",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 19,
          company: "广州",
          employeeCount: "65",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 20,
          company: "济南",
          employeeCount: "37",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 21,
          company: "南昌",
          employeeCount: "30",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 22,
          company: "南京",
          employeeCount: "56",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 23,
          company: "宁波（含外语、舟山）",
          employeeCount: "120",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 24,
          company: "厦门（含福州、泉州）",
          employeeCount: "126",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 25,
          company: "上海",
          employeeCount: "41",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 26,
          company: "深圳（含外语）",
          employeeCount: "127",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 27,
          company: "苏州（含外语）",
          employeeCount: "28",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 28,
          company: "温州（含外语）",
          employeeCount: "35",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 29,
          company: "湖南",
          employeeCount: "16",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 30,
          company: "安徽",
          employeeCount: "49",
          userCount: "0",
          applyRate: "0"
        },
        {
          id: 31,
          company: "重庆",
          employeeCount: "26",
          userCount: "0",
          applyRate: "0"
        }
      ],

      imgurl: "",
      curitem: {
        id: 6,
          company: "海外投资事业部（含各地）",
          employeeCount: "77",
          userCount: "0",
          applyRate: "0",
          iscrj:true,
          rank:5
      }
    };
  },
  methods: {},
  mounted() {
    // let selfboxH = document.querySelector("#self").offsetHeight;
    // let listboxH = document.documentElement.clientHeight - selfboxH - 10; //浏览器可视高度减去div#self高度和一个div#line的高度
    document.querySelector("#punchratelist").style.height =  document.documentElement.clientHeight + "px";
    
    //根据请求结果来渲染对应排名
    let temarr=[]
    this.list.map(el => {
      
      let index = el.company.indexOf("（");
      if (index > -1) {
        el.smallname = el.company.substring(index);
        el.company = el.company.substring(0, index);
      }
      if (el.company.indexOf('海外投资事业部') >-1) {
        el.iscrj = true;
      }
      if (el.company == "乐学幼教") {
        el.islxc = true;
      }
      temarr.push(el);
    });
    this.list=temarr
    let i = 12;
    this.imgurl = require("assets/images/" + i + ".png");
  },
  watch: {}
};

function getParameter(param) {
  var query = window.location.search;
  var iLen = param.length;
  var iStart = query.indexOf(param);
  if (iStart == -1) return "";
  iStart += iLen + 1;
  var iEnd = query.indexOf("&", iStart);
  if (iEnd == -1) {
    return query.substring(iStart);
  }

  return query.substring(iStart, iEnd);
}
</script>
<style>
</style>
