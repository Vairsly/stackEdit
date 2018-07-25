设计模式--singleton
----
## 条件

 1. 必须拥有一个构造方法，并且必须被标记为private;
 2. 拥有一个保存类的实例的静态成员属性（字段）；
 3. 拥有一个访问这个实例的公共的静态方法；
```
static private $_instance;
static public function getInstance(){
	if(!(self::$_instance instanceof self)){
		self::$_instance = new self();
		echo "创建了一个对象";
	}
	return self::$_instance;x
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTM4NTc2MjVdfQ==
-->