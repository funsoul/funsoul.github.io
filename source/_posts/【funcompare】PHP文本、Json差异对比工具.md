---
title: 【funcompare】PHP文本/Json差异对比工具
date: 2018-02-28
tags: 
  - PHP 
  - composer
---

funcompare
==========
A tool compare text differences

# Installation

```bash
composer require "funsoul/funcompare: ~1.1"
```

# Usage

### compareText()
```php
use Funsoul\Funcompare\Funcompare;

$old = 'A tool compare text differences is funny';
$new = 'A tool that compare text differences';

$fc = new Funcompare();
$res = $fc->compareText($old, $new);
echo $res;

// A tool <span class="new-word">that</span> compare text differences <span class="old-word">is</span> <span class="old-word">funny</span>

```
### compareJson()
```php
use Funsoul\Funcompare\Funcompare;

$old = '[{"id":1,"name":"xxx","age":18,"cart":[{"id":100,"name":"rice"}]},{"id":2,"name":"aaa","age":18}]';
$new = '[{"id":1,"name":"yyy","age":20,"cart":[{"id":100,"name":"banana"}]},{"id":2,"name":"bbb","age":18}]';

$fc = new Funcompare();
$res = $fc->compareJson($old, $new);
echo $res

// [{"name":{"old":"<span class=\"old-word\">xxx</span>","new":"<span class=\"new-word\">yyy</span>"},"age":{"old":"<span class=\"old-word\">18</span>","new":"<span class=\"new-word\">20</span>"},"cart":[{"name":{"old":"<span class=\"old-word\">rice</span>","new":"<span class=\"new-word\">banana</span>"}}]},{"name":{"old":"<span class=\"old-word\">aaa</span>","new":"<span class=\"new-word\">bbb</span>"}}]

```

```json
[
    {
        "name":{
            "old":"<span class="old-word">xxx</span>",
            "new":"<span class="new-word">yyy</span>"
        },
        "age":{
            "old":"<span class="old-word">18</span>",
            "new":"<span class="new-word">20</span>"
        },
        "cart":[
            {
                "name":{
                    "old":"<span class="old-word">rice</span>",
                    "new":"<span class="new-word">banana</span>"
                }
            }
        ]
    },
    {
        "name":{
            "old":"<span class="old-word">aaa</span>",
            "new":"<span class="new-word">bbb</span>"
        }
    }
]
```

### css

```css
<style>
    .new-word{background:rgba(245,255,178,1.00)}
    .new-word:after{content:' '; background:rgba(245,255,178,1.00)}
    .old-word{text-decoration:none; position:relative}
    .old-word:after{
        content: ' ';
        font-size: inherit;
        display: block;
        position: absolute;
        right: 0;
        left: 0;
        top: 55%;
        bottom: 30%;
        border-top: 1px solid #000;
        border-bottom: 1px solid #000;
    }
</style>
```

### wrapper()
```php
use Funsoul\Funcompare\Funcompare;

$old = 'A tool compare text differences is funny';
$new = 'A tool that compare text differences';

$fc = new Funcompare();
$res = $fc->wrapper('[',']','<','>')->compareText($old, $new);
echo $res;

// A tool <that> compare text differences [is] [funny]
```

# License

MIT