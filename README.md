# Chrome 绕过豆瓣强制验证跳转

## 绕过这个页面！
![](https://i.imgur.com/kK077Ps.png)

- 只能在电脑上操作
- 测试用的chrome版本: 105
- 需要chrome版本在65以上（因为用到DevTools的local overrides功能)
- 其他chromium-based浏览器应该也可以做类似操作

## 一般流程
1. 右键点击按钮/对话框等, 选择inspect
2. 在Elements panel的Event Listeners子panel里找到按钮触发的脚本
4. 在相关脚本/文件（主要涉及abnormal_account.js, douban.js，comment.js, index等，只要能搜出abnormal的文件应该都需要改造）里, 把window._USER_ABNORMAL替换为0; 删除跳转相关语句
5. 在sources->overrides里勾选enable local overrides, 然后选择本地保存地址
6. 保存替换修改后的文件 （快捷键control+S或者cmd+S, 保存后文件名上会有紫色小点点）
7. 控制台模式下刷新后即可进行发帖, 标记等操作

## 状态
### <a name="发状态"></a>发状态
1.在首页“说句话”“分享生活点滴...”文本输入框处点右键，选择inspect
2.在Event Listeners中选中脚本abnormal_account.js点进去
![](https://i.imgur.com/kqIJOnk.png)
3.将window._USER_ABNORMAL全部替换为0(快捷键control+F或者cmd+F), 保存
![](https://i.imgur.com/AzJliVQ.png)
4.再次inspect文本输入框
![](https://i.imgur.com/jwCovUJ.png)
5.删除掉涉及跳转的语句（上一步截图中的index文件，图中选中部分）
![](https://i.imgur.com/TbyzdQ3.png)
6.把index中所有cls_abnormal替换为空格
7.保存刷新后控制台打开时即可发状态

### 评论状态
1.inspect"添加回应"评论框
2.(假如你还没有修改这个文件)找到abnormal_account.js,参考[发状态](#发状态)中的修改方法进行修改
3.找到comment.js，把所有window._USER_ABNORMAL替换为0，保存刷新即可
![](https://i.imgur.com/vekWQnG.png)
![](https://i.imgur.com/jm2B3CG.png)


## 标记

### 标记音乐
以https://music.douban.com/subject/2133435/ 为例子
首先标记想听/在听/听过：

想听
https://music.douban.com/subject/2133435/?interest=wish&ck=irpD 
在听
https://music.douban.com/subject/2133435/?interest=do&ck=irpD
听过
https://music.douban.com/subject/2133435/?interest=collect&ck=irpD

然后添加短评：
1.inspect 网页上的“修改”按钮
2.把douban.js里的window._USER_ABNORMAL全部替换为0, 保存修改后的本地js文件
![](https://i.imgur.com/PNGVjf2.png)
3.刷新网页后即可编辑短评
![](https://i.imgur.com/Ah7Nfnd.png)

### 标记电影
目前仍可以直接在电影搜索页面上讲行标记和添加短评 （只有电视剧有“在看”按钮）
https://movie.douban.com/subject_search?search_text=rostam
修改方法同音乐

### 标记书
目前仍可以直接在书的搜索页面上进行标记和添加短评
https://book.douban.com/subject_search?search_text=shahnameh
修改方法同音乐


## 豆列

### 添加条目到豆列/创建豆列
1. inspect 网页上的"添加到豆列"按钮
2. 修改index (有多种方法，其一是把window._USER_ABNORMAL全部替换为0), 保存
3. 此时即可收藏到已有豆列，或者创建豆列并收藏
![](https://i.imgur.com/qL21wUg.png)

### 关注豆列

以https://www.douban.com/doulist/12282126/ 为例子,
通过 https://www.douban.com/doulist/12282126/?collect=yes&ck=irpD 即可进行关注

### 取关豆列
1. inspect 变灰的"已关注"按钮
2. 修改index (有多种方法，其一是把window._USER_ABNORMAL全部替换为0), 保存
3. 刷新后再点击"已关注", 弹出"真的要取消关注"对话框，选是即可
4. 页面刷新后如果控制台还开着，则"已关注"仍显示为灰色，此时关闭控制台再刷新即可看到的确已经取关了


