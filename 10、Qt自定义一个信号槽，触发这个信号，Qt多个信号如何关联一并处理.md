# 10、Qt自定义信号槽，如何知道是哪个信号的触发的槽函数

1. 使用QObject::sender()方法
这是最直接的方式，sender()会返回发送当前信号的对象指针，通过判断这个指针可以确定是哪个对象的信号触发了槽函数。
```c++
    void MyWidget::onSignalTriggered() {
        QObject *senderObj = sender();  // 获取发送信号的对象
        
        if (senderObj == m_button1) {
            qDebug() << "按钮1的信号触发了槽函数";
        } else if (senderObj == m_button2) {
            qDebug() << "按钮2的信号触发了槽函数";
        }
    }
```
2. 使用带参数的信号和槽
为不同信号设置不同的参数，在槽函数中通过参数值来区分信号来源。
3. 使用 Lambda 表达式作为中间层
在连接信号时使用 Lambda 表达式，在 Lambda 中明确标识信号来源后再调用槽函数。
```c++
connect(m_button1, &QPushButton::clicked, this, [this]() {
    this->handleSignal("button1");
});
connect(m_button2, &QPushButton::clicked, this, [this]() {
    this->handleSignal("button2");
});

void MyWidget::handleSignal(const QString &senderName) {
    qDebug() << senderName << "触发了信号";
}
