# logging模块配置示例

---

Python中的logging模块是一个在项目中使用频率很高的模块, 用于日志文件的输出与控制台展示.

logging模块是可以免配置直接使用的, 但默认提供的日志输出格式可能并不满足项目需要, 也无法根据项目的不同业务模块定制输出格式, 输出文件名等等

但logging模块提供了一系列扩展配置项, 用于自定义配置日志的输出. 常用的配置有两种, 一种为Dirt格式, 一种为ini配置, 前者是通过声明一个Python字典来定义的配置, 后者是通过配置文件来定义的配置.

## Dict 配置

顾名思义, 即在.py代码中通过声明一个dict来配置

### Dict 配置示例

```python
# config.py
config = {
	'version': 1,
	'disable_existing_loggers': True,
	'formatters': {
		'extend': {
        # 自定义格式 [时间][级别][名称]: 消息
			'format': '[%(asctime)s][%(levelname)s][%(name)s]: %(message)s'
		}
	},
	'handlers': {
        # 控制台输出
		'console': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.StreamHandler',
		},
        # 文件输出
		'文件输出1': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/文件输出1.log',
			'encoding': 'utf-8',
		},
		'文件输出2': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/文件输出2.log',
			'encoding': 'utf-8',
		},
		'文件输出3': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/文件输出.log',
			'encoding': 'utf-8',
		}
	},
	'loggers': {
        # logger 分类
		'分类1': {
			'handlers': ['文件输出1', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'分类2': {
			'handlers': ['文件输出2', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'分类3': {
			'handlers': ['文件输出3', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'分类4': {
			'handlers': ['previewFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		}
	}
}
```

### Dict配置获取Logger对象和使用示例

```python
# logger.py
import logging.config
# 加载dict配置
logging.config.dictConfig(config)
logger = logging.getLogger('分类1')
logger.info('xxx', 'yyy')
```

## ini文件配置

即通过在项目下指定的.ini配置文件来配置日志模块

### ini配置文件示例

```ini
# log.conf / log.ini
; 日志分类
[loggers]
keys=分类1,分类2,分类3
; 日志Handler定义
[handlers]
keys=consoleHandler,分类1Handler,分类2FileHandler,分类3FileHandler
[formatters]
keys=extend
; 日志分类定义
[logger_分类1]
level=INFO
handlers=consoleHandler,分类1FileHandler
qualname=root
propagate=0
[logger_分类2]
level=INFO
handlers=consoleHandler,分类2FileHandler
qualname=分类2
propagate=0
[logger_分类3]
level=INFO
handlers=consoleHandler,分类3FileHandler
qualname=分类3
propagate=0
; 日志Handler定义
[handler_consoleHandler]
class=StreamHandler
level=INFO
formatter=extend
args=(sys.stdout,)
[handler_分类1FileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/logs/分类1.log',)
[handler_分类2FileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/logs/分类2.log',)
[handler_分类3FileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/logs/分类3.log',)
; 日志输出格式定义
[formatter_extend]
format=[%(asctime)s] [%(levelname)s] [%(name)s]: %(message)s
```

### ini配置获取Logger对象和使用示例

```python
# logger.py
import logging.config
# 加载ini配置文件
logging.config.fileConfig('/config/log.ini')
logger = logging.getLogger('分类1')
logger.info('xxx','yyy')
```

## 参考

- [logging官方文档参考(PY2, 简体中文)](https://docs.python.org/zh-cn/2.7/library/logging.config.html?highlight=logging)
- [logging官方文档参考(PY3, 简体中文)](https://docs.python.org/zh-cn/3/library/logging.config.html?highlight=logging)
