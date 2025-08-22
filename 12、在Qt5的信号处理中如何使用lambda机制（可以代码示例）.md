# 12、在Qt5的信号处理中如何使用lambda机制（可以代码示例）

不写接受者和槽函数，直接写lambda表达式：
```c++
QPushButton *button = new QPushButton("Click me", &window);

QPushButton *button = new QPushButton("Click me", &window);
// 使用lambda表达式连接按钮的clicked信号
QObject::connect(button, &QPushButton::clicked, [button]() {
    button->setText("Clicked!");
});