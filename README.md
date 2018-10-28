# homework5
const canvas= document.getElementById("canvas");
const context =canvas.getContext("2d");
const rand = function(num) {
  return Math.floor(Math.random() * num) + 1;
};
const createBoxes=function(count,canvasWidth,canvasHeight){
	let arr=[];
	const colorArray=['red','yellow','green','pink','blue','orange'];
    for(let i=0;i<count;i++){
    	let obj={
    		width: 30,
    		height: 30,
    	    x: rand(canvasWidth-30),
    	    y: rand(canvasHeight-30),
    	    xDelta:2,
    	    yDelta:2,
    	    color:colorArray[rand(colorArray.length)-1],
    	    draw:function(){
    	    	context.fillStyle = this.color;
    	    	context.fillRect(this.x, this.y, this.width, this.height);
            },
    	    update: function(){
    	    	this.x+=this.xDelta;
    	    	this.y+=this.yDelta;
                if(this.x>=canvas.width-this.width ||
                    this.x<=0){
                 this.xDelta *= -1;  
                }
                if(this.y>=canvas.height-this.height ||
                    this.y<=0){
                 this.yDelta*= -1;
                }
                
    	    }
        };
        arr[i]=obj;
    }
return arr;
}

let moo = createBoxes(20, canvas.width, canvas.height);
const draw = function(){
	for(let i=0; i<moo.length; i++){
		moo[i].draw();
	}
}
const update = function(){
	for(let i=0; i<moo.length; i++){
		moo[i].update();
	}
}	
const animate = function() {
	requestAnimationFrame(animate);
	context.clearRect(0,0,canvas.width,canvas.height);
    draw();
    update();
}
animate();
