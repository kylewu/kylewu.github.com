---
layout: post
title: "Handle mail log"
description: "Do complex job in one command"
category: Terminal
tags: [terminal, linux]
---
{% include JB/setup %}

It is the end of March today, so I am going to send mass mails to my users. One
big problem to send tons of email is to avoid being recognized as a spammer.
However, this is not the topic of this post. I am gonna use one line to handle
mail log, and update status in database.

Some users may use unavailable email account, which is quite a waste to send to
them. So when I get one error in mail log, I should update database in order to
avoid to send to this address in the next time.

The command is as below:

	cat /var/log/mail.log | grep "User unknown" | grep -v "postmaster" | awk {'print $7'} | cut -d "=" -f 2 | tr -d "<>,"| xargs -i mysql -uxxxx -pxxxx xxxx -e 'update mail_subscriber set status=-1 where email="{}";'

It is quite straightforward. First it get lines I am interested in. Then get
email address from these lines. At last, execute one update sql clause. Please
notice, there are many different error message in the log and this command only
takes care of 'User unknow' error.
