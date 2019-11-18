# fuckRuanyifengBlogAd
### 屏蔽阮一峰博客的广告

1. 安装[Adblock plus](https://chrome.google.com/webstore/detail/adblock-plus-free-ad-bloc/cfhdojbkjhnklbpkdaibdccddilifddb)并且自定义列表加入以下字段

```
@@||www.ruanyifeng.com^$csp,domain=www.ruanyifeng.com
```

2. 安装[tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) 并且添加以下屏蔽js

> 修改自[阮一峰 blog ad](https://greasyfork.org/zh-CN/scripts/375685-%E9%98%AE%E4%B8%80%E5%B3%B0-blog-ad) 的匹配地址

```
1.adblock plus 自定义列表加入

@@||www.ruanyifeng.com^$csp,domain=www.ruanyifeng.com

2.tampermonkey 加入以下js

// ==UserScript==
// @name         阮一峰 blog ad
// @namespace    http://tampermonkey.net/
// @version      0.2
// @description  防止 阮一峰 博客屏蔽adblock
// @author       You
// @edit         chn-student
// @match        *://www.ruanyifeng.com/*
// @match        *://*.ruanyifeng.com/*
// @grant        none
// @run-at       document-end
// ==/UserScript==

(function() {
    'use strict';
    // Your code here...
    // console.info('Hello Tampermonkey');

    var img = document.createElement('img');
    img.setAttribute('src', 'wangbase.com/blogimg/asset/');
    img.width = 0;
    img.height = 0;
    var a = document.createElement('a');
    a.appendChild(img)
    document.body.insertBefore(a, document.body.firstChild);

    var oldGetComputedStyle = window.getComputedStyle;

    window.getComputedStyle = function(dom) {
        if (dom == img) {
			return {
				display: 'block'
			};
		} else {
			return oldGetComputedStyle(dom);
		}
    };

})();
```
