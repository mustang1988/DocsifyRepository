# logging模块配置示例

---

## Dirt 配置

### Dirt 配置示例

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
		'rootFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/root.log',
			'encoding': 'utf-8',
		},
		'allFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/all.log',
			'encoding': 'utf-8',
		},
		'rpcFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/rpc.log',
			'encoding': 'utf-8',
		},
		'codecFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/codec.log',
			'encoding': 'utf-8',
		},
		'previewFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/preview.log',
			'encoding': 'utf-8',
		},
		'extractFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/extract.log',
			'encoding': 'utf-8',
		},
		'callbackFile': {
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'formatter': 'extend',
			'class': 'logging.handlers.RotatingFileHandler',
			'filename': workPath() + '/logs/callback.log',
			'encoding': 'utf-8',
		},
	},
	'loggers': {
        # logger 分类
		'callback': {
			'handlers': ['callbackFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'codec': {
			'handlers': ['codecFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'extract': {
			'handlers': ['extractFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'preview': {
			'handlers': ['previewFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'root': {
			'handlers': ['rootFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'rpc': {
			'handlers': ['rpcFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
		'all': {
			'handlers': ['allFile', 'console'],
			'level': os.getenv('LOG_LEVEL') if os.getenv('LOG_LEVEL') is not None else 'INFO',
			'propagate': True,
		},
	}
}
```

### Dirt 配置获取Logger对象和使用示例

```python
# logger.py
import logging.config
logging.config.dictConfig(config)
logger = logging.getLogger('rpc')
logger.info('rpc', 'xxx')
```


## ini 文件配置

### ini 配置文件示例

```ini
# log.conf / log.ini
[loggers]
keys=root,rpc,codec,preview,extract,callback
[handlers]
keys=consoleHandler,rootFileHandler,rpcFileHandler,codecFileHandler,previewFileHandler,extractFileHandler,callbackHandler
[formatters]
keys=extend
[logger_root]
level=INFO
handlers=consoleHandler,rootFileHandler
qualname=root
propagate=0
[logger_rpc]
level=INFO
handlers=consoleHandler,rpcFileHandler
qualname=rpc
propagate=0
[logger_codec]
level=INFO
handlers=consoleHandler,codecFileHandler
qualname=codec
propagate=0
[logger_preview]
level=INFO
handlers=consoleHandler,previewFileHandler
qualname=preview
propagate=0
[logger_extract]
level=INFO
handlers=consoleHandler,extractFileHandler
qualname=extract
propagate=0
[logger_callback]
level=INFO
handlers=consoleHandler,callbackHandler
qualname=callback
propagate=0
[handler_consoleHandler]
class=StreamHandler
level=INFO
formatter=extend
args=(sys.stdout,)
[handler_rootFileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/root.log',)
[handler_rpcFileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/rpc.log',)
[handler_codecFileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/codec.log',)
[handler_previewFileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/preview.log',)
[handler_extractFileHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/extract.log',)
[handler_callbackHandler]
class=FileHandler
level=INFO
formatter=extend
args=('/data/www/service_video_transcode/logs/callback.log',)
[formatter_extend]
format=[%(asctime)s] [%(levelname)s] [%(name)s]: %(message)s
```

### ini 配置获取Logger对象和使用示例

```python
# logger.py
import logging.config
logging.config.fileConfig('/config/log.ini')
logger = logging.getLogger('rpc')
logger.info('rpc','xxx')
```