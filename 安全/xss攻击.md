## 定义
跨站脚本（Cross-site scripting，通常简称为XSS）是一种网站应用程序的安全漏洞攻击，是代码注入的一种。它允许恶意用户将代码注入到网页上，其他用户在观看网页时就会受到影响。这类攻击通常包含了HTML以及用户端脚本语言。
## 防范
- 将用户所提供的内容进行过滤
- 使用HTTP头指定内容的类型，使得输出的内容避免被作为HTML解析