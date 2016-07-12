Android事件分发和消费
	简单讲 Android 事件分发和消费跟三个函数有光
	ontouchEvent
	ondispatchTouchEvent
	和onInterceptTouchevetnt
	viewGroup三个函数都有
	view中缺少onInterceptTouchEvent；
	
三个函数都有返回值
	默认情况下是返回的false 正常的执行顺序是 最外层的viewgroup 触发 ondispatchTouchEvent函数，然后 onInterceptTouchevetnt 然后是里层viewgroup的dispathTouchevent
	到onInterceptTouchevetnt 里层view的OndispathTouchevent 到OntouchEvent 到外层的OntouchEvent到最外层的onTouchEvent
	
三个函数的职责
	ondispatchTouchEvent 是用来分发的 
			当dispath返回true是 表示停止分发
			当返回false就表示继续分发 如果是viewgroup就交给onInterceptTouchevetnt如果是view就交给ontouchEvent
	onInterceptTouchevetnt 是负责拦截的 
			当返回true时，就交给ontouchevent 
			当返回false时,就交给下一个层级的dispathTouchevent处理
			
	ontouchEvent是用来负责消费
			当返回true 事件结束传递
			当返回false 事件继续传递给上一个层级的ontouchEvent
			
	
另外 当在view/viewgroup上绑定事件的时候 如果OnTouchListener是在ontouchevent之前的 如果 OnTouchListener中的ontouch事件返回false 则会触发 ontouchevent 而且事件不再传给上层
		click事件是在是在ontouch事件之后的
