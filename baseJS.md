1、getElementsByTagName("") 获取标签，得到的是类数组，并不是真正意义上的数组
2、getElementsByClassName("") 同上

3、getAttribute("属性"); 

获取属性，因为属性是存在于标签里，一般需要先获取标签，

document.getElementsByTagName("a")[0]

4、setAttribute（"属性"，要设置的内容)； 
element.setAttribute(attributename,attributevalue)
设置（改变）属性

这里的属性一般遇见的有src、href、title、target

5、childNodes 获取的是所有子节点，其中也包括文本节点和元素节点。
奇怪的是它在IE6-8使用是不存在问题，但是在其他浏览器里会有问题，因此
我们会用【nodeType】来判断节点类型，举个例子

var oUl=document.getElementById("ul1");


for(var i=0;i<oUl.childNodes.length;i++){

	if(oUl.childNodes[i].nodeType ==1){
      	 oUl.childNodes[i].style.background="green"
		}
	}

<ul id="ul1">        
	<li>第一个元素节点</li>
	<li>第二个元素节点</li>
	<li>第三个元素节点</li>
</ul>

我们需要知道如果 nodeType ==3,它表示的是文本节点，而文本节点是无法加样式的；
如果nodeType ==1，则是元素节点，而我们也只要元素节点，所以在循环里加判断，就不会存在兼容问题。

当然，我们可以使用【children】,它仅仅获取的是元素节点，在高版本浏览器或IE浏览器下都可以使用，所以上述例子中直接把childNode改成children就可以了，也不需要给其加判断，所以建议直接用children。


6、firstChild	获取的是第一个子节点，这个如果直接使用也存在兼容问题，它适用于IE6--8，所以一般在高版本浏览器下使用的是：firstElementChild。同样的使用时，需要加个判断，还是举例：

var oUl=document.getElementById("ul1");

	if(oUl.firstElementChild){
    	// 适配高版本浏览器 
         oUl.firstElementChild.style.background="red"  
    	}else{
    	// IE6-8适用
			oUl.firstChild.style.background="red"
    }
同理肯定还有lastChild/lastElementChild,用法一样。

7、parerntNode  获取父节点

写法为：子元素.parerntNode

*offsetParent  它也可以获取父节点，它有一定的局限性，因为如果改变了定位的样式，那么获取到的父节点就会不一样，比如父节点去掉定位，那么子元素的父节点就会往上一级去找， 写法还是一样的：子元素.offsetParent。



8、nextSibling 获取兄弟节点，这个一般在IE下可执行
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

9、createElement	创建节点/createTextNode	创建文本内容/createDocumentFragment 文档碎片/insertBefore 在父级元素里的某个位置插入新创建的子元素


var oli = document.createElement("li"); 创建li标签

oli.innerText="this is new li" ;  给li标签添加文本内容

obox.appendChild(oli) 

10、removeChild 移除子节点

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



