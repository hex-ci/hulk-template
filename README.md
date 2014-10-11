CodeIgniter 视图继承类库
=============

 为 CodeIgniter 框架增加视图继承功能，不改变原有视图编写方式，无缝增加视图继承功能。

### 安装方法

1. 把 `Hulk_template.php` 放到 `./application/libraries` 目录下
2. 创建目录 `./application/third_party/hulk_template/views`，如果目录不存在则要自己手动逐级创建。
3. 把 `./application/third_party/hulk_template/views` 目录设为可写，Linux 下一定要保证 Apache 或 Nginx 对这个目录可写。

### 例子

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