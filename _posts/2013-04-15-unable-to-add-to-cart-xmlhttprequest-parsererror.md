---
ID: 319
post_title: 'Unable to Add to Cart: XMLHttpRequest parsererror'
author: Luc
post_date: 2013-04-15 20:38:19
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/unable-to-add-to-cart-xmlhttprequest-parsererror/
published: true
---
<ul>
	<li>This is caused by a missing module in Apache: the mbstring module</li>

	<li>There are other similar errors mentioned on the forums, but 'parsererror' in particular is caused by the missing module above</li>

	<li>You need to run EasyUpdate in WHM and add mbstring in the Extended Options step</li>
</ul>



See <a href="http://www.prestashop.com/forums/topic/140974-error-thrown-object-xmlhttprequest-text-status-parsererror/">here</a> for more.