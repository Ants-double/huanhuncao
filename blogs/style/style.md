# 样式

- 基于SimpleMemory修改

## 页面定制css

``` css
#site_nav_under {
    display: none;
}
.c_ad_block, .ad_text_commentbox {
    display: none;
    margin: 0;
    padding: 0;
}
#ad_under_google {
    height: 0;
    overflow: hidden;
}
#ad_under_google a {
    display: none;
}


@charset "utf-8";
/* CSS Document */

/**************************************************
第一部分：所有的模板都使用的公共样式。公告样式是为了更好的向前和向后兼容。
如果不符合你皮肤的要求，你可以在后面通过更好的优先级覆盖着这些样式，但是
你不能删除这些样式。
**************************************************/
#EntryTag {
    margin-top: 20px;
    font-size: 9pt;
    color: gray;
}
.topicListFooter {
    text-align: right;
    margin-right: 10px;
    margin-top: 10px;
}
#divRefreshComments{
    text-align: right; 
    margin-right: 10px;
    margin-bottom: 5px;
    font-size: 9pt;
}
/*****第一部分结束*******************************/

/**************************************************
第二部：公共样式（全局样式）。公共会对所有页面的标签都起作用。这个部分你
可以随意的更改，并不会牵扯到其他的皮肤模板。但是每次更改都要注意你的皮肤
模板所有页面的变化。因为它们是全局的。
**************************************************/
* {
    margin: 0;
    padding: 0;
}
html {
    height: 100%;
}
body {
    background:url(https://i.loli.net/2017/08/15/59923c58cc40f.jpg) no-repeat fixed;
    background-size:cover;
    color:#000;
    font-family: "微软雅黑","verdana","ms song","宋体","Arial", "Helvetica", "sans-serif";
    font-size: 15px;
    min-height: 101%;    
    margin-left:auto;
    margin-right:auto;
    z-index:0;
}

#Uleft, #Uright,#Dleft, #Dright{
    /* Firefox 4 */
    -moz-transition-property:top; 
    -moz-transition-duration:1s;

    /* Safari and Chrome */
    -webkit-transition-property:top; 
    -webkit-transition-duration:1s;

    /* Opera */
    -o-transition-property:top;
    -o-transition-duration:1s;
    position: fixed;
    width: 80px;
    height: 80px;
    line-height: 500px;
    text-align: center;
    z-index:1;
}
#Uleft{
    width: 80px;
    height: 80px;
    top:-60px;
    left: 50px;
}
#Uright{
    width: 110px;
    height: 110px;
    top: -75px;
    right: 150px;
}
#Dleft{
    bottom:10px;
    left: 10px;
    width: 200px;
    height: 200px;
}
#Dright{
    bottom:-50px;
    right: 0px;
    width: 200px;
    height: 250px;
}

#MagicArray{
    /* Firefox 4 */
    -moz-transition-property:width height bottom right; 
    -moz-transition-duration:1s;

    /* Safari and Chrome */
    -webkit-transition-property:width height bottom right; 
    -webkit-transition-duration:1s;

    /* Opera */
    -o-transition-property:width height bottom right;
    -o-transition-duration:1s;

    position: fixed;
    bottom:107px;
    right: 108px;
    width: 0px;
    height: 0px;
    text-align: center;
    z-index:2;
}
#Tab1{
    -moz-transition-property:fontSize width height; 
    -moz-transition-delay:0.8s;

    -webkit-transition-property:fontSize width height; 
    -webkit-transition-delay:0.8s;

    -o-transition-property:fontSize width height;
    -o-transition-delay:0.8s;

    color:#8B0A50;
    position: fixed;
    font-size: 0px;
    text-align: center;
    z-index:3;
    font-weight:500;
    text-shadow:
        -1px 0 #7A67EE,
1px #7A67EE,
        1px 0 #7A67EE,
-1px #7A67EE;
}

::selection{background:#698B22;color:#FFF;}
::-moz-selection{background#698B22;color:#FFF;}
/*
body{cursor:url('https://www.cnblogs.com/images/cnblogs_com/billly/1411802/o_heart.png'),auto;}
A{cursor:url('https://www.cnblogs.com/images/cnblogs_com/billly/1411802/o_Mouse.png'),auto;}
*/


input{outline:medium;}
/*
input{cursor:url('https://www.cnblogs.com/images/cnblogs_com/billly/1411802/o_Mouse.png'),auto;}
wait{cursor:url('https://www.cnblogs.com/images/cnblogs_com/billly/1411802/o_Mouse.png'),auto;}
http://fq.wc.lt//up/1499566113.cur
http://fq.wc.lt//up/1499565578.cur
http://fq.wc.lt//up/1499564884.cur
*/
/*鼠标*/

table {
    border-collapse: collapse;
    border-spacing: 0;
}
fieldset, img {
    border: 0;
}
ul {
    word-break: break-all;
}
li {
    list-style: none;
}
h1, h2, h3, h4, h5, h6 {
    font-size: 100%;
    font-weight: normal;
}
a:link {
    color:black;
    text-decoration:none;
}
a:visited {
    color:#111;
    text-decoration: none;
}
a:hover {
    color: #7B68EE;
    -moz-border-radius: 9px;
    -khtml-border-radius: 9px;
    -webkit-border-radius: 9px;
    border-radius: 9px;
    transition: all 0.4s linear 0s;
}
a:active {
    color: black;
    text-decoration: none;
}
.clear {
    clear: both;
}
/*****第二部分结束*******************************/
/****github****/
.git-link {
    z-index: 100;
    position: fixed;
    top: 0;
    right: 0;
    border: 0;
    height: 149px;
    width: 149px;
    transform: rotate(90deg);
    -webkit-transform: rotate(90deg);
    -moz-transform: rotate(90deg);
    -o-transform: rotate(90deg);
    -ms-transform: rotate(90deg);
    background-image: url(//images2015.cnblogs.com/blog/459873/201603/459873-20160317090540131-1089895320.png);
}

/**************************************************
第三部分：各个页面元素的样式。你可以根据需要随意的更改，并不会牵扯到其他
的皮肤模板。这个部分是最能展现你想象力的部分。其中头部和侧边栏部分是此皮
肤公共的部分。而每个页面特有的部分会有相应的注释和说明。
**************************************************/
/*****home和头部开始**************************/
#home {
    margin: 0 auto;
    width:95%;
    min-width: 60em;
}
#header {
    padding-bottom: 0.4em;
    margin-top: 0.8em;
}
#blogTitle {
    height: 7em;
    clear: both;
    border:1px solid #000;
    -moz-border-radius: 11px;
    -khtml-border-radius: 11px;
    -webkit-border-radius: 11px;
    border-radius: 12px;
    -webkit-box-shadow:5px 2px 6px #000;-moz-box-shadow:5px 2px 6px #000;padding:4px 10px;
    text-shadow:1px 1px 1px #e9f3e8
}
#blogTitle h1 {
    font-size: 300%;
    font-weight: bold;
    margin-left: 1em;
    margin-top: 0.4em;
    width: 50%;
    float: left;
}
#blogTitle h2 {
    margin-left: 6em;
    line-height: 1.5em;
    width: 50%;
    float: left;
    text-shadow:-1px 0 #ddd,
1px #ddd,
                1px 0 #ddd,
-1px #ddd;
}
#blogLogo {
    float: right;
}
#navigator {
/*    background-color: black;
    height: 30px;
    clear: both;*/

    margin-top:0.3em;
    height: 2em;
    clear:both;
    border:1px solid #999;
    -moz-border-radius: 11px;
    -khtml-border-radius: 11px;
    -webkit-border-radius: 11px;
    border-radius: 11px;
    -webkit-box-shadow:5px 2px 6px #000;-moz-box-shadow:5px 2px 6px #000;padding:4px 10px;
    background:#FFF;
    opacity: 0.80;
}
#navList {
    min-height: 1.5em;
    float: left;
}
#navList li {
    float: left;
}
#navList a {
    display: block;
    padding-left:0.5em;
    padding-right:0.5em;
    line-height:2em;
    float: left;
    text-align: center;
    border-right: 1px solid #999;
}
#navList a:link, #navList a:visited, #navList a:active {
/*    color: #ccc;*/
}
#navList a:hover {
    color: #7B68EE;
    padding-left:0.8em;
    padding-right:0.8em;
}

.blogStats {
    float: right;
    font-size:0.8em;
    color: #000;
    margin-top: 0.9em;
    margin-right: 0.2em;
    text-align: right;
}
/*****home和头部结束**************************/

/*****主页文章列表开始**************************/
#main{
    width: 100%;
    min-width: 70em;
    text-align: left;
    background: #f5f5f5;
    opacity: 0.85;
}
#mainContent .forFlow{
    margin-left: 12em;
    float: none; 
    width: auto;
}

#mainContent {
    min-height: 18em;
    padding: 0px 0px 10px 0;
    *padding-top:10px;
    -o-text-overflow: ellipsis;
    text-overflow: ellipsis;
    overflow: hidden;
    word-break: break-all;
    
    float: right;
    margin-left: -26em;
    width: 100%
}
.day {
    min-height: 10px;
    _height: 10px;
    margin-bottom: 20px;
    padding-bottom: 5px;
}
.dayTitle {
    width: 100%;
    color: #666;

    font-weight: bold;
    line-height: 1.5em;
    font-size: 90%;
    margin-top: 3px;
    margin-bottom: 10px;
    clear:both;
    border-bottom: 2px solid #e9f3e8;
    text-align:center;

}
.postTitle {
    font-size: 150%;
    font-weight: bold;
    /*border-bottom: 1px solid #9DAAF4;*/
    float: right;
    line-height: 1.5em;
    width: 100%;
    clear:both;
    text-shadow:-3px 3px 3px #999
}
.postTitle a:link, .postTitle a:visited, .postTitle a:active {
    color: #000;
    transition: all 0.4s linear 0s;
}
.postTitle a:hover {
    margin-left: 10px;
    color: #7B68EE;
    text-decoration: none;
    text-shadow:-13px 3px 3px #999
}
.postCon {
    float: right;
    line-height: 1.5em;
    width: 100%;
    clear:both;
    padding: 10px 0;
}
.postDesc {
    float: right;
    width: 100%;
    clear:both;
    text-align: right;
    padding-right: 5px;
    color: #666;
    margin-top: 5px;
}
.postDesc a:link, .postDesc a:visited, .postDesc a:active {
    color: #666;
    padding-right: 10px;
}
.postDesc a:hover {
    color: #7B68EE;
    text-decoration: none;
}
.postSeparator {
    clear: both;
    height: 1px;
    border-top: 1px dotted #666;
    width: 100%;
    clear:both;
    float: right;
    margin: 0 auto 15px auto;
}
.diggit{
    text-align: center;
    width:50px;
    height:40px;
    background:url(https://www.cnblogs.com/images/cnblogs_com/billly/1411802/o_haha.png);
    background-size:100% 100%;
}
.buryit{
    font-size:0px;
    width:0;
    height:0;
}
.burynum{
    font-size:0px;
    width:0;
    height:0;
}
/*****主页文章列表结束**************************/

/*****侧边栏开始********************************/
#sideBar {
    width: 14em;
    min-height: 14em;
    padding: 0px 0px 0px 5px;
    float: left;
    -o-text-overflow: ellipsis;
    text-overflow: ellipsis;
    overflow: hidden;
    word-break: break-all;
    font-size:0.7em;
    opacity:0.9;
}
.counter{
}
.notice{
    font-size:xx-small;
}
.btn_my_zzk{
  display: inline-block;
  font-size: 24px;
  cursor: pointer;
  text-align: center;   
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #a55b97;
  border: none;
  border-radius: 15px;
  box-shadow: 0 4px #999;
}
.newsItem .catListTitle {
    display: none;
}
.newsItem {
    padding: 15px 0 5px 0px;
    font-weight:bold;
    font-size:14px;
    margin-bottom: 8px;
}
/**日历控件样式开始**/
#calendar {
    width: 14em;
}
#calendar .Cal {
    width: 100%;
    line-height: 1.5em;
}
.Cal {/**日历容器table**/
    border: none;
    color: #111;
}
#calendar table a:link, #calendar table a:visited, #calendar table a:active {
    font-weight: bold;
}
#calendar table a:hover {
    color: #7B68EE;
    text-decoration: none;
    background-color: #7B68EE;
}
.CalTodayDay{/**今天日期样式**/
    color: #EE82EE;
}
#calendar .CalNextPrev a:link,#calendar  .CalNextPrev a:visited, #calendar .CalNextPrev a:active {/**上个月、下个月箭头样式**/
    font-weight: bold;
    background-color: #7B68EE;
}
.CalDayHeader{
    border-bottom:1px solid #ccc;    
}
.CalTitle{/**日历年月头部样式**/
    width:100%;
    background:#FFF;
    color:black;
    border-bottom:1px solid #666;    
}
/**日历控件样式结束**/
.catListTitle {
    font-weight: bolder;
    font-family:STCaiyun;
    color:     #B03060;
    line-height: 2em;
    font-size: 150%;
    margin-top: 50px;
    margin-bottom: 10px;
    border-bottom: 1px solid #e9f3e8;
    text-align: center;
}
.catListComment {
    line-height: 1.5em;
}
.divRecentComment {
    color: #666;
    margin-bottom:1em;
}
.c_b_p_link_desc{
    color: #666;
    font-size: 30%;
    margin-bottom:1.5em;
}
#sideBarMain ul {
    line-height: 1.5em;
}
.catListEssay{
    font-weight: bolder;
}
.catListTag{
    font-size: 90%;
    font-weight: bolder;
}
.catList{
    font-weight: bolder;
}
.catListFeedback{
    font-weight: bolder;
}
.catListView{
    font-weight: bolder;
}
.recent_comment_title{
    font-weight: bolder;
}
.recent_comment_body{
    font-size: 30%;
}
.recent_comment_author{
    color:#666;
    font-size: 30%;
}
/*****侧边栏结束********************************/


/****查看文章页面开始*************************/
#topics {
    width: 100%;
    min-height: 18em;
    padding: 0px 0px 10px 0;
    float: left;
    -o-text-overflow: ellipsis;
    text-overflow: ellipsis;
    overflow: hidden;
    word-break: break-all;
}
#topics .postTitle {
    font-size: 200%;
    font-weight: bold;
    border-bottom: 1px solid #999;
    float: left;
    line-height: 1.5em;
    width: 100%;
    text-align: center;
}
.postBody {
    padding: 5px 2px 5px 5px;
    line-height: 1.5em;
    color: #000;
    border-bottom: 1px solid #8686FF;
}
#EntryTag {
    color: #000;
}
#EntryTag a {
    margin-left: 5px;
}
#EntryTag a:link, #EntryTag a:visited, #EntryTag a:active {
    color: #000;
}
#EntryTag a:hover {
    color: #7B68EE;
}
#topics .postDesc {
    float: right;
    width: 100%;
    font-size:0.9em;
    text-align: right;
    padding-right: 5px;
    color: #000;
    margin-top: 5px;
}
.feedback_area_title {
    font-weight: bold;
    margin-top: 20px;
    border-bottom: 1px solid #8686FF;
    margin-bottom: 10px;
    padding-left: 8px;
}
.louzhu {
    background:transparent url('/images/icoLouZhu.gif') no-repeat scroll right top;
    padding-right:16px;
}
.layer{
    font-family:STFangsong;
    font-size:15px;
    padding-left: 8px;
}
.feedbackListSubtitle {
    margin-left: 10px;
    color: #666;
    font-size:0.9em;
}
.feedbackListSubtitle a:link, .feedbackListSubtitle a:visited, .feedbackListSubtitle a:active {
    font-weight:bold;
    color: #666;
    font-weight: normal;
}
.feedbackListSubtitle a:hover {
    color: #7B68EE;
    text-decoration: none;
}
.feedbackManage {
    width: 160px;
    text-align: right;
    float: right;
}
.feedbackCon {
    font-weight:bold;
    border-bottom: 1px solid #ccc;
    padding: 15px 18px 20px 50px;
    min-height: 35px;
    _height: 35px;
    margin-bottom: 1em;
    line-height: 1.5em;
    width:80%;
}
#divRefreshComments {
    text-align: right;
    margin-bottom: 10px;
}
.commenttb {
    width: 320px;
}
.cnblogs_code{
}
.comment_actions{
    margin-right:30px;
    font-size:16px;
    font-family:STFangsong;
}
.comment_digg{
    font-weight:bold;
    margin-right:10px;
    font-size:15px;
    font-family:STXinwei;
}
.comment_bury{
    font-weight:bold;
    margin-right:10px;
    font-size:15px;
    font-family:STXinwei;
}
/****查看文章页面结束************************

/****列表页面开始******************************/
.entrylistTitle,.PostListTitle,.thumbTitle{/**几个分类列表的标题样式**/
    font-size: 110%;
    font-weight: bold;
    border-bottom: 1px solid #8686FF;
    text-align: right;
    padding-bottom: 3px;
    padding-right: 10px;
}

.entrylistDescription {
    color: #666;
    text-align: right;
    padding-top: 5px;
    padding-bottom: 5px;
    padding-right: 10px;
    margin-bottom: 10px;
}
.entrylistItem {
    min-height: 20px;
    _height: 20px;
    margin-bottom: 30px;
    padding-bottom: 5px;
    width: 100%;
}
.entrylistPosttitle {
    font-size: 110%;
    font-weight: bold;
    border-bottom: 1px solid #666;
    line-height: 1.5em;
    width: 100%;
    padding-left: 5px;
}
.entrylistPosttitle a:hover {
    text-decoration: none;
}
.entrylistPostSummary {
    margin-top: 5px;
    padding-left: 5px;
    margin-bottom: 5px;
}
.entrylistItemPostDesc {
    padding-left: 50px;
    text-align: right;
    color: #666;
}
.entrylistItemPostDesc a:link, .entrylistItemPostDesc a:visited, .entrylistItemPostDesc a:active {
    color: #666;
}
.entrylistItemPostDesc a:hover {
    color: #7B68EE;
}
.entrylist .postSeparator {
    clear: both;
    width: 100%;
    font-size: 0;
    line-height: 0;
    margin: 0;
    padding: 0;
    height: 0;
    border: none;
}

.pager {
    text-align: right;
    margin-right: 10px;
}
.PostList {
    border-bottom: 1px solid #ccc;
    clear: both;
    min-height: 1.5em;
    _height: 1.5em;
    padding-top: 10px;
    padding-left: 5px;
    padding-right: 5px;
    margin-bottom: 5px;
}
.postTitl2 {
    float: left;
    font-size:0.9em;
    color: #666;
}
.postDesc2 {
    color: #666;
    float: right;
    margin-right: ;
    font-size:0.9em;
}
.postText2 {
    clear: both;
    
}
.pfl_feedback_area_title {
    text-align: right;
    line-height: 1.5em;
    font-weight: bold;
    border-bottom: 1px solid #666;
    margin-bottom: 10px;
}
.pfl_feedbackItem {
    border-bottom: 1px solid black;
    margin-bottom: 20px;
}
.pfl_feedbacksubtitle {
    width: 100%;
    border-bottom: 1px dotted #666;
    height: 1.5em;
}
.pfl_feedbackname {
    float: left;
}
.pfl_feedbackManage {
    float: right;
}
.pfl_feedbackCon {
    color: black;
    padding-top: 5px;
    padding-bottom: 5px;
}
.pfl_feedbackAnswer {
    color: #F40;
    text-indent: 2em;
}
.tdSentMessage {
    text-align: right;
}
.errorMessage {
    width: 300px;
    float: left;
}

/****列表页面结束******************************/*/
/****相册页面开始******************************/
.divPhoto {
    border: 1px solid #ccc;
    padding: 2px;
    margin-right: 10px;
}

.thumbDescription {
    color: #666;
    text-align: right;
    padding-top: 5px;
    padding-bottom: 5px;
    padding-right: 10px;
    margin-bottom: 10px;
}
/****相册页面结束******************************/


/*****留言页面开始*****************************/
#green_channel {
    padding: 10px 0;
    margin-bottom: 10px;
    margin-top: 10px;
    border: silver 1px dashed;
    font-size: 12px;
    width: 100%;
    text-align: center;
}
#footer {
    text-align: center;
    min-height: 15px;
    _height: 15px;
    border-top: 1px solid black;
    margin-top: 10px;
    padding-top: 10px;
    margin-bottom: 10px;
}
/*留言查看页面的个人信息*/
.personInfo {
    margin-bottom: 20px;
}
/*留言分页区域*/
.pages {
    text-align: right;
}
/*****留言页面结束*****************************/
/*****第三部分结束*******************************/

/**************************************************
第四部分：文章内容常用标签格式。这个部分是设置作者写作内容的部分。例如：
如果作者的文章用有p标签，则可通过这个对这些文章中的p标签进行设置。前面
的".postBody"明确的指出了这里样式的作用范围。仅仅适用于文章主体部分。
建议这个不要设置过于详细的细节。因为，一些样式，一篇文章比较适合的话，
并不能保证所有的文章都适合。
**************************************************/
/*文章内部常用标签格式*/
.postBody {
    line-height: 1.5em;
}
.postBody p,.postCon  p{
    text-indent: 2em;
    margin: 0 auto 1em auto;
}
.postBody h2{
    font-size: 150%;
    margin: 15px auto 2px auto;
    font-weight:bold;
}
.postBody h3 {
    font-size: 120%;
    margin: 15px auto 2px auto;
    font-weight:bold;
}
.postBody h4{
    font-size:110%;
    margin:15px auto 2px auto;
    font-weight:bold;
    color:#333;
}

.postBody h5{
    font-size:100%;
    margin:15px auto 2px auto;
    font-weight:bold;
    color:#333;
}

.postBody a:link,.postBody a:visited,.postBody a:active{
    text-decoration:none;
}
.postCon a:link,.postCon a:visited,.postCon a:active{
    text-decoration:none;
}
.postBody ul,.postCon ul{
    margin-left:2em;    
}

.postBody li,.postCon li{
    list-style-type:disc;
    margin-bottom:1em;
}

.postBody blockquote{
    background:url('/images/comment.gif') no-repeat 25px 0px;
    padding:10px 60px 5px 60px;
    min-height:35px;
    _height:35px;
    line-height:1.6em;
    color:#333;
}
/*签名*/
#MySignature {
    padding: 1px 10px 80px 1px;
  
    mily: 幼圆;
    margin-top: 2px;
    height: 60px;
    background: #FFFFF0;
}
.MySignature_text {
    line-height: 20px;
    
}
/*****第四部分结束*******************************/
```

