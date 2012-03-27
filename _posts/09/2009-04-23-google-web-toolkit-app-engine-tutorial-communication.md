--- 
layout: post
title: !binary |
  R29vZ2xlIFdlYiBUb29sa2l0IOWSjCBHb29nbGUgQXBwIEVuZ2luZSDnu7zl
  kIjmlZnnqIsg5Lqk5LqS56+H

published: true
meta: {}

tags: 
- Coding
- Eclipse
- GAE
- Google
- GWT
- Java
- Web
type: post
status: publish
---
前面几篇教程已经把Google Web Toolkit 和 Google App Engine 两方面的代码完成了很大部分，这篇教程将让Google Web Toolkit 的客户端代码与 Google App Engine 的服务器端代码联合起来，实现客户端和服务器端的交互。
<h2>Google Web Toolkit 如何与服务器交互？</h2>
Google Web Toolkit 的程序最终会以JavaScript代码的形式在用户的浏览器上运行。所以，如果要与服务器交互，要使用JavaScript支持的方法。Google Web Toolkit 为我们提供了3种方法。
<h3>远程过程调用 (Remote Procedure Calls, GWT RPC)</h3>
如果项目的服务器端使用Java，并且为服务器端的操作都使用了各种接口，那么 GWT RPC是最好的选择。因为我们使用 Google App Engine 作为服务器端，使用Java编码，所以接下来将使用 GWT RPC来完成我们接下来的教程。
更详细的有关 Remote Procedure Calls 的介绍，请看<a href="http://code.google.com/webtoolkit/tutorials/1.6/RPC.html" target="_blank">这里</a>。
<h3>HTTP 取回 JSON</h3>
如果项目的服务器端没有使用Java，亦或是已经使用了JSON 或 XML，那么就可以通过HTTP来取得JSON来实现与服务器端的交互。
更详细的有关 JSON 的介绍，请看<a href="http://code.google.com/webtoolkit/tutorials/1.6/JSON.html" target="_blank">这里</a>。
<h3>利用 JSONP 协议</h3>
如果你对 mashup 很感兴趣，那么一定不能错过 Google Web Toolkit 提供的这种方法。
更详细的有关 JSONP 的介绍，请看<a href="http://code.google.com/webtoolkit/tutorials/1.6/Xsite.html" target="_blank">这里</a>。
<h2>定义 Service Interface</h2>
<!--more-->

RPC Service 要由一个 继承自 RemoteService 的接口来定义。这里我们在 net.kylewu.myideastorm.client.service 包下面新建一个名为 DBWorkerService 的接口。
<code lang="java">package net.kylewu.idea.client.service;

import com.google.gwt.user.client.rpc.RemoteService;
import com.google.gwt.user.client.rpc.RemoteServiceRelativePath;

/**
 * * The client side stub for the RPC service.
 * */
@RemoteServiceRelativePath("myidea")
public interface DBWorkerService extends RemoteService {

	// Remove one idea
	Boolean delete(Long id);

	String getIdeaBySubject(String subject);

	// Read from db
	String[] getIdeas();

	// Add a new idea
	String save(String subject, String detail, String progress);

	// Update one idea
	String update(String id, String subject, String detail, String progress);

}</code>
肯定有人注意到了，这里方法返回的值都是String，为什么不使用我们之前定义过的Idea呢。这里我只能说很抱歉了，我测试过返回Idea对象，但是在运行时会出现 “did you forget to inherit a required module?”的错误，搜索了很久也没有搞定，希望知道的同学联系我，谢谢。
<h2>定义服务器端Service实现</h2>
服务器端的类要实现刚才写过的 DBWorkerService 接口，在这里实现我们具体的操作。
<code lang="java">package net.kylewu.idea.server;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.List;

import javax.jdo.PersistenceManager;
import javax.jdo.Query;

import net.kylewu.idea.client.service.DBWorkerService;

import com.google.gwt.user.server.rpc.RemoteServiceServlet;

