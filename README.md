# CodeIgniter 视图继承类库

 为 CodeIgniter 框架增加视图继承功能，不改变原有视图编写方式，无缝增加视图继承功能。

## 安装方法

1. 把 `Hulk_template.php` 放到 `./application/libraries` 目录下
2. 创建目录 `./application/third_party/hulk_template/views`，如果目录不存在则要自己手动逐级创建。
3. 把 `./application/third_party/hulk_template/views` 目录设为可写，Linux 下一定要保证 Apache 或 Nginx 对这个目录可写。

## 例子

父视图 ./application/views/parent_message.php :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Welcome to <# block title #>CodeIgniter<# /block #></title>
</head>
<body>
    <h1>Welcome to <# block title #>CodeIgniter<# /block #>!</h1>
</body>
</html>
```

子视图 ./application/views/welcome_message.php :

```html
<# extends parent_message #>

<# block title #>CI Chinese<# /block #>
```

控制器：

```php
class Welcome extends CI_Controller {

    public function index()
    {
        // 载入类库
        $this->load->library('hulk_template');

        // 加载子视图。这里可直接代替 $this->load->view() 的功能。
        $this->hulk_template->parse('welcome_message');
    }
}
```

## 视图继承语法

实现视图继承的标签采用 <# 开头，#> 结尾。例如：`<# block #>`

### extends 标签

```
<# extends 视图路径 #>
```

例如 `<# extends welcome/test #>`

这里指的是从 `./application/views/welcome/test.php` 这个视图继承。

注意：`extends` 标签必须在视图文件首行首字母位置。另外这个标签不需要结束标签。

### block 标签

```
<# block 名称 #>内容...<# /block #>
```

在父视图中使用 block 代表定义一个名为“名称”的 block。

在子视图中使用 block 代表替换父视图中同名的 block。

### parent 标签

```
<# block 名称 #>
  <# parent #>

  内容...
<# /block #>
```

`parent` 标签只能在 `block` 标签中使用，功能是把父模板相同 block 名称的内容放到当前 block 中 parent 所在位置。

### child 标签

```
<# block 名称 #>
  <# child #>

  内容...
<# /block #>
```

`child` 标签只能在 `block` 标签中使用，功能是把子模板相同 block 名称的内容放到当前 block 中 child 所在位置。

### slot 标签

```
<# block 名称 #>
  <# slot 插槽名称 #>
    内容
  <# /slot #>

  内容...
<# /block #>
```

`slot` 标签只能在 `block` 标签中使用。

`slot` 标签是用于在父模板中定义一些插槽位置，子模板会替换父模板相同插槽名称所在位置的内容。

### call 标签

```
<# block 名称 #>
  <# call 其它block名称 #>
    <# slot 插槽名称 #>
      内容
    <# /slot #>
  <# /call #>

  内容...
<# /block #>
```

`call` 用于把当前文件其它 block 名称的内容，替换 call 所在位置的内容。其中 `slot` 的意义与上节一样，会替换相应的内容。

### use 标签

```
<# block 名称 #>
  <# use 其它block名称 #>

  内容...
<# /block #>
```

`use` 是简化版的 `call`，如果不需要替换 `slot` 的内容，可以直接使用 `use`。
