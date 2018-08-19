# resume-template

> This is a resume template.Create a beautiful resume for people

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

##项目部署
**参考链接**
[nodejs服务器部署教程二，把vue项目部署到线上](https://segmentfault.com/a/1190000010205995)

#### 打包
```
#在本地使用以下命令，打包
npm run build 
#打包之后本地会出现dist文件夹。将dist文件夹以及package.json 文件上传到centos服务器上，此处随便什么位置，新建个文件夹就能放。
```

#### 启动项目

新建一个app.js文件，文件内容如下
```
//定义目录
const fs = require('fs');
const path = require('path');
const express = require('express');
const app = express();
//vue目录
app.use(express.static(path.resolve(__dirname, './dist')))

app.get('*', function(req, res) {
    const html = fs.readFileSync(path.resolve(__dirname, './dist/index.html'), 'utf-8')
    res.send(html)
})
//定义启动的端口号
app.listen(8082);
```

运行如下命令：
```
#安装依赖包,如果系统中没有安装node，npm命令会找不到
npm install
#启动vue项目（pm2命令也需要单独安装，安装之后再执行下面命令）
pm2 start app.js
```
执行上面操作之后，访问127.0.0.1:8082就可以了，根据自己设置的端口访问。如果想从外网访问，则需要知道自己的ip，ip:port的方式就可以从外网访问。

#### 使用Nginx代理，使用域名访问

**[如果Nginx安装不会请点击此处](https://www.cnblogs.com/alvin-niu/p/9502271.html)**

Nginx配置文件(/etc/nginx/nginx.conf)
```
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
    #以上配置均是默认值未曾修改，如果想搞懂上面的是什么意思，自己去慢慢学习吧
    #这个配置是负载均衡使用的
    #此处的app_nodejs是负载均衡的名字
	upstream app_nodejs {
	    #访问的实际地址是下面的，可以有多个，多个时就达到了负载均衡的作用，后面其实还有一个参数，但是此处写不写无区别。
		server 127.0.0.1:8082;
		keepalive 64;
	}
    	server {
    	#监听的是80端口，不建议换成其他端口，因为换成其他端口后，你访问时，域名也得加上加上端口，比如端口号改成8080，访问时则是：onloading.cn:8080
        listen	80	default;
        #访问的域名
		server_name onloading.cn; 
		#如果访问的是ip，则直接返回404，此处只允许通过域名访问
		if ($host ~ "\d+\.\d+\.\d+\.\d") {
    			return 404;
		}
		location / {
			proxy_set_header X-Real-IP $remote_addr;
        		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        		proxy_set_header Host $http_host;
        		proxy_set_header X-Nginx-Proxy true;
        		proxy_set_header Connection "";
        		#指定使用哪个负载均衡，其他location的值均属于默认值
			proxy_pass http://app_nodejs;
			proxy_redirect off;
		}

    	}
}

    
```

配置完之后，使用onloading.cn边可以访问你的项目了。

