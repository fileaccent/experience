js 中的eval函数,可以执行字符串中的js代码,对正则表达式的遍历使用比较有用

```javascript
$(function(){//检测数据格式是否正确
  tests=new Array("/^[0-9]{12}$/",
                  "/^[\u2E80-\u9FFF]{2,5}$/",
				  "/^1(3|4|5|7|8|9)[0-9]{9}$/",
				  "/^[a-z0-9_-]{6,18}$/",
				  "/^[\u2E80-\u9FFF]{2,}$/");
 information=new Array("学号","姓名","电话","密码","部   门");
 hint=new Array("学号必须为12位的数字",
                "姓名必须为2位到5位的汉字",
                "电话必须为12位电话号码",
                "密码必须为6位到18位的非特殊字符",
                "部门必须为两位以上的汉字"
                )
  $("input").blur(function(){
    $("#registerHint").text("");
		if($("input").attr("readonly")!="readonly"){
	    var j=$(this).attr("placeholder");
      var text=j[j.length-2]+j[j.length-1];
      if(($(this).val()==null||$(this).val()=="")){
          $("#registerHint").text(text+"不能为空!");
          detection=false;
      }
      else{
        for(var i=0;i<tests.length;i++){
          if(text==information[i]){  
             var reg=eval(tests[i]);console.log(i);
              //这里是重点
             if( reg.test($(this).val()) ){
               $("#registerHint").text("");
               detection=true;
               break;
             }
             else{
               $("#registerHint").text(text+"格式错误!"+hint[i]);
               detection=false;
               break;
             }
          }
        }
      }
      if(j=="请再次输入密码"){
        if($("#password").val()!=$("#passwordSure").val()){
          passwordSame=false;
          $("#registerHint").text("两次输入密码不一致");
        }
      }
    }
	});
});
```
2. 使用localstorage的方法:
获取值:
```javascript
  JSON.parse(localStorage.getItem("datas"))
```
设置值:
```javascript
  localStorage.setItem('val', JSON.stringify(val))
```
## 获取数据
* 当获取vuex中或父组件传值给子组件的数据时,需要在computed或watch中获取一下(尤其是需要实时更新的数据)
示例:

```javascript
 computed: {
    isFollowSing () {
      return this.$store.state.isFollowSing
    },
    userId () {
      return this.$store.state.user.id
    }
  }
watch: {
  '$store.state.user.name' (newVal) {
    this.user.name = this.$store.state.user.name
  }
}
```
然后才能在页面中直接使用

* 当页面需要展示请求的数据时,需要设置一个变量,当请求成功后,才显示整个页面,防止页面的卡顿.

## 获取上传图片的方法

```javascript
  getFile (event) { // 读取上传的图片信息,并且显示图片
    const files = event.target.files
    const fileReader = new FileReader() // 内置方法new FileReader()   读取文件
      fileReader.addEventListener('load', () => {
        if (this.callback.imgurl.length <= 2) { // 如果上传的图片数量超过三张则,阻止上传
          this.callback.imgurl.push(fileReader.result)
        } else {
          alert('最多上传三张照片')
        }
      })
      fileReader.readAsDataURL(files[0])
      this.image = files[0]
      // console.log(this.callback.imgurl)
  }
```

可以参考上述的方法,读取显示数据

* 使用js 的数组更新元素,vue才会重新渲染,不然会没有数据

* 当动态修改img的src属性时,需要用require包裹
```html
  <img :src="radioStatus ? start : stop"  @click="startAudio"/>
  start: require('../../../static/conch/stop.svg'),
  stop: require('../../../static/conch/radioStart.svg'),
```

