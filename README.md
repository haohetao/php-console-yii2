# php-console-yii2
PhpConsole wrapper for Yii 2

Based on https://github.com/barbushin/php-console-yii
# 安装

### Composer

	{
		"require": {
			"php-console/php-console": "dev-master"
		}
	}

Or

	$ composer require haohetao/php-console-yii2 dev-master
# Configuration Example
    Into common/main.php
    'bootstrap' => ['phpconsole'],
    'components' => [
        'phpconsole' => [
            'class' => '\haohetao\PhpConsole\PhpConsole',
            'isEnabled' => true,
            'ipMasks'=>['192.168.*.*', '2001:0:5ef5:79fb:*:*:*:*']
        ],
    ]

# Usage

    public function actionIndex()
    {
        \PC::debug('ok');
        return $this->render('index');
    }
    或者自定义全局函数
    /**
     * 使用phpconsole打印调试信息
     * @param $var
     * @param null $tags
     */
    function d($var, $tags = null) {
        $phpConsole=Yii::$app->phpconsole;
        if(!$phpConsole->isEnabled)
        {
            return;
        }
        PhpConsole\Connector::getInstance()->getDebugDispatcher()->dispatchDebug($var, $tags, 1);
    }
    加载全局函数
    在项目根目录的composer.json中加入
        "autoload": {
            "files": [
                "common/components/GlobalFunctions.php"
            ]
        }
    然后
    composer install