---
ID: 322
post_title: Percentage Calculator Function
author: Luc
post_date: 2013-04-16 08:01:15
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/percentage-calculator-function/
published: true
---
Something I seem to need a lot. 
<pre class="lang:js decode:true " title="Percentage calculator" >
function calculate(form, id) {
  a = form.q1.value;
  b = form.q2.value;

  switch(id) {
    case 1:
      total = (a / 100) * b; //What is a percent of b?
      break;
    case 2:
      total = (a / b) * 100; //a is what percent of b?
      break;
    case 3:
      total = (b - a) / a * 100; //What is the percentage increase/decrease from a to b?
      break;
    case 4:
      total = (a / b) * 100; //a is b percent of what?
      break;
  }
  form.total.value = total;
}
</pre>