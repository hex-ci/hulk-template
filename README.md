CodeIgniter 视图继承类库
=============

 为 CodeIgniter 框架增加视图继承功能，不改变原有视图编写方式，无缝增加视图继承功能。

### 安装方法：

- 把 `Hulk_template.php` 放到 `./application/libraries` 目录下
- 创建目录 `./application/third_party/hulk_template/views`，如果目录不存在则要自己手动逐级创建。
- 把 `./application/third_party/hulk_template/views` 目录设为可写，Linux 下一定要保证 Apache 或 Nginx 对这个目录可写。