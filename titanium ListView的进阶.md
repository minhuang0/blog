title: titanium ListView的进阶
date: 2015-03-16
tags: 
    - titanium

categories: 编程

---
listView的下滑加载更多和下拉刷新的做法
<!-- more -->
下面的代码是coffee写的，是从数据库备份里面复制出来的，可能有些缩进问题。
下滑动态加载的原理是重复调用listView的setMarker这个方法.
listview下滑动态加载（避免一次性加载过多，产生不必要的资源浪费）的效果：

```coffeeScript
#一开始进去填充部分数据
add_list_data= () -> 
    if remote_data != undefined
           $.section.setItems 
           push_data(remote_data.slice(0,num))
                  $.list.setMarker({sectionIndex:0, itemIndex: (num - 1)})
                  #为下拉加载更多添加事件
                  $.list.addEventListener 'marker', (e) ->
                      $.section.appendItems push_data(remote_data.slice(num,++num))
                          $.list.setMarker({sectionIndex:0, itemIndex: (num - 1) })
```

listview 下拉刷新

```
#listview下拉刷新
control = Ti.UI.createRefreshControl({
    tintColor:'red'})
    $.listview.refreshControl = control
    #$.listview为View视图listview的ID，$.section为里面的section的IDcontrol.addEventListener('refreshstart', (e) ->
      #你要做的事件
        json(Settings.server+'/interface/projects/project_details?id='+Ti.App.Properties.getObject('id'))
          Ti.API.info('refreshstart')
            ＃几秒钟后停止刷新
              setTimeout( ->
                  Ti.API.debug('Timeout')
                      #$.section.appendItems(genData())
                          control.endRefreshing()
                            , 2000))
```