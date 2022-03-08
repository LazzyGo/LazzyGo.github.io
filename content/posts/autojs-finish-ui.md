---
title: "Autojs销毁UI"
date: 2022-03-08T10:03:22Z
tags: ["autojs"]
categories: ["javascript","android"]
---

## 设置两秒后销毁UI
```js
"ui";

$ui.layout(
	<vertical>
	<appbar>
	<toolbar title="kkk" />
	</appbar>
		<button text="j" />
	</vertical>
)

setTimeout(()=>{
ui.finish()}
,2000)
```
