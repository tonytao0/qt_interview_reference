# 103、Qt的智能指针QSharedPointer和shared_ptr有什么区别，weak_ptr呢？

QSharePointer是一种智能指针，它可以自动管理指向的对象的内存分配和释放，从而实现自动内存管理。

shared_ptr也是一种智能指针，它可以跟踪指向的对象的引用计数，从而保证在没有任何引用的情况下，可以自动释放指向的对象。

weak_ptr是一种特殊的shared_ptr，它可以指向shared_ptr指向的对象，但不会增加指向对象的引用计数。它可以用来避免循环引用导致的内存泄漏问题。

它们的主要区别如下：  

    所有权管理方式  
    QSharedPointer：当对象实现了“写时复制”或是隐式共享机制类型(如QVector)， 被复制时仅复制指针而不复制实际数据，直到发生修改操作时才进行深拷贝（写时复制）  
    std::shared_ptr：通过引用计数管理对象生命周期，复制时仅增加引用计数，不涉及数据拷贝

    线程安全性
    QSharedPointer：引用计数操作是线程安全的，但指向的对象本身需要额外同步  
    std::shared_ptr（C++11 及以后）：引用计数的修改是原子操作，线程安全，但同样不保证所指对象的线程安全
    
    与 Qt 框架的集成
    QSharedPointer：与 Qt 的元对象系统（QObject）深度集成，可以安全管理 QObject 派生类对象，支持qobject_cast等 Qt 特有的类型转换
    std::shared_ptr：标准库组件，与 Qt 框架没有特殊集成，管理 QObject时需要额外注意父对象机制

    自定义删除器
    QSharedPointer：通过QSharedPointer::setDeleter()设置删除器，语法相对复杂  
    std::shared_ptr：在构造时直接指定删除器，语法更简洁直观

    空指针处理
    QSharedPointer：提供isNull()方法检查空指针，行为更接近 Qt 的编程风格  
    std::shared_ptr：使用operator bool()判断是否为空，符合标准库习惯

    循环引用解决  
    QSharedPointer：配合QWeakPointer使用来打破循环引用
    std::shared_ptr：配合std::weak_ptr使用，机制类似但接口不同