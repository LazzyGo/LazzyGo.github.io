# Autojs销毁UI


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

