# 将flask应用部署到heroku

## 准备工作
1. 注册heroku
2. 在GitHub上创建一个repo
3. 在heroku里创建一个Python app，并且关联到GitHub

## 三个文件
 - main.py
 - requirements.txt
 - Procfile

main.py
```python
from flask import Flask

app = Flask(__name__)
 
@app.route('/')
def index():
    return 'Hello World!'
 
if __name__ == '__main__':
    app.run()
```

requirements.txt
```
Flask
gunicorn
```

Procfile
```bash
web: gunicorn main:app
```

## 提交

把这三个文件push到刚才创建的repo。
```bash
git init
git remote add origin [repo]
git add *
git commit -m [msg]
git push origin master
```

## 设置

进heroku后台

在"Manual deploy"这里选择repo的分支，手动deploy一次。

后面将"Automatic deploys"设为"enable"就可以在每次push的时候自动deploy了。

找到"Free Dynos"这个开关，滑动到右边，设为"free"。

到这就设置完成了，点击"open app"查看，可以看到打开了一个新网页，上面显示着"Hello World!"

