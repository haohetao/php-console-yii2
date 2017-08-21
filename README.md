# php-console-yii2
PhpConsole wrapper for Yii 2

Based on https://github.com/barbushin/php-console-yii

# Configuration Example
Into common/main.php
    'components' => [
        'phpconsole' => [
            'class' => '\nilsburg\PhpConsole\PhpConsole',
            'isEvalEnabled' => true,
            'password' => 'some_password'
        ],
    ]

# Usage (Eval)

    public function beforeAction($action)
    {
        if ($action->id === 'index') {
            $this->enableCsrfValidation = false;
        }
        return parent::beforeAction($action);
    }

    public function actionIndex()
    {
        $console = \Yii::$app->phpconsole;
        unset($console);
        return $this->render('index');
    }
