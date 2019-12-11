function getStyle(obj, attr){
	if(obj.currentStyle){
		return obj.currentStyle[attr];
	} else {
		return getComputedStyle(obj, null)[attr];
	}
}
function animate(obj,json,callback){
	clearInterval(obj.timer);
	obj.timer = setInterval(function(){
		var isStop = true;
		for(var attr in json){
			var now = 0;
			if(attr == 'opacity'){
				now = parseInt(getStyle(obj,attr)*100);
			}else{
				now = parseInt(getStyle(obj,attr));
			}
			var speed = (json[attr] - now) / 8;
			speed = speed>0?Math.ceil(speed):Math.floor(speed);
			var cur = now + speed;
			if(attr == 'opacity'){
				obj.style[attr] = cur / 100;
			}else{
				obj.style[attr] = cur + 'px';
			}
			if(json[attr] !== cur){
				isStop = false;
			}
		}
		if(isStop){
			clearInterval(obj.timer);
			callback&&callback();
		}
	}, 30)
}
window.onload = function(){
	var box = document.getElementById("box");
	var navList = document.getElementsByTagName("li");
	var slider = document.getElementById("slider");
	var left = document.getElementById("left");
	var right = document.getElementById("right");
	var w1 = document.getElementById("w1");
	var index = 1;
	var isMoving = false;
	// window.onload = function(){
	var intervalId = setInterval(function(){
		marginLeft = w1.style.marginLeft; 
		w1.style.marginLeft = (parseInt(marginLeft)-1)+"px";
		var pos = parseInt(w1.style.marginLeft);
		if(pos==-450){
			w1.style.marginLeft = '1000px';
		}
	},20)
	// }
	//轮播下一张的函数
	function next(){
		if(isMoving){
			return;
		}
		isMoving = true;
		index = index + 1;
		navChange();
		animate(slider,{left:-1200*index},function(){
			if(index===6){
				slider.style.left="-1200px";
				index = 1;
			}
			isMoving = false;
		});
	}
	//播放上一张图片
	function prev(){
		if(isMoving){
			return;
		}
		isMoving = true;
		index = index - 1;
		navChange();
		animate(slider,{left:-1200*index},function(){
			if(index===0){
				slider.style.left="-6000px";
				index = 5;
			}
			isMoving = false;
		});
	}
	//开定时器,轮播图片
	var timer = setInterval(next,3000);
	//鼠标划入清定时器
	box.onmouseover = function(){
		animate(left,{opacity:50})
		animate(right,{opacity:50})
		clearInterval(timer);
	}
	//鼠标划出开定时器
	box.onmouseout = function(){
		animate(left,{opacity:0})
		animate(right,{opacity:0})
		timer = setInterval(next,3000); 
	}
	//点击左箭头,调用prev函数
	left.onclick = prev;
	//点击右箭头,调用next函数
	right.onclick = next;
	//点击按钮
	for(var i=0;i<navList.length;i++){
		navList[i].idx = i;
		navList[i].onclick = function(){
			index = this.idx + 1;
			navChange();
			animate(slider,{left:-1200*index})
		}
	}
	//小按钮背景切换
	function navChange(){
		for(var i=0;i<navList.length;i++){
			navList[i].className = '';
		}
		if(index===6){
			navList[0].className = 'active';
		}else if(index===0){
			navList[4].className = 'active';
		}else{
			navList[index-1].className = 'active';
		}
		
	}
}
