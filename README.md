# Lookup Module For Yii2


[![Latest Stable Version](https://poser.pugx.org/zacksleo/yii2-lookup/version)](https://packagist.org/packages/zacksleo/yii2-lookup)
[![Total Downloads](https://poser.pugx.org/zacksleo/yii2-lookup/downloads)](https://packagist.org/packages/zacksleo/yii2-lookup)
[![Build Status](https://travis-ci.org/zacksleo/yii2-lookup.svg?branch=master)](https://travis-ci.org/zacksleo/yii2-lookup)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/zacksleo/yii2-lookup/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/zacksleo/yii2-lookup/?branch=master)
[![Code Climate](https://img.shields.io/codeclimate/github/zacksleo/yii2-lookup.svg)]()
[![Code Coverage](https://scrutinizer-ci.com/g/zacksleo/yii2-lookup/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/zacksleo/yii2-lookup/?branch=master)
[![StyleCI](https://styleci.io/repos/75172753/shield?branch=master)](https://styleci.io/repos/75172753)
## Migrate database


To add a lookup table to your database, following is the sql for lookup:

```

CREATE TABLE IF NOT EXISTS `lookup` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `type` varchar(100) DEFAULT NULL,
  `name` varchar(100) DEFAULT NULL,
  `code` int(11) DEFAULT '1',
  `comment` text,
  `active` tinyint(1) DEFAULT '1',
  `order` int(11) DEFAULT '1',
  `created_at` int(11) DEFAULT NULL,
  `updated_at` int(11) DEFAULT NULL,	  
  PRIMARY KEY (`id`),
  UNIQUE KEY `CK_Type_Name_Unique` (`type`,`name`)	  
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=1 ;

```

Or else you can use yii migration
	
```
	
yii migrate/up --migrationPath=@zacksleo/yii2/lookup/migrations

```


## Config the components 



To access the lookup functionality anywhere in you application (either frontend or backend) follow the following steps:
```
In your main.php under config folder add the following:
    'components' => [
        ---
        'lookup' => [
            'class' => 'zacksleo\yii2\lookup\models\Lookup',
        ],
        ---
    ]
```
## Customize the form


Following are the few usage of lookup functionality:

```

/*** dropdown list from lookup ***/

<?= $form->field($model, 'active')->dropDownList(
    Yii::$app->lookup->items('yes_no'),
    //['1'=>'Active', '2' => 'Pending'],
    ['prompt'=>'--- Select ---'] 
) ?>


/*** RadioButton List ***/

<?= $form->field($model, 'gender')->radioList(
    Yii::$app->lookup->items('male_female'), ['separator' => '']
) ?>


/*** CheckBoxes List ***/

<?= $form->field($model, 'language')->checkboxList(
        Yii::$app->lookup->items('language'), ['separator' => '']
    ) ?>


/*** Dropdown List from Lookup ***/

<?= $form->field($model, 'language')->dropDownList(
        Yii::$app->lookup->items('language'), ['prompt' => '--- Select ---']
    ) ?>
	    
```

Inspired By  [Ibrar Turi](http://blog.ituri.net/2015/10/yii2-lookup-module/)  @ibrarturi, Thanks for his work.
