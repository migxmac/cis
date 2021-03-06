---
copyright:
  years: 2018
lastupdated: "2018-03-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 将页面规则与高速缓存配合使用

页面规则使您能够根据页面的 URL 来执行各种操作，例如，创建重定向、微调高速缓存行为，或者启用和禁用服务。

页面规则对与以下格式匹配的给定 URL 模式生效：

`<scheme>://<hostname><:port>/<path>`

例如：


`https://www.example.com:80/image.png`

`scheme` 和 `port` 部分是可选的。如果省略 `scheme` 部分，那么格式接受 `http://` 和 `https://` 协议。如果未指定 `port`，那么规则与所有端口匹配。您可以通过在规则模式中使用 `*` 符号来执行基本通配符匹配，从而使其与一系列相似模式匹配。

**有关页面规则的重要事项：**

 * 对于任何给定请求，仅会有一个页面规则生效。
 * 将按从上到下的顺序对页面规则指定优先级。URL 匹配规则后，将仅应用规则；也就是说，如果请求中已触发页面规则，那么与该 URL 模式匹配的任何后续规则都不会生效。 
 * 通常，建议从具体到通用对规则进行排序。
 * 可以禁用页面规则，在此情况下，页面规则将不执行任何操作，但仍可在列表中显示且可进行编辑。将*已启用*开关设置为“关闭”会创建页面规则，此规则最初为禁用状态。


## 转发（URL 重定向）
使用 HTTP 301 或 302 重定向将一个 URL 重定向到另一个 URL。可以使用 `$X` 语法引用 URL 中通配符匹配的任何部分的内容。`X` 指示模式中的 glob 的索引：`$1` 将替换为第一个匹配通配符，`$2` 替换为第二个匹配通配符，依此类推。

例如，假设设置以下规则：

![image](images/url-redirection-example.png)

在此示例中，对“www.example.com/stuff/things”的请求将重定向到“http://example.com/stuff/things”。

**注：**请注意，不要创建域指向其自身作为目标的重定向。此错误可能导致无限重定向错误，并且受影响的 URL 将无法解析。


## 重定向到 HTTPS
如果要重定向访客以使用 HTTPS，请改为使用**始终使用 HTTPS** 设置：

![image2](images/url-matching-patterns.png)


## 定制高速缓存
使用任何标准高速缓存级别，为任何与“页面规则”模式相匹配的 URL 设置高速缓存行为。将**高速缓存级别**设置为**高速缓存所有内容**，会对任何内容进行高速缓存，即使此内容不是缺省静态文件类型之一也是如此。将**高速缓存级别**设置为**绕过**可阻止在该 URL 上进行高速缓存。

使用页面规则指定高速缓存级别时，可以设置**边缘高速缓存 TTL**，这可控制 CIS 将在高速缓存中保留文件的时间。

**浏览器高速缓存 TTL** 控制客户机浏览器高速缓存的资源保持有效的时间长度。如果浏览器再次请求资源且 TTL 未到期，那么浏览器会收到 `HTTP 304 (Not Modified)` 响应。可以设置范围为 30 分钟到 1 年的 TTL。

并非所有缺省高速缓存行为都严格符合 RFC。通过“页面规则”设置**源高速缓存控制**，会使用一组较新的高速缓存规则，此组规则旨在更严格地遵循 RFC，尤其在重新验证方面。例如，`max-age=0` 这一缺省行为根本不会进行高速缓存，而设置**源高速缓存控制**则会高速缓存，但始终会重新验证。

以下示例设置页面规则来高速缓存在 `/images` 文件夹中找到的所有内容。在用户浏览器中，高速缓存的资源在 30 分钟后到期，在 IBM CIS 数据中心中，则一天后到期：

![image3](images/url-example.png)
