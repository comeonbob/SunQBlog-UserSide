<template>
    <transition name="fade" mode="out-in">
        <div>
            <div class="FriendUrlBac">
                <div class="FriendUrlTitle">
                    <div class="FriendUrlTitleText">前端朋友圈</div>
                    <div class="CreateFriendUrlButton" @click="OpenPopup">我也加入</div>
                </div>
            </div>
            <div class="UrlCardList FriendUrlCard">
                <div class="UrlCardTr">
                    <transition name="Fade">
                        <img src="../../static/img/FriendUrlPlaceholder.png" class="FriendUrlPlaceholderPC" v-if="FriendUrlPlaceholder">
                    </transition>
                    <transition name="Fade">
                        <img src="../../static/img/ArticleList.jpg" class="FriendUrlPlaceholderMobile" v-if="FriendUrlPlaceholder">
                    </transition>
                    <div class="UrlCardTd" v-for="item in FriendsUrlList" @click="OpenFriendUrl(item.FriendUrlAdress)">
                        <div class="UrlIconName">
                            <img v-bind:src="item.FriendUrlIcoUrl" v-if="item.FriendUrlIcoUrl">
                            <img src="../../static/img/DefaultHeadIcon.jpg" v-if="!item.FriendUrlIcoUrl">

                            <div class="UrlName">{{ item.FriendUrlNickName }}</div>
                        </div>
                        <div class="UrlSummary">{{ item.FriendUrlDescript }}</div>
                    </div>
                </div>
                <div class="ListBottom" v-if="AticleBottom">你滑到我底线啦</div>
                <Pagination v-on:PaginationToParent="ValueByPagition" ref="Pagi"></Pagination>
            </div>
            <div class="PopupWindow" v-show="Wrapper">
                <div class="FriendUrlWrapper" @click="ClosePopup"></div>
                <div :class="FadeAnimate ? 'FriendUrlCreateWindowFadeIn' : 'FriendUrlCreateWindowFadeOut'">
                    <div class="FriendUrlCreateWindowHeader">
                        加入朋友圈<span @click="ClosePopup"><i class="iconfont icon-fork IconfontSize"></i></span>
                    </div>
                    <div class="FriendUrlCreateWindowItem">
                        <div class="FriendUrlCreateWindowItemLeft">姓名/昵称：</div>
                        <div class="FriendUrlCreateWindowItemRight">
                            <input v-model="FriendUrlNickName"/>
                        </div>
                    </div>
                    <div class="FriendUrlCreateWindowItem">
                        <div class="FriendUrlCreateWindowItemLeft">博客地址：</div>
                        <div class="FriendUrlCreateWindowItemRight">
                            <input v-model="FriendUrlAdress"/>
                        </div>
                    </div>
                    <div class="FriendUrlCreateWindowItem">
                        <div class="FriendUrlCreateWindowItemLeft">图标地址：</div>
                        <div class="FriendUrlCreateWindowItemRight">
                            <input v-model="FriendUrlIcoUrl" placeholder="可以不填哦"/>
                        </div>
                    </div>
                    <div class="FriendUrlCreateWindowItem">
                        <div class="FriendUrlCreateWindowItemLeft">个人描述：</div>
                        <div class="FriendUrlCreateWindowItemRight">
                            <input v-model="FriendUrlDescript"/>
                        </div>
                    </div>
                    <div class="FriendUrlCreateWindowFooter">
                        <div class="FriendUrlSubmitButton" @click="FriendUrlSubmit">提交</div>
                        <div class="FriendUrlSubmitButton FriendUrlCancelButton" @click="ClosePopup">取消</div>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
  import Pagination from '../SonCompnent/Pagination';
  import Store from '../../store'

  export default {
    name: "FriendUrl",
    components:{
      Pagination:Pagination
    },
    data:function(){
      return{
        Wrapper:false,
        FriendUrlNickName:'',
        FriendUrlAdress:'',
        FriendUrlDescript:'',
        FriendsUrlList:'',
        FriendUrlIcoUrl:'',
        // 弹框显隐动画
        FadeAnimate:false,

        // 文章底线
        AticleBottom:false,

       FriendUrlPlaceholder:true
      }
    },
    methods:{
      // 关闭弹框
      ClosePopup:function () {
        var That = this;
        this.FadeAnimate = false;
        setTimeout(function () {
          That.Wrapper = false;
        },200)
      },
      // 弹出弹框
      OpenPopup:function () {
        this.Wrapper = true;
        this.FadeAnimate = true;
      },
      // 提交友链
      FriendUrlSubmit:function () {
        var That = this;
        if(this.FriendUrlNickName && this.FriendUrlAdress && this.FriendUrlDescript){
          this.SQFrontAjax({
            Url:'/api/FriendUrlCreate/foreend',
            UploadData:{
              FriendUrlNickName: this.FriendUrlNickName,
              FriendUrlAdress: this.FriendUrlAdress,
              FriendUrlDescript:this.FriendUrlDescript,
              FriendUrlIcoUrl:this.FriendUrlIcoUrl
            },
            Success:function () {
              Store.commit('ChangeTip',{
                Show: true,
                Title: '提交成功'
              });
              That.ClosePopup();
              That.GetFriendUrlList();
            }
          });
        }else {
          Store.commit('ChangeTip',{
            Show: true,
            Title: '请完善网站信息哦'
          });
        }
      },
      OpenFriendUrl:function(Url){
        window.open(Url);
      },
      //初始化友链列表
      GetFriendUrlList:function () {
        var That = this,
          mvpUrl = [],//记录有标记的数据
          newArray;

        this.SQFrontAjax({
          Url:'/api/FriendUrlRead/foreend',
          UploadData:{
            PagnationData: {
              Skip: 0,
              Limit: 16
            }
          },
          Success:function (data) {
            // 将有order标记的数据，按order顺序排在前面
            for(let i=0;i<data.length;i++){
              if(data[i].order){
                mvpUrl[data[i].order] = data[i];//根据数据order字段组成一个数组
                data.splice(i,1);
              }
            }
            newArray = mvpUrl.concat(data);    //得到一个将有标记的值提前了的数组

            That.FriendUrlPlaceholder = false;
            That.FriendsUrlList = newArray;
          }
        });
      },
      ValueByPagition:function (SelectPage) {
        var That = this;
        this.SQFrontAjax({
          Url: '/api/FriendUrlRead/foreend',
          UploadData: {
            PagnationData: {
              Skip:SelectPage * 16,
              Limit:16
            }
          },
          Success: function (data) {
            That.FriendsUrlList = That.FriendsUrlList.concat(data);
            if(data.length != 16){
              That.AticleBottom = true;
              // 停止分页器的滚动监听
              That.$refs.Pagi.SetUpdate(false);
            }else {
              That.$refs.Pagi.SetUpdate(true);
            }
          }
        });
      }
    },
    mounted:function(){
      this.GetFriendUrlList();
      // 切换Topbar高亮
      Store.commit("ChangeActive", 3);
    },
  }
</script>

<style scoped lang="less">
    @import '../../static/css/FriendUrl';
</style>
