# SDK >=4.4

### 方式1：

```java
if(Bulid.VERSION.SDK_INT>=Build.VERSION_CODES.KITKAT){
    getWindow().addFlags(WindownManger.LayoutParams.FLAG_TRANSLUCEN_STATUS);
    getWindow().addFlags(WindownManger.LayoutParams.FLAG_TRANSLUCEN_NAVIGATION);
}
```

同时布局文件中（第一个View上）需要加入两个属性

```xml
android:fitsSystemWindows="true"
android:clipToPadding="true"
```

### 方式2：

1. XML中添加隐藏的布局

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
     <!--可以自己定义好状态栏的颜色-->  
     <RelativeLayout
           android:id="@+id/status_bar"
           android:layout_width="match_parent"
           android:layout_height="1px"
           android:visibility="gone"
           >
           
       </RelativeLayout>
       
       <LinearLayout
           android:layout_width="match_parent"
           android:layout_height="match_parent">
           
       </LinearLayout>
   </LinearLayout>
   ```

2. 动态计算状态栏的高度

   ```java
   private int getStatusHeight(){
     try{
       Class<?> c  =Class.forName("com.android.internal.R$dimen");
       Object obj = c.newInstance();
       Field field = c.getField("status_bar_height");
       int height = Integer.praseInt(field.get(obj.toString()));
       return getResources().getDimensionPixelSize(height);
     }catch(Exception e){
       e.printStackTrace();
     }
     return 0;
   }
   ```

3. 代码中设置

   ```java
   protected void onCreate(@Nullable Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
     		getWindow().requestFeature(Window.FEATURE_NO_TITLE); 
           setContentView(R.layout.test);
           if(Build.VERSION.SDK_INT>=Build.VERSION_CODES.KITKAT){
               getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
               getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_NAVIGATION);
               RelativeLayout statusBar  = (RelativeLayout) findViewById(R.id.status_bar);
               ViewGroup.LayoutParams params = statusBar.getLayoutParams();
               params.height = getStatusBarHeight();
               statusBar.setLayoutParams(params);
           }
       }
   ```

# SDK >=5.0

```java
//以下效果实现的状态栏全透明的效果
protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        getWindow().requestFeature(Window.FEATURE_NO_TITLE);  
        if(VERSION.SDK_INT >= VERSION_CODES.LOLLIPOP) {  
            Window window = getWindow();  
            window.clearFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS  
                    | WindowManager.LayoutParams.FLAG_TRANSLUCENT_NAVIGATION);  
            window.getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN  
                            | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION  
                            | View.SYSTEM_UI_FLAG_LAYOUT_STABLE);  
            window.addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS);  
            window.setStatusBarColor(Color.TRANSPARENT);  //可以直接设置状态栏颜色
            window.setNavigationBarColor(Color.TRANSPARENT);   //可以直接设置导航栏颜色
        }  
  
        setContentView(R.layout.activity_main);  
    }  
```



# 其他

实现状态栏沉浸
在 `values-v19` 下的 `styles.xml` 里定义如下主题，并在 `Manifest.xml` 里将应用主题确定为这个主题即可。

```xml
<style name="AppTheme" parent="android:Theme.Holo.Light.NoActionBar">
    <item name="android:windowTranslucentStatus">true</item>
    <item name="android:windowTranslucentNavigation">false</item>
</style>
```

需要注意布局的调整，fitsSystemWindows的调整设置





### 开源工具库

[SystemBarTint](https://github.com/jgilfelt/SystemBarTint)

