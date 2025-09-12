# 3、描述Qt中的文件流(QTextStream)和数据流(QDataStream)的区别

在Qt中，QTextStream和QDataStream都是用于读写数据的类，都可以操作文件和套接字设备，但它们所处理的数据类型不同，QTextStream主要处理文本数据，而QDataStream主要处理二进制数据。 

QTextStream – 处理文本数据, 操作轻量级数据(int, double, QString), 数据写入文件中之后以文本的方式呈现。  
QDataStream - 处理二进制数据，支持几乎所有Qt基础类型（int、double、QByteArray、QString、QImage等），以及自定义类型（需注册）。以二进制方式读写到文件、套接字等设备。  

| 对比项 | QTextStream | QDataStream |
| --- | --- | --- |
| 数据形式 | 所有数据转为字符串（文本形式） | 保留数据的原始二进制形式（类型相关） |
| 写入int| 字符串形式（如 123） | 二进制形式（4 字节，如 0x0000007B） |
| 可读性（人类） | 高（可直接用文本编辑器打开） |  低（二进制数据，需用对应程序解析）|
| 用途 | 文本交互（人可阅读） | 数据存储/传输（程序间交互，保留类型信息） |
| 文件打开方式 | QIODevice::Text | 默认二进制 |
| 写入QString的结果 | 直接写入字符序列（带编码） | 先写4字节长度+字符的二进制编码（UTF-16） |


QDataStream 直接操作对象，需要重载操作符
``` c++
#include <QDataStream>
#include <QString>

class Student {
public:
    QString id;
    QString name;
    int score;
};
// 序列化：将Student对象写入QDataStream
QDataStream& operator<<(QDataStream& out, const Student& s) {
    // 按顺序写入所有成员变量
    out << s.id << s.name << s.score;
    return out;
}
// 反序列化：从QDataStream读取并还原Student对象
QDataStream& operator>>(QDataStream& in, Student& s) {
    // 必须按序列化时的顺序读取
    in >> s.id >> s.name >> s.score;
    return in;
}
Student stu;
QByteArray buffer;
QDataStream out(&buffer, QIODevice::WriteOnly);
out << stu; // 现在可以直接写入自定义对象
```
	
		
		
