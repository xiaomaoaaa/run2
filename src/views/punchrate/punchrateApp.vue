<template>
    <div>
        <div class="header2" id="header2">
            <div class="imgcon2" @click="gotoindex"><img :src="close" class="return"></div>
            公司打卡率
            <div class="bg22"></div>
        </div>
        <div class="header" id="header">
            <div class="imgcon" @click="gotoindex"><img :src="close" class="return"></div>
            <h1 class="headertit">公司打卡率</h1>
        </div>
        <div class="punchratelist">
            <div class="unit2">
                <div class="number"><img :src="imgurl"></div>
                <div class="borderbox">
                    <div class="logo" :class="{lxc:curitem.islxc,crj:curitem.iscrj}"></div>
                    <div class="info">
                        <p>{{curitem.company}}<span class="ml20">{{curitem.smallname}}</span></p>
                        <p><span class="w100">总人数：{{curitem.employeeCount}}人</span><span class="ml50">报名人数：{{curitem.userCount}}</span></p>
                    </div>
                    <div class="rate">
                        <p>打卡率</p>
                        <p>{{curitem.applyRate}}%</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="">
            <div class="unit" v-for="(item,index) in list" :key="index">
                <div class="number"></div>
                <div class="borderbox">
                    <div class="logo" :class="{lxc:item.islxc,crj:item.iscrj}"></div>
                    <div class="info">
                        <p>{{item.company}}<span class="ml20">{{item.smallname}}</span></p>
                        <p><span class="w100">总人数：{{item.employeeCount}}人</span><span class="ml50">报名人数：{{item.userCount}}</span></p>
                    </div>
                    <div class="rate">
                        <p>打卡率</p>
                        <p>{{item.applyRate}}%</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="bottom clearfix">
            <div class="left"></div>
            <div class="mid">没有更多了</div>
            <div class="right"></div>
        </div>
        <loading :show="show1" :text="text1"></loading>
    </div>