## 侧边栏

``` html
<!DOCTYPE html>
<html>

<body>

    <div>
        <p>公众号:</p>
    </div>
    <div class="head_img"><img width="160" height="160" alt="我的头像"
            src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_qrcode_for_gh_96a5ba9e83ea_258.jpg"
            class="img_avatar">
        <div>

            <p>QQ:896478104</p>
            <p>Mail:ants_double@yeah.net</p>
            <p>希望大家多多支持，觉得文章好可以点个赞，动动你的鼠标加下关注哦</p>
            <!-- Your XlchPlayerKey -->
            <script>XlchKey = "d9zz3e6DHX";</script>
            <!-- font-awesome 4.2.0 -->
            <link
                href="https://lib.baomitu.com/font-awesome/5.7.2/advanced-options/use-with-node-js/fontawesome-free/css/all.min.css"
                rel="stylesheet" type="text/css">

            <!-- JQuery 2.2.4 -->
            <script src="https://lib.baomitu.com/jquery/3.3.1/jquery.min.js"></script>
            <!-- JQuery-mousewheel 3.1.9 -->
            <script src="https://lib.baomitu.com/jquery-mousewheel/3.1.13/jquery.mousewheel.min.js"></script>
            <!-- Scrollbar -->
            <script src="https://static.https.badapple.top/BadApplePlayer/js/scrollbar.js"></script>
            <!-- BadApplePlayer -->
            <script src="https://static.https.badapple.top/BadApplePlayer/Player.js"></script>
</body>

</html>
```

