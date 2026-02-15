# DDoS攻击检测系统部署文档

**开发时间戳**：2026-02-14 12:00:00

## 项目概述

基于机器学习模型的DDoS攻击检测系统，包含后端（Flask）和前端（HTML/JavaScript）组件，支持实时攻击检测、数据可视化和模型训练。

## 系统要求

### 硬件要求
- CPU: 至少2核
- 内存: 至少4GB
- 存储空间: 至少10GB

### 软件要求
- Python 3.8+
- pip 20.0+
- 浏览器: Chrome、Firefox、Edge等现代浏览器

## 部署步骤

### 1. 克隆项目

```bash
# 克隆项目到本地
git clone <项目仓库地址>
cd <项目目录>
```

### 2. 安装依赖

```bash
# 安装Python依赖
pip install -r requirements.txt
```

### 3. 生成训练数据

```bash
# 生成DDoS攻击检测系统的训练数据集
python generate_train_data.py
```

### 4. 训练模型

```bash
# 训练机器学习模型
python test_model_training.py
```

### 5. 启动后端服务

```bash
# 启动Flask后端服务
python run.py
```

后端服务将在以下地址运行：
- http://127.0.0.1:5000
- http://<本地IP>:5000

### 6. 启动前端服务

在另一个终端中执行：

```bash
# 进入前端目录
cd frontend

# 启动HTTP服务器（端口8000）
python -m http.server 8000
```

前端服务将在以下地址运行：
- http://127.0.0.1:8000
- http://<本地IP>:8000

## 系统配置

### 1. 数据库配置

系统使用SQLite数据库，无需额外配置。数据库文件将自动创建在 `instance/database.db`。

### 2. 模型配置

训练好的模型将保存在 `app/models/` 目录下，包含以下文件：
- `xgboost_model.pkl` - XGBoost模型
- `svm_model.pkl` - SVM模型
- `random_forest_model.pkl` - 随机森林模型
- 对应的 `.metadata` 文件 - 包含模型准确率等元数据

### 3. 日志配置

预测日志将保存在 `app/datasets/prediction_logs.json` 文件中。

## 环境变量

系统支持以下环境变量：

| 环境变量 | 描述 | 默认值 |
|---------|------|--------|
| FLASK_APP | Flask应用入口 | app |
| FLASK_ENV | 运行环境 | development |
| SECRET_KEY | Flask密钥 | 自动生成 |
| DEBUG | 调试模式 | True |

## 常见问题

### 1. 跨域请求问题

如果遇到跨域请求问题，请确保后端CORS配置正确。系统已默认配置了CORS支持。

### 2. 模型训练失败

- 确保训练数据格式正确
- 确保依赖库版本兼容
- 检查内存是否足够

### 3. 前端页面无法加载

- 确保前端服务正在运行
- 确保后端服务正在运行
- 检查浏览器控制台是否有错误信息

### 4. 预测API响应缓慢

- 检查模型文件是否存在
- 检查服务器性能
- 考虑使用更轻量级的模型

## 停止服务

### 停止后端服务

在运行后端服务的终端中，按下 `Ctrl+C` 停止服务。

### 停止前端服务

在运行前端服务的终端中，按下 `Ctrl+C` 停止服务。

## 部署到生产环境

### 注意事项

1. **禁用调试模式**：在生产环境中，将 `DEBUG` 设置为 `False`
2. **使用WSGI服务器**：建议使用Gunicorn等WSGI服务器部署Flask应用
3. **配置HTTPS**：在生产环境中，建议配置HTTPS
4. **设置强密钥**：在生产环境中，设置强的 `SECRET_KEY`

### 生产环境部署示例

```bash
# 安装Gunicorn
pip install gunicorn

# 使用Gunicorn启动服务
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

## 监控与维护

### 日志监控

- 后端日志：查看运行后端服务的终端输出
- 前端日志：查看浏览器控制台
- 预测日志：查看 `app/datasets/prediction_logs.json` 文件

### 模型更新

当需要更新模型时，执行以下步骤：

1. 生成新的训练数据
2. 重新训练模型
3. 重启后端服务

### 系统备份

建议定期备份以下文件和目录：
- `app/models/` - 模型文件
- `app/datasets/` - 数据集和日志
- `instance/database.db` - 用户数据库

## 联系方式

如有部署问题，请联系系统管理员。

- **联系邮箱**：di@didilighttech.cn
- **联系微信**：17396163410

## 版权声明

© 2026 武汉市荻荻为光科技有限公司 版权所有 保留所有权利

本系统及相关文档受中华人民共和国著作权法保护，未经允许，严禁转卖、复制、修改或分发本系统的任何部分。

如需商业使用或其他授权，请联系我们获取正式授权。

联系邮箱：di@didilighttech.cn
联系微信：17396163410

