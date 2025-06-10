# seafile
## 全s3 存储 vim /opt/seafile-data/seafile/conf/seafile.conf 
- 注意点
- 路径 path_style_request = true
- host = 10.60.10.3:9000
```
[fileserver]
port = 8082

[database]
type = mysql
host = db
port = 3306
user = seafile
password = ji123486.*
db_name = seafile_db
connection_charset = utf8


[memcached]
memcached_options = --SERVER=memcached --POOL-MIN=10 --POOL-MAX=100

[commit_object_backend]
name = s3
bucket = seafile-commit
key_id = cloud
key = ji123486.*
use_v4_signature = true
aws_region = us-east-1
host = 10.60.10.3:9000
use_https = false
path_style_request = true

[fs_object_backend]
name = s3
bucket = seafile-fs
key_id = cloud
key = ji123486.*
use_v4_signature = true
aws_region = us-east-1
host = 10.60.10.3:9000
use_https = false
path_style_request = true

[block_backend]
name = s3
bucket = seafile-block
key_id = cloud
key = ji123486.*
use_v4_signature = true
aws_region = us-east-1
host = 10.60.10.3:9000
use_https = false
path_style_request = true
```


## 存储方式
### git存储方式
**1. `[commit_object_backend]` - 提交对象后端**

- 存储：版本历史、提交记录、目录结构信息
- 内容：每次文件修改的元数据、文件树结构、提交时间戳等
- 格式：Git-like的提交对象，包含SHA1哈希值

**2. `[fs_object_backend]` - 文件系统对象后端**

- 存储：目录结构、文件名、文件属性
- 内容：文件夹层次结构、文件权限、文件元数据
- 格式：文件系统结构的抽象表示

**3. `[block_backend]` - 块存储后端**

- 存储：实际的文件内容数据
- 内容：文件被分割成的数据块（通常每块8MB）
- 格式：经过加密和压缩的二进制数据块

### 混合存储

你可以将块存储改为文件系统存储，保留其他后端的S3配置：

```
[commit_object_backend]
name = s3
bucket = seafile-commit
key_id = cloud
key = ji123486.*
use_v4_signature = true
aws_region = us-east-1
host = 10.60.10.3
port = 9000
use_https = false

[fs_object_backend]
name = s3
bucket = seafile-fs
key_id = cloud
key = ji123486.*
use_v4_signature = true
aws_region = us-east-1
host = 10.60.10.3
port = 9000
use_https = false

# 使用文件系统存储实际文件内容
[block_backend]
name = fs
dir = /opt/seafile-data/blocks
```