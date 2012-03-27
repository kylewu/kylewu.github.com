--- 
layout: post
title: !binary |
  5a2m5Lmg5L2/55SoVHdpdHRlcjRK

published: true
meta: {}

tags: 
- Coding
- Java
- Twitter
type: post
status: publish
---
<h2>What is Twitter4J?</h2>
<a href="http://yusuke.homeip.net/twitter4j/en/index.html" target="_blank">Twitter4J</a>是TwitterAPI的一个Java库。使用<a href="http://yusuke.homeip.net/twitter4j/en/index.html" target="_blank">Twitter4J</a>，你可以方便的将你的应用程序与Twitter服务结合。
<h2>How to use Twitter4J?</h2>
首先，从<a href="http://yusuke.homeip.net/twitter4j/en/index.html" target="_blank">Twitter4J</a>的网站上下载最新的<a href="http://yusuke.homeip.net/twitter4j/en/index.html" target="_blank">Twitter4J</a>的jar包。点<a href="http://yusuke.homeip.net/twitter4j/en/index.html#download" target="_blank">这里</a>可以进入下载界面。

下载完成后，让我们打开Eclipse，新建一个Java工程，不要忘记将Twitter4J的jar包加入Library中，见下图。

<img src="http://farm4.static.flickr.com/3568/3411419232_b67a10f6df_o.jpg" alt="" />

接下来我们可以创建一个net.kylewu.twitter.TwitterMain类，用来程序主流程。代码如下(代码比较多，折叠起来了，点箭头就可以看到完整的了)。
<code lang="java">
package net.kylewu.twitter;

import java.util.List;
import java.util.Scanner;

import twitter4j.DirectMessage;
import twitter4j.Query;
import twitter4j.QueryResult;
import twitter4j.Status;
import twitter4j.Tweet;
import twitter4j.Twitter;
import twitter4j.TwitterException;

/**
 * The main class of twitter client
 *
 * @author Kyle Wu
 *
 */
public class TwitterMain {

	public static void print(String string) {
		System.out.println(string);
	}

	public static void main(String[] args) {

		if (args.length < 2) {
			print("Usage: java net.kylewu.twitter.TwitterMain ID Password");
			System.exit(-1);
		}

		String strTip = "=========================n"
				+ "Please select what you want to do:n"
				+ "1. Updating statusn" + "2. Getting Timelinen"
				+ "3. Sending Direct Messagesn"
				+ "4. Receiving Direct Messagesn" + "5. Search for Tweetsn"
				+ "6. Asynchronous APIn"
				+ "0. Exitn" +
				"=========================";

		// Twitter class is the one you may want to look first
		Twitter twitter = new Twitter(args[0], args[1]);

		Scanner scanner = new Scanner(System.in);

		while (true) {
			print(strTip);

			String select = scanner.nextLine();

			if (select.compareTo(TwitterAction.UPDATE.toString()) == 0) {

				// get message
				print("Please input message you want to update:");
				String message = scanner.nextLine();

				try {
					// update here
					Status status = twitter.update(message);
					print("Successfully updated the status to ["
							+ status.getText() + "].");
				} catch (TwitterException e) {
					print("Error occured when updating");
					e.printStackTrace();
				}

			} else if (select.compareTo(TwitterAction.GETTIMELINE.toString()) == 0) {

				try {
					// get friend time line here
					List statuses = twitter.getFriendsTimeline();
					print("Showing friends timeline.");
					for (Status status : statuses) {
						print(status.getUser().getName() + ":"
								+ status.getText());
					}
				} catch (TwitterException e) {
					print("Error occured when getting friends timeline");
					e.printStackTrace();
				}

			} else if (select.compareTo(TwitterAction.SENDDIRECTMSG.toString()) == 0) {

				print("Please input id you want to send to :");
				String id = scanner.nextLine();
				print("Please input message you want to send to :");
				String message = scanner.nextLine();
				try {
					// send direct message here
					twitter.sendDirectMessage(id, message);
					print("Successfully send message to " + id + ".");
				} catch (Exception e) {
					print("Error occured when sending direct message");
					e.printStackTrace();
				}

			} else if (select.compareTo(TwitterAction.RECVDIRECTMSG.toString()) == 0) {

				try {
					// receive direct message here
					List list = twitter.getDirectMessages();
					print("There are " + list.size() + " messages");
					for (DirectMessage dm : list) {
						print("Sender:" + dm.getSenderScreenName());
						print("Text:" + dm.getText() + "n");

					}
				} catch (Exception e) {
					print("Error occured when receiving direct message");
					e.printStackTrace();
				}
			} else if (select.compareTo(TwitterAction.SEARCHFORTWEETS
					.toString()) == 0) {

				try {
					// search for tweets
					Query query = new Query("wenwu");
					QueryResult result = twitter.search(query);
					print("hits:" + result.getTotal());
					for (Tweet tweet : result.getTweets()) {
						print(tweet.getFromUser() + ":" + tweet.getText());
					}

				} catch (Exception e) {
					print("Error occured when searching for tweets");
					e.printStackTrace();
				}
			} else {
				// exit
				System.exit(0);
			}

		}
	}
}</code>

接下来创建一个net.kylewu.twitter.TwitterAction的Enum，主要是对各种消息进行枚举。代码如下。
<code lang="java">
package net.kylewu.twitter;

/**
 *
 * @author Kyle Wu
 *
 */
public enum TwitterAction {
	UPDATE(1),
	GETTIMELINE(2),
	SENDDIRECTMSG(3),
	RECVDIRECTMSG(4),
	SEARCHFORTWEETS(5);

	final private int type;

	private TwitterAction(int type) {
		this.type = type;
	}

	@Override
	public String toString() {
		return String.valueOf(this.type);
	}

	public int getType() {
		return this.type;
	}

}</code>
好了，我们运行一下，功能很简单是吧，当然代码也很简单。Twitter4J已经为我们做了很多事情，我们所要做的仅仅是调用Twitter类提供的一些方法。后面我还会发布一篇Twitter4J探秘，让我们从内部看看Twitter4J是如何帮助我们的:-)

哪位朋友用Twitter4J做了好的应用，别忘记告诉我一声哦。
