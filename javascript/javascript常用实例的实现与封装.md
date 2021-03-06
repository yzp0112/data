### 手机类型判断

```javascript
var BrowserInfo = {
	userAgent:navigator.userAgent.toLowerCase()
	isAndroid:Boolean(navigator.userAgent.match(/android/ig)),
	isIphone:Boolean(navigator.userAgent.match(/iphone|ipod/ig),
	isIpad:Boolean(navigator.userAgent.match(/ipad/ig)),
	isWeixin:Boolean(navigator.userAgent.match(/MicroMessenger/ig)),
}
```
### 字符串操作

1. 去除字符串空格

	```javascript
	//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
	function trim(str,type){
	    switch (type){
	        case 1:return str.replace(/\s+/g,"");
	        case 2:return str.replace(/(^\s*)|(\s*$)/g, "");
	        case 3:return str.replace(/(^\s*)/g, "");
	        case 4:return str.replace(/(\s*$)/g, "");
	        default:return str;
	    }
	}
	```

2. 字母大小写切换

	```javascript
	/*type
	1:首字母大写   
	2：首页母小写
	3：大小写转换
	4：全部大写
	5：全部小写
	 * */
	//changeCase('asdasd',1)
	//Asdasd
	function changeCase(str,type)
	{
	    function ToggleCase(str) {
	        var itemText = ""
	        str.split("").forEach(
	            function (item) {
	                if (/^([a-z]+)/.test(item)) {
	                    itemText += item.toUpperCase();
	                }
	                else if (/^([A-Z]+)/.test(item)) {
	                    itemText += item.toLowerCase();
	                }
	                else{
	                    itemText += item;
	                }
	            });
	        return itemText;
	    }
	    switch (type) {
	        case 1:
	            return str.replace(/^(\w)(\w+)/, function (v, v1, v2) {
	                return v1.toUpperCase() + v2.toLowerCase();
	            });
	        case 2:
	            return str.replace(/^(\w)(\w+)/, function (v, v1, v2) {
	                return v1.toLowerCase() + v2.toUpperCase();
	            });
	        case 3:
	            return ToggleCase(str);
	        case 4:
	            return str.toUpperCase();
	        case 5:
	            return str.toLowerCase();
	        default:
	            return str;
	    }
	}
	```

3. 字符串循环复制

	```javascript
	//repeatStr(str->字符串, count->次数)
	//repeatStr('123',3)
	//"123123123"
	function repeatStr(str, count) {
	    var text = '';
	    for (var i = 0; i < count; i++) {
	        text += str;
	    }
	    return text;
	}
	```

4. 字符串替换

	```javascript
	//字符串替换(字符串,要替换的字符,替换成什么)
	function replaceAll(str,AFindText,ARepText){
	　　　raRegExp = new RegExp(AFindText,"g");
	　　　return str.replace(raRegExp,ARepText);
	}
	```

5. 替换 * 

	```javascript
	//replaceStr(字符串,字符格式, 替换方式,替换的字符（默认*）)
	function replaceStr(str, regArr, type,ARepText) {
	    var regtext = '', Reg = null,replaceText=ARepText||'*';
	    //replaceStr('18819322663',[3,5,3],0)
	    //188*****663
	    //repeatStr是在上面定义过的（字符串循环复制），大家注意哦
	    if (regArr.length === 3 && type === 0) {
	        regtext = '(\\w{' + regArr[0] + '})\\w{' + regArr[1] + '}(\\w{' + regArr[2] + '})'
	        Reg = new RegExp(regtext);
	        var replaceCount = repeatStr(replaceText, regArr[1]);
	        return str.replace(Reg, '$1' + replaceCount + '$2')
	    }
	    //replaceStr('asdasdasdaa',[3,5,3],1)
	    //***asdas***
	    else if (regArr.length === 3 && type === 1) {
	        regtext = '\\w{' + regArr[0] + '}(\\w{' + regArr[1] + '})\\w{' + regArr[2] + '}'
	        Reg = new RegExp(regtext);
	        var replaceCount1 = repeatSte(replaceText, regArr[0]);
	        var replaceCount2 = repeatSte(replaceText, regArr[2]);
	        return str.replace(Reg, replaceCount1 + '$1' + replaceCount2)
	    }
	    //replaceStr('1asd88465asdwqe3',[5],0)
	    //*****8465asdwqe3
	    else if (regArr.length === 1 && type == 0) {
	        regtext = '(^\\w{' + regArr[0] +  '})'
	        Reg = new RegExp(regtext);
	        var replaceCount = repeatSte(replaceText, regArr[0]);
	        return str.replace(Reg, replaceCount)
	    }
	    //replaceStr('1asd88465asdwqe3',[5],1,'+')
	    //"1asd88465as+++++"
	    else if (regArr.length === 1 && type == 1) {
	        regtext = '(\\w{' + regArr[0] +  '}$)'
	        Reg = new RegExp(regtext);
	        var replaceCount = repeatSte(replaceText, regArr[0]);
	        return str.replace(Reg, replaceCount)
	    }
	}
	```

