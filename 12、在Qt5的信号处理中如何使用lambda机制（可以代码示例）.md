# 12、在Qt5的信号处理中如何使用lambda机制（可以代码示例）

不写接受者和槽函数，直接写lambda表达式：
 


    QPushButton *button = new QPushButton("Click me", &window);

    // 使用lambda表达式连接按钮的clicked信号
    QObject::connect(button, &QPushButton::clicked, [&]() {
        // 当按钮被点击时，执行以下代码
        button->setText("Clicked!");
    });