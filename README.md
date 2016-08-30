
### Create A Gird System By yourself

#### 背景
 有时候想用一个栅格系统，但又不想引入一个库，比如bootstrap。这时，真的不妨自己来写一个。

#### 栅格系统的主要元素
* container
* rows
* columns
* gutters(columns之间的间距)

##### Container
container栅格系统里的容器，目的在于设置栅格的整个宽度。一般都设置为100%，即占满整个屏幕宽度。但你一可以用max-width来限制其最大的宽度。

	.gird-container{
		width: 100%;
		max-width: 1200px；
	}

##### Row
row是栅格系统的每一行，主要用来包住columns，并与其他row分割开来。
	
	/*-- cleafix hack -- */ 
    .row:before, 
    .row:after {
        content:"";
        display: table ;
         clear:both;
    }

##### column
即每个row里面的每列，你可以给自己的网格系统规定列数，并且给column分配宽度。   
首先，为了让每列可以水平排列。最简单就是用float属性让他们水平排列：
	
	[class*='col-'] {
        float: left;
        min-height: 1px; 
    }

之后，为占据不同列数的类分配宽度。如果是分成6列，那么每列就是100/6=16.66%的宽度。基于此，得到下列的设置：

	.col-1{
        width: 16.66%; 
    }
    .col-2{
        width: 33.33%; 
    }
    .col-3{
        width: 50%; 
    }
    .col-4{
        width: 66.664%;
    }
    .col-5{
        width: 83.33%;
    }
    .col-6{
        width: 100%;
    }
你可以分成12列,how many U like is up to U.

##### Column Gutters
如果你不希望column之间贴在一起，可以给它们设置间距。不过要注意，避免设置了padding之后导致整个盒模型增大，你还要设置box-sizing。

 	 [class*='col-'] {
        float: left;
		background: #eee; //这里只是为了方便看到效果
        min-height: 20px; //这里只是为了方便看到效果
        width: 16.66%; 
        /*-- our gutter --*/
        padding: 12px;
	    box-sizing: border-box; 
    }

#### 实现响应式布局的栅格系统
通过上面几步一个最简单的栅格系统就完成了，但是通常栅格系统都能够实现响应式布局。实现方法也很简单，利用css的媒介查询就行啦。以下是一个例子，分别在大于768px和小于768px的情况设置了宽度。
	
	@media all and (min-width:768px) {
    .col-md-1 {
        width: 8.33%;
    }
    .col-md-2 {
        width: 16.66%;
    }
    .col-md-3 {
        width: 25%;
    }
    .col-md-4 {
        width: 33.33%;
    }
    .col-md-5 {
        width: 41.66%;
    }
    .col-md-6 {
        width: 50%;
    }
    .col-md-7 {
        width: 58.33%;
    }
    .col-md-8 {
        width: 66.66%;
    }
    .col-md-9 {
        width: 75%;
    }
    .col-md-10 {
        width: 83.33%;
    }
    .col-md-11 {
        width: 91.66%;
    }
    .col-md-12 {
        width: 100%;
    }
	}

	@media (max-width: 768px){
    .col-ms-1 {
        width: 8.33%;
    }
    .col-ms-2 {
        width: 16.66%;
    }
    .col-ms-3 {
        width: 25%;
    }
    .col-ms-4 {
        width: 33.33%;
    }
    .col-ms-5 {
        width: 41.66%;
    }
    .col-ms-6 {
        width: 50%;
    }
    .col-ms-7 {
        width: 58.33%;
    }
    .col-ms-8 {
        width: 66.66%;
    }
    .col-ms-9 {
        width: 75%;
    }
    .col-ms-10 {
        width: 83.33%;
    }
    .col-ms-11 {
        width: 91.66%;
    }
    .col-ms-12 {
        width: 100%;
    }

	}

#### 准备就绪，待君使用
以下例子不仅利用了栅格来分配宽度，还实现了在大于和小于768px的响应式布局。
	
	 <div class="gird-container">
        <div class="row">
            <div class="col-md-4 col-ms-6"></div>
            <div class="col-md-4 col-ms-6"></div>
            <div class="col-md-4 col-ms-12"></div>
        </div>
        <div class="row">
            <div class="col-md-3 col-ms-3"></div>
            <div class="col-md-6 col-ms-6"></div>
            <div class="col-md-3 col-ms-3"></div>
        </div>
        <div class="row">
            <div class="col-md-1 col-ms-2"></div>
            <div class="col-md-1 col-ms-2"></div>
            <div class="col-md-2 col-ms-8"></div>
            <div class="col-md-2 col-ms-3"></div>
            <div class="col-md-6 col-ms-3"></div>
        </div>
    </div>

#### 后话
以上的栅格系统并不是一个完备的栅格系统，仅仅作为学习之用，重点在于理解栅格系统的原理和基本实现。个人觉得bootstrap的栅格系统很值得借鉴，不妨去看看它关于栅格系统的源码，就知道上面的栅格系统还能进行怎么样的优化了~代码也附上了bootstrap的gird.css