6. 检测字符串

	```javascript
	//checkType('165226226326','phone')
	//false
	//大家可以根据需要扩展
	function checkType (str, type) {
	    switch (type) {
	        case 'email':
	            return /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/.test(str);
	        case 'phone':
	            return /^1[3|4|5|7|8][0-9]{9}$/.test(str);
	        case 'tel':
	            return /^(0\d{2,3}-\d{7,8})(-\d{1,4})?$/.test(str);
	        case 'number':
	            return /^[0-9]$/.test(str);
	        case 'english':
	            return /^[a-zA-Z]+$/.test(str);
	        case 'chinese':
	            return /^[\u4E00-\u9FA5]+$/.test(str);
	        case 'lower':
	            return /^[a-z]+$/.test(str);
	        case 'upper':
	            return /^[A-Z]+$/.test(str);
	        default :
	            return true;
	    }
	}
	```

7. 检测密码强度

	```javascript
	//checkPwd('12asdASAD')
	//3(强度等级为3)
	function checkPwd(str) {
	    var nowLv = 0;
	    if (str.length < 6) {
	        return nowLv
	    }
	    ;
	    if (/[0-9]/.test(str)) {
	        nowLv++
	    }
	    ;
	    if (/[a-z]/.test(str)) {
	        nowLv++
	    }
	    ;
	    if (/[A-Z]/.test(str)) {
	        nowLv++
	    }
	    ;
	    if (/[\.|-|_]/.test(str)) {
	        nowLv++
	    }
	    ;
	    return nowLv;
	}
	```

8. 随机码（toString详解）

	```javascript
	//count取值范围0-36
	//randomNumber(10)
	//"2584316588472575"
	//randomNumber(14)
	//"9b405070dd00122640c192caab84537"
	//Math.random().toString(36).substring(2);
	//"83vhdx10rmjkyb9"
	function randomNumber(count){
	   return Math.random().toString(count).substring(2);
	}
	```

9. 查找字符串

	```javascript
	function countStr (str,strSplit){
	    return str.split(strSplit).length-1
	}
	var strTest='sad44654blog5a1sd67as9dablog4s5d16zxc4sdweasjkblogwqepaskdkblogahseiuadbhjcibloguyeajzxkcabloguyiwezxc967'
	//countStr(strTest,'blog')找出'blog'的出现次数
	//6
	```

### 数组操作

1. 数组去重

	```javascript
	//ES6新增的Set数据结构，类似于数组，但是里面的元素都是唯一的 ，其构造函数可以接受一个数组作为参数
	//let arr=[1,2,1,2,6,3,5,69,66,7,2,1,4,3,6,8,9663,8]
	//let set = new Set(array);
	//{1,2,6,3,5,69,66,7,4,8,9663}
	//ES6中Array新增了一个静态方法from，可以把类似数组的对象转换为数组
	//Array.from(set)
	//[1,2,6,3,5,69,66,7,4,8,9663]
	function removeRepeatArray(arr){
	    return Array.from(new Set(arr))
	}
	```

2. 数组顺序打乱

	```javascript
	function upsetArr(arr){
	    return arr.sort(function(){ return Math.random() - 0.5});
	}
	```

3. 数组最大值最小值

	```javascript
	//这一块的封装，主要是针对数字类型的数组
	function maxArr(arr){
	    return Math.max.apply(null,arr);
	}
	function minArr(arr){
	    return Math.min.apply(null,arr);
	}
	```

4. 数组求和，平均值

	```javascript
	//这一块的封装，主要是针对数字类型的数组
	//求和
	function sumArr(arr){
	 var sumText=0;
	 for(var i=0,len=arr.length;i<len;i++){
	 sumText+=arr[i];
	 }
	 return sumText
	}
	//平均值,小数点可能会有很多位，这里不做处理，处理了使用就不灵活了！
	function covArr(arr){
	 var sumText=sumArr(arr);
	 var covText=sumText/length;
	 return covText
	}
	```

