# 134、strcpy/sprintf/memcpy它们之间区别？

strcpy、sprintf和memcpy都是C语言中的字符串和内存操作函数，它们之间的主要区别如下：


strcpy：字符串复制函数，用于将源字符串（以 \0 结尾）完整地复制到目标缓冲区，包括结束符 \0。函数原型为：char *strcpy(char *dest, const char *src)；

sprintf：格式化字符串输出函数，将格式化的数据写入目标字符串缓冲区，自动添加结束符 \0。支持多种数据类型（如整数、浮点数、字符串等）的格式化拼接。函数原型为：int sprintf(char *buf, const char *format, ...)；

memcpy：内存块复制函数，按字节复制指定长度的内存数据，不关心数据内容（可以是字符串、数组、结构体等），也不处理结束符'\0'。函数原型为：void *memcpy(void *dest, const void *src, size_t n)；
