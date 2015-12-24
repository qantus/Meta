# Meta
Модуль Meta-информации для Mindy

## Применение шаблонов Meta

Controller:

Устанавливаем мета-шаблон в контроллере. 
Первый входящий параметр - code.
Вторым входящим параметром передаем объекты, которые будут доступны в шаблоне

```php
...

public function actionView($slug) 
{
  $model = $this->getOr404(new Product(), ['slug' => $slug]);
  $this->setMetaTemplate('UNIT', [
      'model' => $model
  ]);
}

...
```

Логика работы такова: 

1. Сначала ищется перекрытая мета-информация по url (Meta). Если найдена - используем ее, если нет - то идем дальше
2. Ищется шаблон. Найден - рендерим и используем его, если нет - идем дальше.
3. Используем мета-информацию контроллера.


## Применение мета-текстов

Используем мета-тексты по шаблону в шаблонах (html). 
Первый входящий параметр - code.
Вторым входящим параметром передаем объекты, которые будут доступны в шаблоне

```twig
{% set seo = meta_text('UNIT', ['model' => model]) %}
{% if seo %}
    {% include 'meta/meta_text.html' with [
        'title' => seo.renderTitle(),
        'text' => seo.renderText()
    ] %}
{% endif %}
```
