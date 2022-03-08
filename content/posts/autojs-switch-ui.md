---
title: "Auto.js切换UI布局"
date: 2022-03-08T04:27:46Z
tags: ["auto.js"]
categories: ["javascript","android"]
---

## 切换布局
```js
"ui";

界面1();

function 界面1(){
	ui.layout(
	    <vertical>
		<button id="ok" text="切换界面"/>
	    </vertical>
	);
	ui.ok.click(function(){
	    界面2();
	});
}

function 界面2(){
	ui.layout(
	    <vertical>
		<button id="ok" text="点一下回去"/>
	    </vertical>
	);
	ui.ok.click(function(){
	   界面1();
	});
}

```