5. 从数组中随机获取元素

	```javascript
	//randomOne([1,2,3,6,8,5,4,2,6])
	//2
	//randomOne([1,2,3,6,8,5,4,2,6])
	//8
	//randomOne([1,2,3,6,8,5,4,2,6])
	//8
	//randomOne([1,2,3,6,8,5,4,2,6])
	//1
	function randomOne(arr) {
	    return arr[Math.floor(Math.random() * arr.length)];
	}
	```

6. 返回数组（字符串）一个元素出现的次数

	```javascript
	//getEleCount('asd56+asdasdwqe','a')
	//3
	//getEleCount([1,2,3,4,5,66,77,22,55,22],22)
	//2
	function getEleCount (obj, ele) {
	    var num = 0;
	    for (var i = 0, len = obj.length; i < len; i++) {
	        if (ele == obj[i]) {
	            num++;
	        }
	    }
	    return num;
	}
	```

7. 返回数组（字符串）出现最多的几次元素和出现次数

	```javascript
	//arr, rank->长度，默认为数组长度，ranktype，排序方式，默认降序
	function getCount(arr, rank，ranktype){ 
	    var obj = {}, k, arr1 = []
	    //记录每一元素出现的次数
	    for (var i = 0, len = arr.length; i < len; i++) {
	        k = arr[i];
	        if (obj[k]) {
	            obj[k]++;
	        }
	        else {
	            obj[k] = 1;
	        }
	    }
	    //保存结果{el-'元素'，count-出现次数}
	    for (var o in obj) {
	        arr1.push({el: o, count: obj[o]});
	    }
	    //排序（降序）
	    arr1.sort(function (n1, n2) {
	        return n2.count - n1.count
	    });
	    //如果ranktype为1，则为升序，反转数组
	    if(ranktype===1){
	        arr1=arr1.reverse();
	    }
	    var rank1 = rank || arr1.length;
	    return arr1.slice(0,rank1);
	}
	/*
	 * getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2])默认情况，返回所有元素出现的次数
	 * getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3)传参（rank=3），只返回出现次数排序前三的
	 * getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],null,1)传参（ranktype=1,rank=null），升序返回所有元素出现次数
	 * getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3,1)传参（rank=3，ranktype=1），只返回出现次数排序（升序）前三的
	*/
	```

8. 得到n1-n2下标的数组

	```javascript
	//getArrayNum([0,1,2,3,4,5,6,7,8,9],5,9)
	//[5, 6, 7, 8, 9]
	 
	//getArrayNum([0,1,2,3,4,5,6,7,8,9],2) 不传第二个参数,默认返回从n1到数组结束的元素
	//[2, 3, 4, 5, 6, 7, 8, 9]
	function getArrayNum(arr,n1,n2){
	    var arr1=[],len=n2||arr.length-1;
	    for(var i=n1;i<=len;i++){
	        arr1.push(arr[i])
	    }
	    return arr1;
	}
	```

9. 筛选数组

	```javascript
	/删除值为'val'的数组元素
	//removeArrayForValue(['test','test1','test2','test','aaa'],'test','%')
	//["aaa"]   带有'test'的都删除
	     
	//removeArrayForValue(['test','test1','test2','test','aaa'],'test')
	//["test1", "test2", "aaa"]  //数组元素的值全等于'test'才被删除
	function removeArrayForValue(arr,val,type){
	    arr.filter(function(item){return type==='%'?item.indexOf(val)!==-1:item!==val})
	}
	```

### 基础DOM操作

```javascript
	//设置对象内容
	jquery：$('#xxx').html('hello world');
	现在：html(document.getElementById('xxx'),'hello world')
	//获取对象内容
	jquery：$('#xxx').html();
	现在：html(document.getElementById('xxx'))
```

1. 检测对象是否有哪个类名

	```javascript
	function hasClass(obj,classStr){ 
	    var arr=obj.className.split(/\s+/); //这个正则表达式是因为class可以有多个,判断是否包含 
	    return (arr.indexOf(classStr)==-1)?false:true;
	}
	 var str = document.getElementById("xxx");
	 hasClass(str,className)
	```

2. 添加类名

	```javascript
	function addClass(obj,classStr){
	    if (!this.hasClass(obj,classStr)){obj.className += " " + classStr};
	},
	```

3. 删除类名

	```javascript
	function removeClass(obj,classStr){
	    if (this.hasClass(obj,classStr)) {
	        var reg = new RegExp('(\\s|^)' + classStr + '(\\s|$)');
	        obj.className = obj.className.replace(reg, '');
	    }
	},
	```

