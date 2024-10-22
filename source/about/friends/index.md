---
layout: page
menu_id: about
breadcrumb: false
comments: false
---

{% navbar active:/about/friends/ [关于本站](/about/) [我的好友](/about/friends/) [关于我](/about/me/) %}

{% friends api:https://raw.githubusercontent.com/Timor2016/friends/refs/heads/output/v2/data.json %}