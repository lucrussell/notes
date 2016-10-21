---
ID: 313
post_title: >
  PrestaShop Maintenance Mode Sends a 503
  Status
author: Luc
post_date: 2013-04-15 20:34:35
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/prestashop-maintenance-mode-sends-a-503-status/
published: true
---

For some reason, maintenance mode sets a status of 503 which causes some browsers to display an error message. Comment the offending line in classes/FrontController.php. See <a href="http://alvinjiang.blogspot.co.uk/2011/12/prestashop-tips-issues-when-yous.html">this link</a> for more details.