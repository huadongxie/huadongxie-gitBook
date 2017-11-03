## History 对象

History 对象包含用户（在浏览器窗口中）访问过的 URL。

History 对象是 window 对象的一部分，可通过 window.history 属性对其进行访问。

注释：没有应用于 History 对象的公开标准，不过所有浏览器都支持该对象。

## History 对象描述

History 对象最初设计来表示窗口的浏览历史。但出于隐私方面的原因，History 对象不再允许脚本访问已经访问过的实际 URL。唯一保持使用的功能只有[back\(\)](http://www.w3school.com.cn/jsref/met_his_back.asp)、[forward\(\)](http://www.w3school.com.cn/jsref/met_his_forward.asp)和[go\(\)](http://www.w3school.com.cn/jsref/met_his_go.asp)方法。

