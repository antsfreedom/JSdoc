1、getElementsByTagName("") 获取标签，得到的是类数组，并不是真正意义上的数组
2、getElementsByClassName("") 同上

3、getAttribute("属性"); 

获取属性，因为属性是存在于标签里，一般需要先获取标签，

document.getElementsByTagName("a")[0]

4、setAttribute（"属性"，要设置的内容)； 
element.setAttribute(attributename,attributevalue)
设置（改变）属性

这里的属性一般遇见的有src、href、title、target

5、childNodes  (nodeType)	获取子节点

6、offsetParent 

这是一种全局的，获取的是父节点， 写法为：子元素.offsetParent
parerntNode

写法为：子元素.parerntNode

7、nextSibling 获取兄弟节点，这个一般在IE下可执行
为了兼容谷歌，写法为：nextElementSibling

 var Oli = document.getElementsByTagName("li")

	for(var i=0;i<Oli.length;i++){
		Oli[i].onclick = function(){
			if(this.nextElementSibling){
				// 为了兼容谷歌
				alert(this.nextElementSibling.innerText)   
				  }else{
				  	alert(this.nextSibling.innerText)
				  }
				}
			}

8、createElement	创建节点/createTextNode	创建文本内容/createDocumentFragment 文档碎片


var oli = document.createElement("li"); 创建li标签

oli.innerText="this is new li" ;  给li标签添加文本内容

obox.appendChild(oli) 

9、removeChild 移除子节点

移除子节点肯定得有父节点，所以要先获取父节点，然后获取要删除的每个子节点，最后实现的就是在父节点里删除子节点，下面的例子中要删除的肯定是li,但是我们获取的是每个a,所以还要再获取a的父节点，用parentNode获取到li

var obox = document.getElementById("box");

	var oa = document.getElementsByTagName("a")
		for(var i=0;i<oa.length;i++){
			oa[i].onclick = function(){
				obox.removeChild(this.parentNode)
			}
		}

<ul id="box">
	<li>第一个<a href="javascript:"> delete</a></li>
	<li>第二个<a href="javascript:"> delete</a></li>
	<li>第三个<a href="javascript:"> delete</a></li>
	<li>第四个<a href="javascript:"> delete</a></li>
</ul>