public class DBWorkerServiceImpl extends RemoteServiceServlet implements
		DBWorkerService {

	private static final long serialVersionUID = 6183858098728558886L;

	@Override
	public Boolean delete(Long id) {
		PersistenceManager pm = PMF.get().getPersistenceManager();
		Idea idea = (Idea) pm.getObjectById(Idea.class, id);
		pm.deletePersistent(idea);
		pm.close();
		return true;
	}

	@SuppressWarnings("unchecked")
	@Override
	public String[] getIdeas() {
		PersistenceManager pm = PMF.get().getPersistenceManager();
		String query = "select from " + Idea.class.getName();
		List ideas = (List) pm.newQuery(query).execute();
		String[] rtn = new String[ideas.size()];
		for (int i = 0; i < ideas.size(); i++) {
			Idea idea = ideas.get(i);
			rtn[i] = idea.toString();
		}

		return rtn;
	}

	@Override
	public String save(String subject, String detail, String progress) {
		Idea idea = new Idea(subject, detail, progress,
				progress.compareTo("100%") == 0 ? new SimpleDateFormat("yyyy-mm-dd")
						.format(new Date()) : "null");
		PersistenceManager pm = PMF.get().getPersistenceManager();
		try {
			pm.makePersistent(idea);
		} finally {
			pm.close();
		}
		String str = getIdeaBySubject(subject);
		return str;
	}

	@Override
	public String update(String id, String subject, String detail,
			String progress) {
		PersistenceManager pm = PMF.get().getPersistenceManager();
		Idea idea = (Idea) pm.getObjectById(Idea.class, Long.valueOf(id));
		idea.setSubject(subject);
		idea.setDetail(detail);
		idea.setProgress(progress);
		if (progress.compareTo("100%") == 0
				&& idea.getDate().compareTo("null") == 0) {
			idea.setDate(new SimpleDateFormat("yyyy-mm-dd").format(new Date()));
		}
		pm.makePersistent(idea);

		String rtn = ((Idea) pm.getObjectById(Idea.class, Long.valueOf(id)))
				.toString();
		pm.close();

		return rtn;
	}

	@SuppressWarnings("unchecked")
	@Override
	public String getIdeaBySubject(String subject) {
		PersistenceManager pm = PMF.get().getPersistenceManager();
		Query query = pm.newQuery("select from " + Idea.class.getName()
				+ " where subject == subjectParm "
				+ "parameters String subjectParm");
		List ids = (List) query.execute(subject);
		if (ids.isEmpty() == false) {
			pm.close();
			return ids.get(0).toString();
		}
		pm.close();
		return "";
	}

}</code>
如上一篇教程最后部分提到的，这里通过PMF得到PersistenceManager，进而进行数据库的增删改查。
<h2>定义 RPC Interface</h2>
代码很简单，在我们的DBWorkerService接口中的方法的参数最后添加一个AsyncCallback参数，并且这些方法都是void。
<code lang="java">package net.kylewu.idea.client.service;

import com.google.gwt.user.client.rpc.AsyncCallback;

/**
 * The async counterpart of DBWorker.
 */
public interface DBWorkerServiceAsync {

	// Remove one idea
	void delete(Long id, AsyncCallback callback);

	// Read from db
	void getIdeas(AsyncCallback callback);

	// Add a new idea
	void save(String subject, String summary, String progress, AsyncCallback callback);

	// Update one idea
	void update(String id, String summary, String subject, String progress,	AsyncCallback callback);

	void getIdeaBySubject(String subject, AsyncCallback callback);

}</code>
好了，到这里，就可以调用 RPC 接口了。
<h2>调用 RPC Interface</h2>
重新打开EntryPoint，在类中添加一段如下代码，然后在需要数据库操作的地方添加代码。
<pre lang="java">private DBWorkerServiceAsync dbWorker = GWT.create(DBWorkerService.class);</pre>
这里是最后完整的Kylewuidea类。
<code lang="java">package net.kylewu.idea.client;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

import net.kylewu.idea.client.service.DBWorkerService;
import net.kylewu.idea.client.service.DBWorkerServiceAsync;

import com.google.gwt.core.client.EntryPoint;
import com.google.gwt.core.client.GWT;
import com.google.gwt.event.dom.client.ClickEvent;
import com.google.gwt.event.dom.client.ClickHandler;
import com.google.gwt.user.client.rpc.AsyncCallback;
import com.google.gwt.user.client.ui.Button;
import com.google.gwt.user.client.ui.DialogBox;
import com.google.gwt.user.client.ui.FlexTable;
import com.google.gwt.user.client.ui.HasHorizontalAlignment;
import com.google.gwt.user.client.ui.HasVerticalAlignment;
import com.google.gwt.user.client.ui.HorizontalPanel;
import com.google.gwt.user.client.ui.ListBox;
import com.google.gwt.user.client.ui.Panel;
import com.google.gwt.user.client.ui.RootPanel;
import com.google.gwt.user.client.ui.TextArea;
import com.google.gwt.user.client.ui.TextBox;
import com.google.gwt.user.client.ui.VerticalPanel;

/**
 * Entry point classes define onModuleLoad().
 */
public class Kylewuidea implements EntryPoint {

	private final int COL_ID = 0;
	private final int COL_SUBJECT = 1;
	private final int COL_DETAIL = 2;
	private final int COL_PROGRESS = 3;
	private final int COL_TIME = 4;
	private final int COL_OPERATION = 5;

	private FlexTable table = new FlexTable();

	private ArrayList subjectList = new ArrayList();

	private Map mapStrToInt = new HashMap();
	private Map mapIntToStr = new HashMap();

