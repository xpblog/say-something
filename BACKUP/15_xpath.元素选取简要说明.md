# [xpath 元素选取简要说明](https://github.com/xpblog/say-something/issues/15)

[返回目录](https://github.com/xpblog/say-something)

<html>
<body>
<!--StartFragment-->

表达式 | 描述
-- | --
node_name | 选取此节点的所有子节点。
/ | 绝对路径匹配，从根节点选取。
// | 相对路径匹配，从所有节点中查找当前选择的节点，包括子节点和后代节点，其第一个 / 表示根节点。
. | 选取当前节点。
.. | 选取当前节点的父节点。
@ | 选取属性值，通过属性值选取数据。常用元素属性有 @id 、@name、@type、@class、@tittle、@href。

<!--EndFragment-->
</body>
</html>