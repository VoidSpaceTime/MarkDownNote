## 常用命令
```
docker compose down && docker compose up -d
```

## 坑
1. 是官网
	1. https://cloud.seafile.com/wiki/publish/seafile-manual/7Lj3/
2. 访问以及文件上传问题
	1. 如需自定义端口，请编辑配置文件caddy.yml
	2. 编辑配置文件.env：SEAFILE_SERVER_HOSTNAME需加端口号:
3. [把80端口改成其它端口之后要如何配置才能上传文件?](https://bbs.seafile.com/t/topic/21385)
	1. 修改.env文件中SEAFILE_SERVER_HOSTNAME，添加端口号
	2. 12 取消了在GUI 界面配置 URL和端口，你只能通过配置文件调整。官网版本的发布说明里有提到的  [访问](https://wiki.anas365.com/spaces/VirtualReal/pages/62259239/docker-seafile-12.06)
	3. 
## S3配置
```
### S3
INIT_S3_STORAGE_BACKEND_CONFIG=true
INIT_S3_COMMIT_BUCKET=seafile-commit
INIT_S3_FS_BUCKET=seafile-fs
INIT_S3_BLOCK_BUCKET=seafile-block
INIT_S3_KEY_ID=cloud
INIT_S3_SECRET_KEY=ji123486.*
INIT_S3_USE_V4_SIGNATURE=true
INIT_S3_AWS_REGION=us-east-1
INIT_S3_HOST=172.17.0.1:9000
INIT_S3_USE_HTTPS=false

### S3 mode
SS_S3_USE_V4_SIGNATURE=true
SS_S3_ACCESS_ID=cloud
SS_S3_ACCESS_SECRET=ji123486.*
SS_S3_ENDPOINT=172.17.0.1:9000
SS_S3_BUCKET=cloud
SS_S3_USE_HTTPS=true
SS_S3_PATH_STYLE_REQUEST=true
SS_S3_AWS_REGION=us-east-1
## SS_S3_SSE_C_KEY=<your SSE-C key>
```
记得 在配置文件中 增加pathstyle = true
```
[commit_object_backend]

name = s3
bucket =seafile-commit
key_id = cloud
key = ji123486.*
host = 172.17.0.1:9000
path_style_request = true

[fs_object_backend]

name = s3
bucket = seafile-fs
key_id = cloud
key = ji123486.*
host = 172.17.0.1:9000
path_style_request = true

[block_backend]

name = s3
bucket = seafile-block
key_id = cloud
key = ji123486.*
host = 172.17.0.1:9000
path_style_request = true

[memcached]
memcached_options = --SERVER=localhost --POOL-MIN=10 --POOL-MAX=100
```