	private DBWorkerServiceAsync dbWorker = GWT.create(DBWorkerService.class);

	/**
	 * This is the entry point method.
	 */
	public void onModuleLoad() {

		// Initial all items.
		init();
		// Add table to html page.
		RootPanel.get("ideastorm").add(createBasePanel());
		// Initial table.
		importFromDatabase();

	}

	private void init() {

		mapStrToInt.put("0%", 0);
		mapStrToInt.put("25%", 1);
		mapStrToInt.put("50%", 2);
		mapStrToInt.put("75%", 3);
		mapStrToInt.put("100%", 4);
		mapIntToStr.put(0, "0%");
		mapIntToStr.put(1, "25%");
		mapIntToStr.put(2, "50%");
		mapIntToStr.put(3, "75");
		mapIntToStr.put(4, "100%");

		// Initial table structure.
		table.setText(0, COL_ID, "ID");
		table.setText(0, COL_SUBJECT, "Subject");
		table.setText(0, COL_DETAIL, "Detail");
		table.setText(0, COL_PROGRESS, "Progress");
		table.setText(0, COL_OPERATION, "Operation");
		table.setText(0, COL_TIME, "Time");

		// Set table attribute.
		table.setCellPadding(5);
		table.getColumnFormatter().setWidth(0, "10");
		table.getColumnFormatter().setWidth(1, "200");
		table.getColumnFormatter().setWidth(2, "400");
		table.getColumnFormatter().setWidth(3, "150");
		table.getColumnFormatter().setWidth(4, "100");
	}

	/**
	 * Initial table data
	 */
	private void importFromDatabase() {
		// Get exist ideas from db
		dbWorker.getIdeas(new AsyncCallback() {

			@Override
			public void onFailure(Throwable caught) {
				// TODO Exception

			}

			@Override
			public void onSuccess(String[] result) {
				for (String idea : result) {
					String[] parts = idea.split("\|");
					insertIdeaIntoTable(-1, parts[0], parts[1], parts[2],
							parts[3], parts[4]);

				}
			}

		});

	}

	/**
	 * Create base panel
	 *
	 * @return
	 */
	private Panel createBasePanel() {
		// Base Panel of this project.
		VerticalPanel mainPanel = new VerticalPanel();
		Button btnAdd = new Button("Add Idea");

		// Add click handler to add button.
		btnAdd.addClickHandler(new ClickHandler() {
			public void onClick(ClickEvent event) {
				// Show Add Idea Dialog
				showIdeaEditDialog(true, -1);
			}
		});

		// Assemble the panel.
		mainPanel.setHorizontalAlignment(HasHorizontalAlignment.ALIGN_CENTER);
		mainPanel.add(table);
		mainPanel.add(btnAdd);

		return mainPanel;
	}

	/**
	 * Show Add Idea Dialog
	 */
	private void showIdeaEditDialog(final boolean isNew, final int index) {
		// Initial Add Idea Dialog.
		final DialogBox dialog = new DialogBox();
		final TextBox txtBoxSubject = new TextBox();
		final TextArea txtAreaDetail = new TextArea();
		final ListBox listBox = new ListBox();
		VerticalPanel dialogPanel = new VerticalPanel();
		HorizontalPanel itemPanel = new HorizontalPanel();
		Button btnInsert = new Button();
		Button btnClose = new Button("Close");

		// Set attribute.
		dialog.setText("Input your idea");
		dialog.setAnimationEnabled(true);
		txtAreaDetail.setSize("300", "380");
		listBox.clear();
		listBox.addItem("0%");
		listBox.addItem("25%");
		listBox.addItem("50%");
		listBox.addItem("75%");
		listBox.addItem("100%");
		listBox.setVisibleItemCount(5);

		if (isNew) {
			btnInsert.setText("Insert");
			txtBoxSubject.setText("Input your indea");
			listBox.setSelectedIndex(0);
		} else {
			btnInsert.setText("Update");
			txtBoxSubject.setText(table.getText(index, COL_SUBJECT));
			txtAreaDetail.setText(table.getText(index, COL_DETAIL));
			listBox.setSelectedIndex(mapStrToInt.get(table.getText(index,
					COL_PROGRESS)));
			if (table.getText(index, COL_PROGRESS).compareTo("100%") == 0  )
				listBox.setEnabled(false);
		}

		// Add ClickHandler to Insert button
		btnInsert.addClickHandler(new ClickHandler() {
			public void onClick(ClickEvent event) {
				// Check empty
				if (txtBoxSubject.getText().length() == 0
						|| txtAreaDetail.getText().length() == 0)
					return;
				// Check exist
				if (subjectList.contains(txtBoxSubject.getText()) == true
						&& isNew) {
					return;
				}

				insert(index, txtBoxSubject.getText(), txtAreaDetail.getText(),
						mapIntToStr.get(listBox.getSelectedIndex()));
				dialog.hide();
			}

		});

		// Add ClickHandler to Close button
		btnClose.addClickHandler(new ClickHandler() {
			public void onClick(ClickEvent event) {
				dialog.hide();
			}
		});

		// Assemble dialog panel.
		itemPanel.setWidth("100%");
		itemPanel.setVerticalAlignment(HasVerticalAlignment.ALIGN_MIDDLE);
		itemPanel.add(listBox);
		itemPanel.add(btnInsert);
		itemPanel.add(btnClose);
		dialogPanel.add(txtBoxSubject);
		dialogPanel.add(txtAreaDetail);
		dialogPanel.add(itemPanel);

		// Associate the dialog with the panel.
		dialog.setWidget(dialogPanel);

		// Show dialog.
		dialog.center();
	}

