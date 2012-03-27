--- 
layout: post
title: !binary |
  R29vZ2xlIFdlYiBUb29sa2l0IOWSjCBHb29nbGUgQXBwIEVuZ2luZSDnu7zl
  kIjmlZnnqIsg55WM6Z2i56+H

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
诸位还不清楚Google Web Toolkit 和 Google App Engine是什么的同学，请移步这里，看我的综合教程 启蒙篇。
请装好Eclipse的插件，后面的程序都是以插件为准，用命令行的同学请自己注意。
<h2>创建Eclipse工程</h2>
<img class="alignnone" title="Eclipse plugin button" src="http://farm4.static.flickr.com/3304/3445125282_b4c2cde5bd_o.png" alt="" width="69" height="22" />点击最左面的小图标就开始创建新的Web应用。我这里创建了一个名为kylewuidea的Project，包设为net.kylewu.idea，我们这里要同时使用Google Web Toolkit 和 Google App Engine，所以两个都要选择支持。确认后可以看到Eclipse为我们创建好了整个Project，结构见图。

<img class="alignnone" title="New Eclipse Project" src="http://farm4.static.flickr.com/3373/3444307627_1b0ab58861_o.png" alt="" width="525" height="552" /><img class="alignnone" title="Project structure" src="http://farm4.static.flickr.com/3316/3444307657_86ab8b604b_o.png" alt="" width="305" height="420" />
<h2>Google Web Toolkit 部分</h2>
打开Kylewuidea.java，里面已经写好了一个事例程序，有兴趣的同学可以先熟悉一下。接下来删除这个文件里多余的代码，仅保留下面这些。<!--more-->
<code lang="java">package net.kylewu.idea.client;

import com.google.gwt.core.client.EntryPoint;

/**
 * Entry point classes define onModuleLoad().
 */
public class Kylewuidea implements EntryPoint {

	/**
	 * This is the entry point method.
	 */
	public void onModuleLoad() {

	}
}</code>
下面我们就要往里面填东西了，同学们来看一下页面的结构，一个表格，包括了IdeaId，Idea主题，Idea详情，Idea完成进度及完成时间，按钮，备注。最后有一个添加Idea按钮，用来加入Idea。结构清晰了，就来写代码吧。
<code lang="java">package net.kylewu.idea.client;

import com.google.gwt.core.client.EntryPoint;
import com.google.gwt.user.client.ui.Button;
import com.google.gwt.user.client.ui.DialogBox;
import com.google.gwt.user.client.ui.FlexTable;
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

	private FlexTable table = new FlexTable();

	/**
	 * This is the entry point method.
	 */
	public void onModuleLoad() {
		// Initial all items.
		init();
		// Add table to html page.
		RootPanel.get("idea").add(createBasePanel());
		// Initial table.
		importFromDatabase();
	}

	private void init() {
		// TODO Initial table structure.
		// TODO Set table attribute.
	}
	private void importFromDatabase() {
		// TODO Add initial data to table or get from database.

	}
	private Panel createBasePanel() {
		// Base Panel of this project.
		VerticalPanel mainPanel = new VerticalPanel();
		// TODO Add click handler to add button.
		// TODO Assemble the panel.

		return mainPanel;
	}
}</code>
onModuleLoad()方法就是程序的入口，这里我们写了一下初始化的代码。我在这里是直接写成方法了，这样看入口感觉清爽一些。

写Google Web Toolkit的代码与写普通Java界面很相似，在Panel里加入一些组件。这里要注意，RootPanel.get()方法得到的就是HTML页面中的某个元素，也就是我们的最上级容器。在这里我get名为idea的panel，那么它到底在什么地方呢？

打开war/Kylewuidea.html，删除body内除iframe的所有内容，改为如下代码。
<code lang="html">
<h1>Kyle Wu's Idea</h1>
</code>
看到了么，我们将一个div命名为idea，这样我们Project都会在这个div标签下，当然，你也可以get到其他的元素。

到这里页面中还没有任何元素，下面任务很简单了。点击添加Idea的按钮，弹出一个对话框，可以填入主题和详情等。当我们点击添加Idea的时候，一条新的Idea将显示在表格中。对于每条idea，都需要更新或者删除，功能应该不难了吧，同学们可以自己写写看。

Google Web Toolkit 的任务差不多了，让我们看看最后的代码。
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

				insertIdeaIntoTable(index, "", txtBoxSubject.getText(), txtAreaDetail.getText(),
						mapIntToStr.get(listBox.getSelectedIndex()), "");
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
				// Remove

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
好奇的同学肯定会问，光写Google Web Toolkit 的东西了，怎么不见Google App Engine 呢？呵呵，不要着急，休息，休息一下：） 在下一篇里将介绍Google App Engine 在我们这个应用里如何帮助诸位同学把idea存储起来。