## 首页html

``` html
<!DOCTYPE html>
<html>

<body>


    <style>
        #Canvas {
            position: fixed;
            top: 0px;
            left: 0px;
            opacity: 0.3;
        }
    </style>

    <canvas id="Canvas"></canvas>


    <style>
        #nav {
            width: 150px;
            height: 400px;
            border: 1px solid #D4CD49;
            position: fixed;
            left: 0;
            top: 30%
        }
    </style>
    <a class="git-link" href="https://github.com/Ants-double"></a>
    <input type="image" id="Uleft"
        src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132102016-280648354.png"
        onmouseover="this.style.top='10px'; this.src='https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132110485-340298713.png' "
        onmouseout="this.style.top='-60px'; this.src='https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132102016-280648354.png' "
        onclick="ShowPicture()">

    <input type="image" id="Uright"
        src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132057500-1294518696.png"
        onmouseover="this.style.top='10px'; this.src='https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132044282-1070510381.png' "
        onmouseout="this.style.top='-55px'; this.src='https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132057500-1294518696.png' "
        onclick="ChangePicture()" style="top: -55px;">

    <input type="image" id="Dright"
        src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132721735-572062833.png"
        onclick="ShowTab()">

    <input type="image" id="MagicArray"
        src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132726032-1459872254.png"
        onclick="ShowTab()">

    <a name="Tab" id="Tab1" href="https://www.cnblogs.com//" style="right:78px;bottom:165px;">博客园</a>
    <a name="Tab" id="Tab1" href="https://www.cnblogs.com/ants_double/" style="right:150px;bottom:130px;">首页</a>
    <a name="Tab" id="Tab1" href="https://msg.cnblogs.com/send/ants_double" style="right:10px;bottom:130px;">私信博主</a>
    <a name="Tab" id="Tab1" onclick="fixedIndexs.show()" style="right:120px;bottom:50px;">显示目录</a>
    <a name="Tab" id="Tab1" onclick="fixedIndexs.hide()" style="right:20px;bottom:50px;">隐藏目录</a>
    <a name="Tab" id="Tab1" href="https://i.cnblogs.com/" style="right:85px;bottom:10px;">管理</a>
    <a name="Tab" id="Tab1" style="right:85px;bottom:88px;" onclick="control()">动画</a>

    <script src="https://static.tctip.com/tctip-1.0.2.min.js"></script>
    <script>
        new tctip({
            top: '20%',
            button: {
                id: 9,
                type: 'zanzhu'
            },
            list: [
                {
                    type: 'alipay',
                    qrImg: 'https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_WeChat%20Image_20190306085659.png'
                }, {
                    type: 'wechat',
                    qrImg: 'https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_WeChat%20Image_20190306085653.png'
                }, {
                    type: 'tenpay',

                    qrImg: 'https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_qq_pic_merged_1551919230938.jpg'
                }
            ]
        }).init()
    </script>
    <script>
        window.requestAnimFrame =
            window.requestAnimationFrame ||
            window.webkitRequestAnimationFrame ||
            window.mozRequestAnimationFrame ||
            window.oRequestAnimationFrame ||
            window.msRequestAnimationFrame ||
            function (callback) { window.setTimeout(callback, 1000 / 10); };
        var W = document.body.scrollWidth, H = document.body.scrollHeight;
        var ca = document.getElementById("Canvas"), el = ca.getContext("2d");
        var num = 0, SpeedBasic = 3, SpeedRand = 0.8, angleBasic = 0.5, timer, lline = 20;
        var x = new Array(), y = new Array(), speed = new Array(), angle = new Array(), t = new Array(), TT = new Array();
        var img1 = new Image(), img2 = new Image(), img3 = new Image(), img4 = new Image();
        ca.width = W; ca.height = H;
        img1.src = "https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132729688-38554350.png";
        img2.src = "https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132733563-1765368712.png";
        img3.src = "https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132739141-33127178.png";
        img4.src = "https://www.cnblogs.com/images/cnblogs_com/ants_double/1411802/o_841250-20170914132745860-1067567351.png";

        function RandomNum(Min, Max) {
            var Range = Max - Min;
            var Rand = Math.random();
            return (Min + Math.round(Rand * Range));
        }
        function RandomReal(Min, Max) {
            return Min + (Max - Min) * Math.random();
        }
        function abs(W) { return W <= 0 ? -W : W; }
        function drawtail(px, py, an) {
            an = Math.atan(an);
            for (var i = 0; i < 10; i++) {
                var X, Y;
                Y = Math.sqrt(RandomReal(0, lline * lline));
                X = RandomReal(-Y * 5 / lline, Y * 5 / lline) + RandomReal(-Y * 5 / lline, Y * 5 / lline);
                Y = lline - Y;
                X += 10;
                el.fillRect(px + (X * Math.cos(an) - Y * Math.sin(an)), py - (X * Math.sin(an) + Y * Math.cos(an)), 2, 2);
            }
        }
        function drawstar(px, py, ti) {
            if (ti == 1) el.drawImage(img1, px, py, 20, 20); else
                if (ti == 2) el.drawImage(img2, px, py, 20, 20); else
                    if (ti == 3) el.drawImage(img3, px, py, 20, 20); else
                        if (ti == 4) el.drawImage(img4, px, py, 20, 20);
        }
        function drawline(sx, sy, px, py) {
            el.beginPath();
            el.moveTo(sx, sy);
            el.lineTo(px, py);
            el.stroke();
            el.closePath();
        }
        function dis(sx, sy, px, py) {
            return Math.sqrt((px - sx) * (px - sx) + (py - sy) * (py - sy));
        }
        function work(timestamp) {
            if (RandomNum(0, 5) == 0) {
                x.push(RandomNum(0, W));
                y.push(RandomNum(0, H));
                t.push(0);
                TT.push(RandomNum(3, 10));
                speed.push(SpeedBasic + RandomReal(-SpeedRand, SpeedRand) + RandomReal(-SpeedRand, SpeedRand) + RandomReal(-SpeedRand, SpeedRand));
                angle.push(RandomReal(-angleBasic, angleBasic) + RandomReal(-angleBasic, angleBasic) + RandomReal(-angleBasic, angleBasic));
                for (; ;) {
                    if (Math.random() <= 0.7) y[num] = 0; else {
                        y[num] %= 200;
                        if (Math.random() <= 0.5) x[num] = 0, angle[num] = abs(angle[num]); else x[num] = W - 1, angle[num] = -abs(angle[num]);
                    }
                    var i;
                    for (i = 0; i < num; i++) if (dis(x[i], y[i], x[num], y[num]) < 20) break;
                    if (i == num) break;
                    x[num] = RandomNum(0, W); y[num] = RandomNum(0, H);
                }
                num++;
            }
            el.clearRect(0, 0, W, H);
            el.fillStyle = "#7B68EE";
            var tmp;
            for (var i = 0; i < num; i++)
                for (var j = i + 1; j < num; j++)
                    if (dis(x[i], y[i], x[j], y[j]) < 20) {
                        tmp = speed[i];
                        speed[i] = speed[j];
                        speed[j] = tmp;

                        tmp = angle[i];
                        angle[i] = angle[j];
                        angle[j] = tmp;
                    }
            for (var i = 0; i < num; i++) {
                //el.fillRect(x[i],y[i],10,10);
                drawtail(x[i], y[i], angle[i]);
                drawstar(x[i], y[i], (parseInt(t[i] / TT[i]) % 4) + 1);
                y[i] += speed[i]; x[i] += (speed[i] * angle[i]);
                t[i]++;
                if (y[i] >= H || x[i] < 0 || x[i] >= W) {
                    num--;
                    x[i] = x[num]; y[i] = y[num]; speed[i] = speed[num]; angle[i] = angle[num]; t[i] = t[num]; TT[i] = TT[num];
                    x.pop(); y.pop(); speed.pop(); angle.pop(); t.pop(); TT.pop();
                    i--;
                }
            }
            timer = requestAnimationFrame(work);
        }
        timer = requestAnimationFrame(work);
        var sta = 1;
        function control() {
            if (sta == 1) {
                cancelAnimationFrame(timer);
                ca.style.opacity = "0";
                sta = 0;
            } else {
                timer = requestAnimationFrame(work);
                ca.style.opacity = "1";
                sta = 1;
            }
        }


        function ShowTab() {
            dx = document.getElementById("MagicArray");
            if (dx.style.width == "200px") {
                dx.style.width = "0px";
                dx.style.height = "0px";
                dx.style.bottom = "100px";
                dx.style.right = "100px";
                dx.style.transform = "rotate(0deg)";
            } else {
                dx.style.width = "200px";
                dx.style.height = "200px";
                dx.style.bottom = "0px";
                dx.style.right = "0px";
                dx.style.transform = "rotate(180deg)";
            }

            dy = document.getElementsByName("Tab");
            for (var i = 0; i < dy.length; i++) {
                dx = dy[i];
                if (dx.style.fontSize == "15px") {
                    dx.style.fontSize = "0px";
                    dx.style.transitionDelay = "0s";
                } else {
                    dx.style.fontSize = "15px";
                    dx.style.transitionDelay = "0.8s";
                }
            }
        }
        function ShowPicture() {
            dx = document.getElementById("main");
            if (dx.style.opacity == "0") dx.style.opacity = "0.9"; else dx.style.opacity = "0";
        }
        function ChangePicture() {
            dx = document.body;
            dy = RandomNum(0, 13);
            if (dy == 0) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_01.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 1) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_02.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 2) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_03.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 3) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_04.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 4) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_05.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 5) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_06.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 6) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_07.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 7) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_08.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 8) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_09.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 9) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_10.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 10) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_11.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 11) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_12.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 12) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_13.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            } else if (dy == 13) {
                dx.style.background = "url(https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_14.jpg) no-repeat fixed";
                dx.style.backgroundSize = "cover";
            }
        }
        ChangePicture();
    </script>

    <script type="text/javascript">
        /* 鼠标特效 */
        var a_idx = 0;
        jQuery(document).ready(function ($) {
            $("body").click(function (e) {
                var a = new Array("❤关关雎鸠❤", "❤在河之洲❤", "❤窈窕淑女❤", "❤君子好逑❤", "❤参差荇菜❤", "❤左右流之❤", "❤窈窕淑女❤", "❤寤寐求之❤", "❤求之不得❤", "❤寤寐思服❤", "❤悠哉悠哉❤", "❤辗转反侧❤", "❤参差荇菜❤", "❤左右采之❤", "❤窈窕淑女❤", "❤琴瑟友之❤", "❤参差荇菜❤", "❤左右芼之❤", "❤窈窕淑女❤", "❤钟鼓乐之❤");
                var $i = $("<span></span>").text(a[a_idx]);
                a_idx = (a_idx + 1) % a.length;
                var x = e.pageX,
                    y = e.pageY;
                $i.css({
                    "z-index": 999999999999999999999999999999999999999999999999999999999999999999999,
                    "top": y - 20,
                    "left": x,
                    "position": "absolute",
                    "font-weight": "bold",
                    "color": "rgb(" + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + ")"
                });
                $("body").append($i);
                $i.animate({
                    "top": y - 180,
                    "opacity": 0
                },
                    1500,
                    function () {
                        $i.remove();
                    });
            });
        });
    </script>
</body>

</html>
```

