---
layout: post
title: Can’t mass-assign protected attributes和Rails表单保护
categories: [Web]
tags: [Rails]
---

最近在学习Rails，教材是Agile Web Development 4th，书上的例子程序在运行到*Add to Cart*按钮这一小节时报错：

>ActiveModel::MassAssignmentSecurity::Error in LineItemsController#create	
>Can’t mass-assign protected attributes: product

Google了一下，成果如下：

	...
	product = Product.find(params[:product_id])
	...
	# 把
	@lint_item = @cart.line_items.build(:product => product)
	# 替换成
	@line_item = @cart.line_items.build
	@line_item.product = product
	...

通过以上修改就可以正确运行程序。具体原因是Rails不允许*mass-assignment*，即不允许通过链接直接往数据库插入数据。所以不能用build接受表单参数直接来new这个新对象。除非显式的用`attr_accessible :product,:cart`告诉Rails允许*mass-assignment*。

# 关于Rails表单数据保护

## 一、必要性
Web应用在表单提交时，有些字段是不允许用户提交的，如权限、激活状态等。但是恶意用户可以通过模拟表单提交这些属性。以防这种情况发生，我们控制器中就不能直接用new来接受params表单参数，把数据库直接暴露。所以我们在控制器里用到attr_protected、 attr_accessible这两个方法。
## 二、方法解释
1. attr_protected 指定某些字段不可以通过块赋值。即new不能接受params表单参数。

2. attr_accessible 与attr_protected相反，指定某些字段可以通过块赋值。即new只能接受指定的params字段。

