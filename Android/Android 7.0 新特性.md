Android 7.0的新特性

1. 分屏多任务
   在API24中可以使用 android:resizeableActivity="true"，来开启分屏支持，
   这个时候layout标签有几个属性需要配置：
       这个layout标签的属性意义：
       1.android:defaultHeight 配置多窗口模式下默认的高度。
       2.android:defaultWidth 配置多窗口模式下默认的宽度。
       3.android:gravity 配置activityde 初始位置
       4.android:minimalHeight 最小高度
       5.android:minimalWidth 最小宽度
     此时Activity中有了一个新的生命周期回调：onMultiWindowModeChanged。
   而isInMultiWindowMode()可以判断当前是否是分屏模式。
2. 新的通知栏与Notification
   捆绑通知：也就是同意应用的多条Notification信息,合并成一条
   快速回复：类似短信等应用，可以直接在下拉通知栏进行回复
3. Data Server 功能
4. Doze 优化
5. 画中画模式
6. 跨Activity拖拽（内容）
   注意设置DRAG_FLAG_GLOBAL标示
       public boolean onLongClick(View view){  
                       ClipData data = ClipData.newPlainText(view.getClass().getName(),((Button)view).getText());  
                       View.DragShadowBuilder builder = new View.DragshadowBuilder(view);  
                       view.startDragAndDrop(data,builder,view,View.DRAG_FLAG_GLOBAL);  
                       return true;  
                }  
       findViewById(R.id.container).setOnDragListener(new View.OnDragListener(){  
          @Override  
              public boolean onDrag(View view,DragEvent dragEvent){  
                 switch(DragEvent getAction()){  
                 case DragEnent ACTION_DROP:  
                     ClipData.Item item = dragEvent.getClipData().getItemAt(0);  
                     content.setText(item.getText());  
                     break;  
                 return true;  
          }  
7. 夜间模式
8. 增强JAVA8的支持
9. Unicode 9支持和全新的emoji表情符号
10. 应用下载在下拉通知栏增加取消按钮
11. 原生支持自定义锁屏壁纸
12. Instant Apps 无需下载就可以使用的应用
13. Daydream VR支持
14. 调整尺寸（屏幕DPI）
15. 正式支持Vulkan API
16. 屏幕RGB调节
    
    
