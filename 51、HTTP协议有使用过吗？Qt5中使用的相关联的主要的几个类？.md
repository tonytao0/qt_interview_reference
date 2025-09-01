# 51、HTTP协议有使用过吗？Qt5中使用的相关联的主要的几个类？

QNetworkAccessManager：管理所有网络请求，是 HTTP 操作的核心入口。
QNetworkRequest：表示一个网络请求（包含 URL、请求头、协议版本等）。
QNetworkReply：表示请求的响应（包含返回的数据、状态码、错误信息等）。
辅助类：QUrl（处理 URL）、QByteArray（处理二进制数据）、QJsonDocument（处理 JSON 数据，需Qt Core模块）
