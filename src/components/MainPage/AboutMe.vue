<template>
    <transition name="Fade" mode="out-in">
    <div>
        <div class="FlexContent">
            <div class="LeftPart">
                <div class="BigBlock">
                    <div class="TitleFontLine">My Info</div>
                    <p><i class="iconfont icon-person AboutMeIcon" style="color:#49a9ee"></i>94年选手，中原工学院软件本科毕业，三年前端开发经历，一年连锁品牌管理经验</p>
                    <p><i class="iconfont icon-aihao1 AboutMeIcon" style="color:#f46e65"></i>爱好篮球、跑步、吉他。喜爱车评、历史记录片、交朋友</p>
                    <p><i class="iconfont icon-tool AboutMeIcon" style="color:#3db8c1"></i>Layui、ElementUI、Vue.js、node</p>
                    <p><i class="iconfont icon-biaoqian AboutMeIcon" style="color:#3dbd7d"></i>阳光大叔、靠谱伙伴、傻大个</p>
                    <p><i class="iconfont icon-xiazai20 AboutMeIcon" style="color:#948aec"></i>郑州 二七区 嵩山路西三环</p>
<!--
                    <p><i class="iconfont icon-jianzhu AboutMeIcon" style="color:#f78e3d"></i></p>
-->
                </div>
                <div class="BigBlock AboutMeMarginTop">
                    <div class="TitleFontLine">Her Info</div>
                    <p><i class="iconfont AboutMeIcon icon-wangzhanxinxi" style="color:#f46e65"></i>本博客纯手工编写，木有使用第三方建站工具。前后端用到的东西都很基础，代码存放在github</p>
                    <p><i class="iconfont AboutMeIcon icon-quanju_qianduanjiemian" style="color:#3dbd7d"></i>用户端自己UI组件 + Vue.js，管理端使用ElementUI + Vue.js</p>
                    <p><i class="iconfont AboutMeIcon icon-fuwuqi" style="color:#f78e3d"></i>服务端语言使用node.js、框架使用Express</p>
                    <p><i class="iconfont AboutMeIcon icon-dataBase" style="color:#49a9ee"></i>数据库使用Mongo db</p>
                </div>
                <div class="BigBlock AboutMeMarginTop">
                    <div class="TitleFontLine TitleFontLineThank">Thanks You All</div>
                    <div class="UrlCardTr AboutPage">
                        <a class="UrlCardTd UrlCardTdBc" href="https://www.ruanyifeng.com/blog/javascript/" target="_blank">
                            <div class="UrlIconName UrlIconNameMargin">
                                <img src="../../static/img/DefaultHeadIcon.jpg">
                                <div class="UrlName">阮一峰的个人网站</div>
                            </div>
                        </a>
                        <a class="UrlCardTd UrlCardTdBc" href="http://bh-lay.com/" target="_blank">
                            <div class="UrlIconName UrlIconNameMargin">
                                <img src="http://bh-lay.com/touch-icon-ipad-retina.png">
                                <div class="UrlName">小剧博客</div>
                            </div>
                        </a>
                        <a class="UrlCardTd UrlCardTdBc" href="https://github.com/SunQQQ" target="_blank">
                            <div class="UrlIconName UrlIconNameMargin">
                                <img src="http://39.104.22.73:67/favicon.jpg">
                                <div class="UrlName">孙权的博客</div>
                            </div>
                        </a>
                    </div>
                </div>
            </div>
            <div class="RightPart">
                <div class="GitPart">
                    <div class="TopBackBlack"></div>
                    <div class="GitPic">
                        <img src="../../static/img/ZhihuIcon.jpg">
                    </div>
                    <div class="GitBack">
                        <i class="iconfont TopBackBlackGit icon-github1"></i>
                    </div>
                    <div class="Content">
                        <div class="GitName">孙权的Github</div>
                        <a class="BlueButton" href="https://github.com/SunQQQ" target="_blank">博客源码</a>
                        <div class="BlogStatistic">
                            <div class="BlogStatisticItem">
                                <div class="BlogStatisticItemNum">13</div>
                                <div class="BlogStatisticItemText AboutMeGitData">Followers</div>
                            </div>
                            <div class="BlogStatisticItem">
                                <div class="BlogStatisticItemNum">17</div>
                                <div class="BlogStatisticItemText AboutMeGitData">Repositories</div>
                            </div>
                            <div class="BlogStatisticItem">
                                <div class="BlogStatisticItemNum">88</div>
                                <div class="BlogStatisticItemText AboutMeGitData">Star</div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="BigBlock AboutMeMarginTop">
                    <div class="TitleFontLine">Contacts</div>
                    <div class="BlogStatistic" style="border-top: none;padding-bottom: 0">
                        <div class="BlogStatisticItem">
                            <a href="https://github.com/SunQQQ" target="_blank"><i class="iconfont icon-github AboutMeIcon" style="color:#948aec"></i></a>
                        </div>
                        <div class="BlogStatisticItem">
                            <a href="https://www.zhihu.com/people/s-q-51-44-23/activities" target="_blank"><i class="iconfont icon-zhihu AboutMeIcon" style="color:#3dbd7d"></i></a>
                        </div>
                        <div class="BlogStatisticItem">
                            <a href="https://blog.csdn.net/sun_qqq" target="_blank"><i class="iconfont icon-CN_csdnnet AboutMeIcon" style="color:#f78e3d"></i></a>
                        </div>
                        <div class="BlogStatisticItem">
                            <i class="iconfont icon-youxiang AboutMeIcon" style="color:#49a9ee"></i>
                        </div>
                        <div class="BlogStatisticItem">
                            <a href="https://music.163.com/#/user/home?id=386558098" target="_blank"><i class="iconfont AboutMeIcon icon-CN_NetEasemusic" style="color:#f46e65"></i></a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <Heartfelt></Heartfelt>
    </div>
    </transition>
</template>

<script>
  import Heartfelt from '../SonCompnent/Heartfelt';
  import Store from '../../store'

  export default {
    name: "AboutMe",
    components:{
      Heartfelt
    },
    mounted:function () {
      // 切换Topbar高亮
      Store.commit("ChangeActive", 4);
    }
  }
</script>

<style scoped lang="less">
    @import "../../static/css/AboutMe";

</style>
