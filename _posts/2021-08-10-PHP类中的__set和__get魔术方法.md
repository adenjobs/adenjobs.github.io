---
layout: post
title:  "PHP类中的__set和__get魔术方法"
date:   2021-08-10 17:30:00 +0800
categories: php
tags:
    - php
    - 魔术方法
---

# PHP类中的__set和__get魔术方法

## 使用示例
假如我们有以下类(```Account.php```)：
```
<?php
class Account
{
	private $user = 1;
	private $pwd = 2;
}


$a = new Account();
echo $a->user .PHP_EOL;
?>
```
我们想直接调用并获取里面的属性值:
```
php Account.php
```
不出意外的话，额，会报错，因为```$user```和```$pwd```是私有属性，不能直接被获取，报错信息如下：
```
PHP Fatal error:  Uncaught Error: Cannot access private property Account::$user in Account.php
```
那么我们想要获取有没有办法呢？有的！那就是使用```__set()```和```__get()```两个魔术方法，我们修改```Account.php```代码如下：
```
<?php
class Account
{
	private $user = 1;
	private $pwd = 2;

	public function __set($name , $value)
	{
		echo "Setting $name to $value \r\n";
		$this->$name = $value;
	}

	public function __get($name)
	{
		if(!isset($this->$name)){
			$this->$name = "未设置此变量";
		}else{
			return $this->$name;
		}
	}
}

$a = new Account();
echo $a->user .PHP_EOL;

?>
```
然后再运行起来，就正常了
```
$ php Account.php 
1
```
## 增加程序的健壮性
> PHP手册里把以上两个方法归到重载，PHP的重载和JAVA的重载不同。PHP提供的"重载"指动态地"创建"类属性和方法。

在以上案例中，我们看到如果在类中定义了__set()和__get()这一对魔术方法，那么当给对象属性赋值或取值时，即使这个属性不存在，也不会报错，这就在一定程度上增强了程序的健壮性。