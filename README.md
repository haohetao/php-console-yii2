# php-console-yii2
PhpConsole wrapper for Yii 2

Based on https://github.com/barbushin/php-console-yii

# Configuration Example
Into common/main.php
    'bootstrap' => ['phpconsole'],
    'components' => [
        'phpconsole' => [
            'class' => '\haohetao\PhpConsole\PhpConsole',
            'isEnabled' => true
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
    在composer.json中加入
        "autoload": {
            "files": [
                "common/components/GlobalFunctions.php"
            ]
        }
    然后
    composer install