4. 替换类名("被替换的类名","替换的类名")

	```javascript
	function replaceClass(obj,newName,oldName) {
	    removeClass(obj,oldName);
	    addClass(obj,newName);
	}
	```

5. 获取兄弟节点

	```javascript
	function siblings(obj){
	    var a=[];//定义一个数组，用来存o的兄弟元素 
	    var p=obj.previousSibling; 
	    while(p){//先取o的哥哥们 判断有没有上一个哥哥元素，如果有则往下执行 p表示previousSibling 
	        if(p.nodeType===1){ 
	        a.push(p); 
	        } 
	        p=p.previousSibling//最后把上一个节点赋给p 
	    } 
	    a.reverse()//把顺序反转一下 这样元素的顺序就是按先后的了 
	    var n=obj.nextSibling;//再取o的弟弟 
	    while(n){//判断有没有下一个弟弟结点 n是nextSibling的意思 
	        if(n.nodeType===1){ 
	            a.push(n); 
	        } 
	        n=n.nextSibling; 
	    }
	    return a;
	},
	```

6. 设置样式

	```javascript
	function css(obj,json){
	    for(var attr in json){
	        obj.style[attr]=json[attr];
	    }
	}
	```

7. 设置文本内容

	```javascript
	function html(obj){
	    if(arguments.length==0){
	        return this.innerHTML;
	    }
	    else if(arguments.length==1){
	        this.innerHTML=arguments[0];
	    }
	}
	```

8. 显示隐藏

	```javascript
	function show(obj){
	    obj.style.display="";
	}
	function hide(obj){
	    obj.style.display="none";
	}
	```

### 其他操作

1. cookie

	```javascript
	//cookie
	//设置cookie
	function setCookie(name,value,iDay){
	 var oDate=new Date();
	 oDate.setDate(oDate.getDate()+iDay);
	 document.cookie=name+'='+value+';expires='+oDate;
	}
	//获取cookie
	function getCookie(name){
	 var arr=document.cookie.split('; ');
	 for(var i=0;i<arr.length;i++){
	 var arr2=arr[i].split('=');
	 if(arr2[0]==name)
	 {
	 return arr2[1];
	 }
	 }
	 return '';
	}
	//删除cookie
	function removeCookie(name){
	 setCookie(name,1,-1);
	}
	```

2. 清除对象中值为空的属性

	```javascript
	//filterParams({a:"",b:null,c:"010",d:123})
	//Object {c: "010", d: 123}
	function filterParams(obj){
	    let _newPar = {};
	    for (let key in obj) {
	        if ((obj[key] === 0 || obj[key]) && obj[key].toString().replace(/(^\s*)|(\s*$)/g, '') !== '') {
	            _newPar[key] = obj[key];
	        }
	    }
	    return _newPar;
	}
	```

3. 现金额大写转换函数

	```javascript
	//upDigit(168752632)
	//"人民币壹亿陆仟捌佰柒拾伍万贰仟陆佰叁拾贰元整"
	//upDigit(1682)
	//"人民币壹仟陆佰捌拾贰元整"
	//upDigit(-1693)
	//"欠人民币壹仟陆佰玖拾叁元整"
	function upDigit(n)   
	{  
	    var fraction = ['角', '分','厘'];  
	    var digit = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];  
	    var unit = [ ['元', '万', '亿'], ['', '拾', '佰', '仟']  ];  
	    var head = n < 0? '欠人民币': '人民币';  
	    n = Math.abs(n);  
	    var s = '';  
	    for (var i = 0; i < fraction.length; i++)   
	    {
	        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, ''); 
	    } 
	    s = s || '整';  
	    n = Math.floor(n);  
	    for (var i = 0; i < unit[0].length && n > 0; i++)   
	    {  
	        var p = '';  
	        for (var j = 0; j < unit[1].length && n > 0; j++)   
	        {  
	            p = digit[n % 10] + unit[1][j] + p; 
	            n = Math.floor(n / 10);
	        }
	        //s = p.replace(/(零.)*零$/, '').replace(/^$/, '零')+ unit[0][i] + s; 
	        s = p+ unit[0][i] + s;
	    }
	    return head + s.replace(/(零.)*零元/, '元').replace(/(零.)+/g, '零').replace(/^整$/, '零元整');
	}
	```

