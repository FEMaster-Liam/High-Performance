# High-Performance
It collects many high performance JavaScript.
=
1. JavaScript 会阻塞页面渲染,将<script>标签放在boby底部
2. ***减少<script>的数量***,通过合并script标签,使用打包工具或者专门的合并处理器来合并。
3. ***defer***, 在script标签中添加这个属性,如果浏览器支持,就可以延迟加载script标签,延迟加载就是在页面加载完之后,在加载JavaScript?
4. 动态加载JavaScript标签script:
	
	```
	var script = document.createElement("script");
	script.type = "text/javascript";
	script.src = "xxx.js";
	document.getElementsByTagName("head")[0].appendChild(script);
	```
	
	这种动态加载的一般放在head标签中
	这种动态加载的脚本加载完之后会自执行,如果该脚本中使用了其他加载未完成的脚本,就会报错
	在Chrome,Safari,Firefox等浏览器中:
	
	```
	script.onload = function() {
		// TO DO
	}
	```
	
IE中使用***readyState***:

	```
	function loadScript (url, callback) {
	  var script = document.createElement("script");
	  script.type = "text/javascript";
	  if (script.readyState) {//IE
      	script.onreadystatechange = function(){
        	if (script.readyState == "loaded" || script.readyState == "comlete"){//一定是这两种状态结束
          		script.onreadystatechange = null;
          		callback();
        	}
      	}
      } else {
      	script.onload = function() {
        	callback();
      	};
      }
    	script.src = url;
    	document.getElementsByTagName("head")[0].appendChild(script);
	}
	```
	
5.Firefox 和 Opera能保证脚本按顺序执行，但其他浏览器有些是按照从服务器返回的顺序下载和执行。
  loadScript("file1.js",function()) {
    loadScript("file2.js",function()) {
      //ToDo
    }
  }
  这样就会先file1.js 再file2.js,但是最好的都是将两个file按顺序合并在一起。
6. 使用***XMLHttpRequest***脚本注入

  ```
  var xhr = new XMLHttpRequest();
  var.open("get","file1.js",true);
  xhr.onreadystatechange = function() {
    if (xhr.readyStatus ==4 ) {
      if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
        var script = document.createElement("script");
        script.type = "text/javascript";
        script.text = xhr.responseText;
        document.body.appendChild(script);
      }
    }
  };
  xhr.send(null);
  ```
  
  优点：所有浏览器都可以支持这种方法，且不会加载完自执行。
  缺点：不可以跨域
7.如果某个跨作用域的值在函数中被引用一次以上，那么就把它存储到局部变量里。因为标识符深度越大，读写越慢。
8.with 和 try...catch 会产生一个新变量，并置于作用域链顶端，访问这个新变量的所有属性速度会很快，但于此同时，访问其他的作用域变量的速度都会变慢。
9.搜索原型链越深，速度越慢。
10. 对象成员嵌套越深，读取速度就会越慢。执行location.href比执行window.location.href要快。所以缓存成员变量可以提升执行速度。
                                               
                                              
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
