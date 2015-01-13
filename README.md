Yii 2 Comments Module
===============================
[![License](https://poser.pugx.org/rmrevin/yii2-comments/license.svg)](https://packagist.org/packages/rmrevin/yii2-comments)
[![Latest Stable Version](https://poser.pugx.org/rmrevin/yii2-comments/v/stable.svg)](https://packagist.org/packages/rmrevin/yii2-comments)
[![Latest Unstable Version](https://poser.pugx.org/rmrevin/yii2-comments/v/unstable.svg)](https://packagist.org/packages/rmrevin/yii2-comments)
[![Total Downloads](https://poser.pugx.org/rmrevin/yii2-comments/downloads.svg)](https://packagist.org/packages/rmrevin/yii2-comments)

Code Status
-----------
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/rmrevin/yii2-comments/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/rmrevin/yii2-comments/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/rmrevin/yii2-comments/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/rmrevin/yii2-comments/?branch=master)
[![Travis CI Build Status](https://travis-ci.org/rmrevin/yii2-comments.svg)](https://travis-ci.org/rmrevin/yii2-comments)
[![Dependency Status](https://www.versioneye.com/user/projects/54119b799e16229fe00000da/badge.svg)](https://www.versioneye.com/user/projects/54119b799e16229fe00000da)

Installation
------------
Add in `composer.json`:
```
{
    "require": {
        "rmrevin/yii2-comments": "1.0.1"
    }
}
```

In config `/protected/config/main.php`
```php
<?
return [
	// ...
	'modules' => [
		// ...
		'comments' => 'rmrevin\yii\module\Comments\Module',
	],
	// ...
];
```

In auth manager add rules:
```php
use \yii\rbac\Role;
use \rmrevin\yii\module\Comments\Permission;
use \rmrevin\yii\module\Comments\rbac\ItsMyComment;

$AuthManager = \Yii::$app->getAuthManager();
$ItsMyCommentRule = new ItsMyComment();

// Rules
$AuthManager->add($ItsMyCommentRule);

// Permissions
$AuthManager->add(new Role(['name' => Permission::CREATE]));
$AuthManager->add(new Role(['name' => Permission::UPDATE]));
$AuthManager->add(new Role(['name' => Permission::UPDATE_OWN, 'ruleName' => $ItsMyCommentRule->name]));
$AuthManager->add(new Role(['name' => Permission::DELETE]));
$AuthManager->add(new Role(['name' => Permission::DELETE_OWN, 'ruleName' => $ItsMyCommentRule->name]));
```

Usage
-----
In view
```php
<?
// ...

echo \rmrevin\yii\module\Comments\widgets\CommentListWidget::widget([
    'entity' => (string) 'photo-15', // type and id
]);

```