</template>
<script>
var browser = {
    versions: function() {
        var u = navigator.userAgent,
                        app = navigator.appVersion;
        return {
            trident: u.indexOf('Trident') > -1,
                         /*IE内核*/               
            presto: u.indexOf('Presto') > -1,
                  /*opera内核*/               webKit: u.indexOf('AppleWebKit') > -1,
            /*苹果、谷歌内核*/
             gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1,
                 /*火狐内核*/                
            mobile: !!u.match(/AppleWebKit.*Mobile.*/),
                 /*是否为移动终端*/                
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/),
            /*ios终端*/
              android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1,
            /*android终端或者uc浏览器*/
            iPhone: u.indexOf('iPhone') > -1,
                  /*是否为iPhone或者QQHD浏览器*/
            iPad: u.indexOf('iPad') > -1,
                /*是否iPad*/                
            webApp: u.indexOf('Safari') == -1,
                  /*是否web应该程序，没有头部与底部*/                souyue: u.indexOf('souyue') > -1,
                           superapp: u.indexOf('superapp') > -1,
                           weixin: u.toLowerCase().indexOf('micromessenger') > -1,
                           Safari: u.indexOf('Safari') > -1
        };
    }(),
    language: (navigator.browserLanguage || navigator.language).toLowerCase()

};
import axios from 'axios';
import Lib from 'assets/js/Lib';
require('assets/css/punchrate.css');
var close = require('assets/images/close.png');
window.jsBbridge = function(callback) {
    if (window.WebViewJavascriptBridge) {
        return callback(WebViewJavascriptBridge);
    } else {
        document.addEventListener(
            'WebViewJavascriptBridgeReady',
            function() {
                callback(WebViewJavascriptBridge)
            },
            false
        );
    }
    if (window.WVJBCallbacks) {
        return window.WVJBCallbacks.push(callback);
    }
    window.WVJBCallbacks = [callback];
    var WVJBIframe = document.createElement('iframe');
    WVJBIframe.style.display = 'none';
    WVJBIframe.src = 'wvjbscheme://__BRIDGE_LOADED__';
    document.documentElement.appendChild(WVJBIframe);
    setTimeout(function() {
        document.documentElement.removeChild(WVJBIframe)
    }, 0);
};
import {
    Loading
}
from 'vux'
export default {
    components: {
        Loading
    },
    data() {
        return {
            close: close,
            show1: false,
            text1: '数据加载中...',
            list: [],
            list: [{
                "id": 1,
                "company": "集团（含小麦、蓝海）",
                "employeeCount": "284",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 2,
                "company": "集团驻京",
                "employeeCount": "85",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 3,
                "company": "杭州外语（含预科）",
                "employeeCount": "205",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 4,
                "company": "浙江分公司",
                "employeeCount": "299",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 5,
                "company": "乐学城",
                "employeeCount": "37",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 6,
                "company": "出入境公司（含各地出入境）",
                "employeeCount": "77",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 7,
                "company": "北京",
                "employeeCount": "81",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 8,
                "company": "北京外语",
                "employeeCount": "33",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 9,
                "company": "天津",
                "employeeCount": "122",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 10,
                "company": "大连",
                "employeeCount": "21",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 11,
                "company": "青岛（含外语）",
                "employeeCount": "18",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 12,
                "company": "山西（含外语）",
                "employeeCount": "43",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 13,
                "company": "陕西",
                "employeeCount": "123",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 14,
                "company": "长春",
                "employeeCount": "18",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 15,
                "company": "河南",
                "employeeCount": "84",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 16,
                "company": "沈阳",
                "employeeCount": "23",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 17,
                "company": "武汉",
                "employeeCount": "51",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 18,
                "company": "成都",
                "employeeCount": "73",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 19,
                "company": "广州",
                "employeeCount": "65",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 20,
                "company": "济南",
                "employeeCount": "37",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 21,
                "company": "南昌",
                "employeeCount": "30",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 22,
                "company": "南京",
                "employeeCount": "56",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 23,
                "company": "宁波（含外语、舟山）",
                "employeeCount": "120",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 24,
                "company": "厦门（含福州、泉州）",
                "employeeCount": "126",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 25,
                "company": "上海",
                "employeeCount": "41",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 26,
                "company": "深圳（含外语）",
                "employeeCount": "127",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 27,
                "company": "苏州（含外语）",
                "employeeCount": "28",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 28,
                "company": "温州（含外语）",
                "employeeCount": "35",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 29,
                "company": "湖南",
                "employeeCount": "16",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 30,
                "company": "安徽",
                "employeeCount": "49",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 31,
                "company": "重庆",
                "employeeCount": "26",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 32,
                "company": "夏恩",
                "employeeCount": "32",
                "userCount": "0",
                "applyRate": "0"
            }, {
                "id": 33,
                "company": "新通悉尼",
                "employeeCount": "2",
                "userCount": "0",
                "applyRate": "0"
            }],

            imgurl: '',
            curitem: {},

        }
    },
    methods: {
        gotoindex() {
                var isIos = browser.versions.ios;
                if (isIos) {
                    // window.location.href = "../home/index.vm"
                    jsBbridge(function(bridge) {
                        bridge.callHandler(
                            'pageBack', {
                                // phone: self.phoneNo,
                                // userName: self.name,
                                // countryName: self.nationvaltext,
                                // specialDate: self.timetext
                            },
                            //回调函数
                            function(responseData) {

                            }
                        )
                    })
                } else {
                    yxapp.pageBack();
                }


            }

    },
    mounted() {
        // var curcompany="深圳（含外语）";
        // var curcompany=getParameter("company");
        // var self = this;
        // var temarr = [];
        // self.list.forEach(function(el, index) {
        //     if(el.company==curcompany){
        //      // var imgurl=document.getElementById('imgurl').value;
        //        self.imgurl="http://10.10.11.26:8083/run/resources/gen/img/"+"img_rank_"+(index+1)+".png";
        //        self.curitem=el;
        //     }

        //     var index = el.company.indexOf("（");
        //     if (index > -1) {
        //         el.smallname = el.company.substring(index);
        //         el.company = el.company.substring(0, index);
        //     }
        //     if (el.id == 5) {
        //         el.islxc = true;
        //     }
        //     if (el.id == 6) {
        //         el.iscrj = true;
        //     }
        //     temarr.push(el);
        // })
        // self.list = temarr;
        // console.log( self.curitem);
        // var pagetitle = "出入境公司（含各地出入境）"; //由原生传公司名称给我,先写死
        var curcompany = decodeURI(getParameter("company"));

        // this.show1 = true;
        var self = this;
        // var url = document.getElementById('punchrateUrl').value;
        // var imgurl = document.getElementById('imgurl').value;
        var i=7
        let imageurl=require("assets/images/"+i+".png")
        this.imgurl=imageurl
        console.log(imageurl)
        // axios.post(url, {})
        //     .then(function(response) {
        //         self.show1 = false;
        //         if (response.data.rc == 0) {
        //             var temarr = [];
        //             response.data.obj.forEach(function(el, index) {
        //                 if (el.company == curcompany) {

        //                     self.imgurl = imgurl + "img_rank_" + (index + 1) + ".png";
        //                     self.curitem = el;
        //                 }

        //                 var index = el.company.indexOf("（");
        //                 if (index > -1) {
        //                     el.smallname = el.company.substring(index);
        //                     el.company = el.company.substring(0, index);
        //                 }
        //                 if (el.id == 5) {
        //                     el.islxc = true;
        //                 }
        //                 if (el.id == 6) {
        //                     el.iscrj = true;
        //                 }
        //                 temarr.push(el);
        //             })
        //             self.list = temarr;
        //             console.log(self.curitem);
        //         }
        //     })
        //     .catch(function(error) {
        //         self.show1 = false;
        //     });
    },
    watch: {



    },

}
window.onscroll = function() {
    //变量t就是滚动条滚动时，到顶部的距离
    var t = document.documentElement.scrollTop || document.body.scrollTop;
    var header2 = document.getElementById("header2"),
        header = document.getElementById("header");
    if (t >= 100) { //当拖动到距离顶部100px处时，左边导航固定，不随滚动条滚动
        header2.style.display = "block";
        header.style.display = "none";
    } else {
        header2.style.display = "none";
        header.style.display = "block";
    }
}

function getParameter(param) {
    var query = window.location.search;
    var iLen = param.length;
    var iStart = query.indexOf(param);
    if (iStart == -1)
        return "";
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