4. 获取，设置url参数

	```javascript
	//获取url参数
	//getUrlPrmt('segmentfault.com/write?draftId=122000011938')
	//Object{draftId: "122000011938"}
	function getUrlPrmt(url) {
	    url = url ? url : window.location.href;
	    let _pa = url.substring(url.indexOf('?') + 1), _arrS = _pa.split('&'), _rs = {};
	    for (let i = 0, _len = _arrS.length; i < _len; i++) {
	        let pos = _arrS[i].indexOf('=');
	        if (pos == -1) {
	            continue;
	        }
	        let name = _arrS[i].substring(0, pos), value = window.decodeURIComponent(_arrS[i].substring(pos + 1));
	        _rs[name] = value;
	    }
	    return _rs;
	}
	 //设置url参数
	//setUrlPrmt({'a':1,'b':2})
	//a=1&b=2
	function setUrlPrmt(obj) {
	    let _rs = [];
	    for (let p in obj) {
	        if (obj[p] != null && obj[p] != '') {
	            _rs.push(p + '=' + obj[p])
	        }
	    }
	    return _rs.join('&');
	}
	```

5. 随机返回一个范围的数字

	```javascript
	function randomNumber(n1,n2){
	    //randomNumber(5,10)
	    //返回5-10的随机整数，包括5，10
	    if(arguments.length===2){
	        return Math.round(n1+Math.random()*(n2-n1));
	    }
	    //randomNumber(10)
	    //返回0-10的随机整数，包括0，10
	    else if(arguments.length===1){
	        return Math.round(Math.random()*n1)
	    }
	    //randomNumber()
	    //返回0-255的随机整数，包括0，255
	    else{
	        return Math.round(Math.random()*255)
	    }  
	}
	```

6. 随机产生颜色

	```javascript
	function randomColor(){
	    //randomNumber是上面定义的函数
	    //写法1
	    return 'rgb(' + randomNumber(255) + ',' + randomNumber(255) + ',' + randomNumber(255) + ')';
	     
	    //写法2
	    return '#'+Math.random().toString(16).substring(2).substr(0,6);
	     
	    //写法3
	    var color='#';
	    for(var i=0;i<6;i++){
	        color+='0123456789abcdef'[randomNumber(15)];
	    }
	    return color;
	}
	//这种写法，偶尔会有问题。大家得注意哦
	//Math.floor(Math.random()*0xffffff).toString(16);
	```

7. Date日期时间部分

	```javascript
	//到某一个时间的倒计时
	//getEndTime('2017/7/22 16:0:0')
	//"剩余时间6天 2小时 28 分钟20 秒"
	function getEndTime(endTime){
	    var startDate=new Date();  //开始时间，当前时间
	    var endDate=new Date(endTime); //结束时间，需传入时间参数
	    var t=endDate.getTime()-startDate.getTime();  //时间差的毫秒数
	    var d=0,h=0,m=0,s=0;
	    if(t>=0){
	      d=Math.floor(t/1000/3600/24);
	      h=Math.floor(t/1000/60/60%24);
	      m=Math.floor(t/1000/60%60);
	      s=Math.floor(t/1000%60);
	    } 
	    return "剩余时间"+d+"天 "+h+"小时 "+m+" 分钟"+s+" 秒";
	}
	```

8. 封装

	```javascript
	//这样的话，封装了几个操作，就增加了几个全局函数，污染了全局变量，在开发中应该尽量避免全局变量。不说别的，如果一个项目，几个人开发，很有可能会造成命名的冲突。
	function setUrlPrmt(obj){..}
	function getUrlPrmt(url){..}
	function upsetArr(obj){..}
	//所以，建议的封装姿势是
	var myJS={
	    setUrlPrmt:function(obj){..},
	    getUrlPrmt:function(url){..},
	    upsetArr:function(arr){..},
	}
	这样就算别人也写这样的函数,也不会造成冲突。全局变量也只有一个，加上别人也不会很多！
	var otherJS={
	    setUrlPrmt:function(obj){..},
	    getUrlPrmt:function(url){..},
	    upsetArr:function(arr){..},
	}
	//最后，封装的效果是
	var myJS={
	    //去除字符串空格
	    trim:function(obj){..},
	    //字母大小写切换
	    changeCase:function(obj){..},
	    //字符串循环复制
	    repeatStr:function(str){..},
	    .....
	}
	//如果是es6的模块化开发，大家也可以
	let myJS={
	    //去除字符串空格
	    trim:function(obj){..},
	    //字母大小写切换
	    changeCase:function(obj){..},
	    //字符串循环复制
	    repeatStr:function(str){..},
	    .....
	}
	//暴露模块，里面的方式大家也可以用es6方式实现，代码至少会少一点！
	export {myJS}
	```