	private void insert(final int index, final String subject,
			final String detail, final String progress) {
		if (index == -1) {
			// new idea
			dbWorker.save(subject, detail, progress,
					new AsyncCallback() {

						@Override
						public void onFailure(Throwable caught) {
							// TODO Auto-generated method stub
						}

						@Override
						public void onSuccess(String idea) {
							if (idea.length() != 0) {
								String[] parts = idea.split("\|");
								insertIdeaIntoTable(index, parts[0], parts[1],
										parts[2], parts[3],
										parts[4] == "null" ? "" : parts[4]);
							}
						}

					});
		} else {
			dbWorker.update(table.getText(index, COL_ID), subject, detail,
					progress, new AsyncCallback() {

						@Override
						public void onFailure(Throwable caught) {
							// TODO Auto-generated method stub

						}

						@Override
						public void onSuccess(String idea) {
							if (idea.length() != 0) {
								String[] parts = idea.split("\|");
								insertIdeaIntoTable(index, parts[0], parts[1],
										parts[2], parts[3],
										parts[4].compareTo("null")==0 ? "" : parts[4]);
							}
						}

					});
		}
	}

	private void insertIdeaIntoTable(int index, final String id,
			final String subject, String detail, String progress, String date) {
		//
		if (index == -1) {
			index = table.getRowCount();
			subjectList.add(subject);
		} else {
			subjectList.set(index - 1, subject);
		}

		HorizontalPanel panel = new HorizontalPanel();
		Button btnUpdate = new Button("Update");
		Button btnRemove = new Button("Remove");

		// Add handler to buttons
		btnUpdate.addClickHandler(new ClickHandler() {

			@Override
			public void onClick(ClickEvent event) {
				int i = subjectList.indexOf(subject);
				showIdeaEditDialog(false, i + 1);
			}

		});

		btnRemove.addClickHandler(new ClickHandler() {

			@Override
			public void onClick(ClickEvent event) {
				dbWorker.delete(Long.valueOf(id), new AsyncCallback() {

					@Override
					public void onFailure(Throwable caught) {
						// TODO Auto-generated method stub

					}

					@Override
					public void onSuccess(Boolean result) {
						int i = subjectList.indexOf(subject);
						table.removeRow(i + 1);
						subjectList.remove(subject);

					}
				});

			}

		});

		panel.add(btnUpdate);
		panel.add(btnRemove);

		table.setWidget(index, COL_OPERATION, panel);
		table.setText(index, COL_ID, id);
		table.setText(index, COL_SUBJECT, subject);
		table.setText(index, COL_DETAIL, detail);
		table.setText(index, COL_PROGRESS, progress);
		if (progress.compareTo("100%") == 0	&& table.getText(index, COL_TIME).length() == 0) {
			table.setText(index, COL_TIME, date);
		}

	}
}</code>
Well done，来运行一下看效果吧。点击Add弹出对话框，填入新的idea，这样在table中就出现了这个idea，同时，会把idea插入服务器端的数据库。重新刷新一下界面，会再次从数据库读取信息，显示在table中。
演示地址 ：<a title="Kyle Wu Idea" href="http://kylewuidea.appspot.com" target="_blank">http://kylewuidea.appspot.com</a>
<p style="text-align: center;"><img class="aligncenter" title="Kyle Wu Idea" src="http://farm4.static.flickr.com/3548/3465334900_5fb4c6e66e.jpg" alt="" width="500" height="244" /></p>

<h2>总结</h2>
好了，就写到这里了，稍微回顾一下，在熟悉了Google Web Toolkit 和 Google App Engine 后，我们先制作了界面，然后实现了服务器端的数据存储，今天把前后台结合起来。难度很低，因为是一个入门教程，也是自我学习的一个记录。还有很多东西没有去实现，比如现在任何人都可以Add Idea ( 这个其实只要在server端判断一下user就可以了 )，对重复的idea没有进行检查，样式上几乎没做任何操作......
希望诸位同学多多指导，大家都来做些好的应用。
