 NotePad应用功能拓展
====
## 一、实验要求
* NoteList中显示条目增加时间戳显示
* 添加笔记查询功能（根据标题查询）
## 二、项目代码分析
### 1.NoteList中显示条目增加时间戳显示
（1）在布局文件notelist_item.xml中添加一个用于显示时间戳的TextView
```java
<TextView
    android:id="@+id/text2"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:gravity="right"
    android:textAppearance="?android:attr/textAppearanceSmall"
    android:paddingLeft="5dip"
    android:textColor="#000000"

/>
```
（2）在NodeEditor.java中找到updateNode()函数，格式化修改时间字段并存入数据库
```java
Date nowTime = new Date(System.currentTimeMillis());
        SimpleDateFormat sdFormatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String retStrFormatNowDate = sdFormatter.format(nowTime);
        values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, retStrFormatNowDate);
```
(3)在NoteList.java中找到PROJECTION
```java
private static final String[] PROJECTION = new String[] {
        NotePad.Notes._ID, // 0
        NotePad.Notes.COLUMN_NAME_TITLE, // 1
        NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, //添加该元素
};
```
### 2.添加笔记查询功能（根据标题查询）
(1)在布局文件list_options_menu.xml中，添加一个SearchView,用于显示搜索图标与搜索框
```java
<item
        android:id="@+id/menu_search"
        android:actionViewClass="android.widget.SearchView"
        android:icon="@drawable/ic_search_black_24dp"
        android:showAsAction="always"
        android:title="Search" />
 ```
 （2）为SearchView配置监听器
 ```java
 SearchView searchview = (SearchView)findViewById(R.id.search_view);
 searchview.setOnQueryTextListener(NoteSearch.this);
 ```
 
