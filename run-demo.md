

# 切到专门的运行demo分支上
git checkout run-demo

# 在 Ubuntu 里创建 & 激活 Conda 环境
conda create -n bettafish python=3.10
conda activate bettafish

# 安装 Python 依赖 + 浏览器驱动
pip install -r requirements.txt
playwright install chromium

# 在 Ubuntu 里安装并配置 PostgreSQL 数据库(直接用本地的，不再用docker的)
sudo apt update
sudo apt install postgresql postgresql-contrib

## 启动服务（一般安装完会自动启动，这里保险再手动启一次）
sudo service postgresql start
## 进入psql
sudo -u postgres psql

## 依次执行
CREATE USER bettafish WITH PASSWORD 'bettafish';
CREATE DATABASE bettafish OWNER bettafish;
GRANT ALL PRIVILEGES ON DATABASE bettafish TO bettafish;
\q

## 这样在ubuntu中的psql配置
DB 名：bettafish

用户：bettafish

密码：bettafish

地址：127.0.0.1:5432


## 在项目里复制 .env 并配置
cp .env.example .env
nano .env

### 配置数据库
DB_HOST=127.0.0.1
DB_PORT=5432
DB_USER=bettafish
DB_PASSWORD=bettafish
DB_NAME=bettafish
DB_DIALECT=postgresql
DB_CHARSET=utf8mb4

### 配置api
REPORT_ENGINE_API_KEY=sk-75ba99c2f17b426bb67ec922e4e96658
REPORT_ENGINE_BASE_URL=https://api.deepseek.com/v1
REPORT_ENGINE_MODEL_NAME=deepseek-chat

# MindSpider Agent（推荐deepseek-chat，官方申请地址：https://platform.deepseek.com/）
MINDSPIDER_API_KEY=sk-75ba99c2f17b426bb67ec922e4e96658
MINDSPIDER_BASE_URL=https://api.deepseek.com/v1
MINDSPIDER_MODEL_NAME=deepseek-chat

# 论坛主持人（推荐qwen-plus，官方申请地址：https://www.aliyun.com/product/bailian）
FORUM_HOST_API_KEY=sk-75ba99c2f17b426bb67ec922e4e96658
FORUM_HOST_BASE_URL=https://api.deepseek.com/v1
FORUM_HOST_MODEL_NAME=deepseek-chat

# SQL Keyword Optimizer（推荐qwen-plus，官方申请地址：https://www.aliyun.com/product/bailian）
KEYWORD_OPTIMIZER_API_KEY=sk-75ba99c2f17b426bb67ec922e4e96658
KEYWORD_OPTIMIZER_BASE_URL=https://api.deepseek.com/v1
KEYWORD_OPTIMIZER_MODEL_NAME=deepseek-chat

# 修改好后，直接将app.py跑起来即可
python app.py
## 注意，终端输出Flask服务已启动，就证明项目正常启动了，到那时如果此时访问0.0.0.5000可能是显示没有数据的，需要访问http://localhost:5000