## 页脚

``` html
<!--PageEndHtml Block Begin-->
<script type="text/javascript">
    var setMyBlog = {
        setCopyright: function () {
            //设置版权信息，转载出处自动根据页面url生成
            var info_str = '<p>作者：<a target="_blank">@ants_double</a><br>' +
                '本文为作者原创，转载请注明出处：<a class="uri"></a></p><hr></hr>',
                info = $(info_str),
                info_a = info.find("a"),
                url = window.location.href;
            $(info_a[0]).attr("href", "https://www.cnblogs.com/ants_double/");
            $(info_a[1]).attr("href", url).text(url);
            $("#cnblogs_post_body").prepend(info);
        },
        setAtarget: function () {
            // 博客内的链接在新窗口打开
            $("#cnblogs_post_body a").each(function () {
                this.target = "_blank";
            })
        },
        setContent: function () {
            //博客园内自动生成目录

            var jquery_h1_list = $('#cnblogs_post_body h1');
            if (jquery_h1_list.length == 0) { return; }
            if ($('#cnblogs_post_body').length == 0) { return; }

            var content = '<a name="_labelTop"></a>';
            content += '<div id="navCategory">';
            content += '<p style="font-size:18px"><b>阅读目录(Content)</b></p>';
            // 一级目录 start
            content += '<ul class="first_class_ul">';

            for (var i = 0; i < jquery_h1_list.length; i++) {
                var go_to_top = '<div style="text-align: right"><a href="#_labelTop">回到顶部(go to top)</a><a name="_label' + i + '"></a></div>';
                $(jquery_h1_list[i]).before(go_to_top);

                // 一级目录的一条
                var li_content = '<li><a href="#_label' + i + '">' + $(jquery_h1_list[i]).text() + '</a></li>';

                var nextH1Index = i + 1;
                if (nextH1Index == jquery_h1_list.length) { nextH1Index = 0; }
                var jquery_h2_list = $(jquery_h1_list[i]).nextUntil(jquery_h1_list[nextH1Index], "h2");
                // 二级目录 start
                if (jquery_h2_list.length > 0) {
                    //li_content +='<ul style="list-style-type:none; text-align: left; margin:2px 2px;">';
                    li_content += '<ul class="second_class_ul">';
                }
                for (var j = 0; j < jquery_h2_list.length; j++) {
                    var go_to_top2 = '<div style="text-align: right"><a name="_lab2_' + i + '_' + j + '"></a></div>';
                    $(jquery_h2_list[j]).before(go_to_top2);
                    // 二级目录的一条
                    li_content += '<li><a href="#_lab2_' + i + '_' + j + '">' + $(jquery_h2_list[j]).text() + '</a></li>';

                    var nextH2Index = j + 1;
                    var next;
                    if (nextH2Index == jquery_h2_list.length) {
                        if (i + 1 == jquery_h1_list.length) {
                            next = jquery_h1_list[0];
                        }
                        else {
                            next = jquery_h1_list[i + 1];
                        }
                    }
                    else {
                        next = jquery_h2_list[nextH2Index];
                    }
                    var jquery_h3_list = $(jquery_h2_list[j]).nextUntil(next, "h3");
                    // 三级目录 start
                    if (jquery_h3_list.length > 0) {
                        li_content += '<ul class="third_class_ul">';
                    }

                    for (var k = 0; k < jquery_h3_list.length; k++) {
                        var go_to_third_Content = '<div style="text-align: right"><a name="_label3_' + i + '_' + j + '_' + k + '"></a></div>';
                        $(jquery_h3_list[k]).before(go_to_third_Content);
                        // 三级目录的一条
                        li_content += '<li><a href="#_label3_' + i + '_' + j + '_' + k + '">' + $(jquery_h3_list[k]).text() + '</a></li>';
                    }

                    if (jquery_h3_list.length > 0) {
                        li_content += '</ul>';
                    }
                    li_content += '</li>';
                    // 三级目录 end
                }
                if (jquery_h2_list.length > 0) {
                    li_content += '</ul>';
                }
                li_content += '</li>';
                // 二级目录 end

                content += li_content;
            }
            // 一级目录 end
            content += '</ul>';
            content += '</div>';

            $($('#cnblogs_post_body')[0]).prepend(content);
        },
        runAll: function () {
            /* 运行所有方法
             * setAtarget() 博客园内标签新窗口打开
             * setContent() 设置目录
             * setCopyright() 设置版权信息
             * setCodeRow() 代码行号显示
             */
            this.setAtarget();
            this.setContent();
            this.setCopyright();
        }
    }
    setMyBlog.runAll();
</script>

<script src="https://cdn.bootcss.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
<link href="https://files.cnblogs.com/files/ants_double/my1505.css" rel="stylesheet">
<script type="text/javascript" src="https://files.cnblogs.com/files/ants_double/my1505.js"></script>
<!-- <script type="text/javascript">
    $(function () {

        //加载图片
        var posttitle = "";
        if ($(".entrylistPosttitle").length != 0)
            posttitle = "entrylistPosttitle";
        if ($(".postTitle").length != 0)
            posttitle = "postTitle";
        $(".c_b_p_desc").each(function (i) {
            var ispictures = $("." + posttitle + " a:eq(" + i + ")").html();
            var hrefStr = $("." + posttitle + " a:eq(" + i + ")").attr("href");
            if (ispictures.substring(ispictures.length - 1) == ".") {
                var str = hrefStr.substring(hrefStr.lastIndexOf("/") + 1, hrefStr.lastIndexOf("."));
                var imgurl = "https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_" + str + ".png";
                $(".c_b_p_desc:eq(" + i + ")").before('<div class="main_img desc_img"><img class="lazy" style="width:240px;height:160px;margin-right: 20px;" src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_t.gif" data-original="' + imgurl + '"><div class="show"><span class="imgArea"><a title="阅读全文" href="' + hrefStr + '"></a></span></div></div>');
            } else {
                $(".c_b_p_desc:eq(" + i + ")").before('<div class="main_img desc_img"><img class="lazy" style="width:240px;height:160px;margin-right: 20px;" src="https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_t.gif" data-original="https://www.cnblogs.com/images/cnblogs_com/ants_double/1503498/o_666.png"><div class="show"><span class="imgArea"><a title="阅读全文" href="' + hrefStr + '"></a></span></div></div>');
            }
            $("img.lazy").lazyload();
        });
    });
</script> -->
<!--PageEndHtml Block End-->
```

