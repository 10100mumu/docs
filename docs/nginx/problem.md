# Nginx 常见问题

**相同 server_name 虚拟主机的优先级**

按照配置文件的顺序，先配置的生效

**多个 location 的优先级**

* `=`：普通字符匹配，完全匹配
* `^~`：普通匹配，前缀匹配
* `~ \~*`：执行一个正则匹配，`～`区分大小写，`～*`不区分大小写