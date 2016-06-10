# Custom-Tablayout-android

![alt tag](http://s33.postimg.org/scuddsfy7/Capture1.png)
<br>
<br>
![alt tag](http://s33.postimg.org/jddnt20n3/Capture.png)
<br>
<br>
<b>Simple tablayout hack to custom text, background and etc..</b> <br>
Below is the base init to custom tab layout
```java
        Tablayout tabs = (TabLayout)findViewById(R.id.tabs);
        //cast the selected tablayout to viewgroup
        ViewGroup vg = (ViewGroup) tabs.getChildAt(0);
        //count how many tabs in tablayout
        int tabsCount = vg.getChildCount();
        //iterative each tab
        for (int j = 0; j < tabsCount; j++) {
            //Get all element in each tabs and cast to viewgroup
            ViewGroup vgTab = (ViewGroup) vg.getChildAt(j);
            //count the element in each tabs
            int tabChildsCount = vgTab.getChildCount();
            for (int i = 0; i < tabChildsCount; i++) {
                // cast to View
                View tabViewChild = vgTab.getChildAt(i);
            }
        }
```

<br>
<b>How to use</b><br>
To change the font of the tabs. Just use <i>View instanceOf TextView</i>

```java
        // using built-in tablayout function to change indicator and text color but limited
        tabs.setTabTextColors(ContextCompat.getColor(this, R.color.md_grey_500), ContextCompat.getColor(this, R.color.white));
        tabs.setSelectedTabIndicatorColor(getResources().getColor(android.R.color.transparent));
```

Custom Tabs
```java
        // init your font
        Typeface tf = Typeface.createFromAsset(getAssets(), "fonts/knockout-htf49-liteweight.ttf");
        ViewGroup vg = (ViewGroup) tabs.getChildAt(0);
        int tabsCount = vg.getChildCount();
        for (int j = 0; j < tabsCount; j++) {
            ViewGroup vgTab = (ViewGroup) vg.getChildAt(j);
            int tabChildsCount = vgTab.getChildCount();
            for (int i = 0; i < tabChildsCount; i++) {
                View tabViewChild = vgTab.getChildAt(i);
                // Get TextView Element
                if (tabViewChild instanceof TextView) {
                  // change font
                  ((TextView) tabViewChild).setTypeface(tf);
                  // change color
                  ((TextView) tabViewChild).setTextColor(getResources().getColor(R.color.white));
                  // change size
                  ((TextView) tabViewChild).setTextSize(18);
                  // change padding
                  tabViewChild.setPadding(0, 0, 0, 0);
                  //..... etc...
                }
            }
        }
```
<br>

To change background of the tabs
```java
        ViewGroup vg = (ViewGroup) tabs.getChildAt(0);
        int tabsCount = vg.getChildCount();
        for (int j = 0; j < tabsCount; j++) {
            View view = vg.getChildAt(j);
            //change drawable for each tabs
            view.setBackgroundResource(R.drawable.backgroundtabs);
          
            //if you want to diff drawable for each tabs for example tabs is 4
            //if j == 0    view.setBackgroundResource(R.drawable.backgroundtabs1);  
            //if j == 1    view.setBackgroundResource(R.drawable.backgroundtabs2);
            //if j == 2    view.setBackgroundResource(R.drawable.backgroundtabs3);
            //if j == 3    view.setBackgroundResource(R.drawable.backgroundtabs4);
            
            ViewGroup vgTab = (ViewGroup) view;
            int tabChildsCount = vgTab.getChildCount();
            for (int i = 0; i < tabChildsCount; i++) {
                View tabViewChild = vgTab.getChildAt(i);
            }
        }
```

to change background of the tablayout
```xml
        <android.support.design.widget.TabLayout
          android:layout_height="wrap_content"
          android:layout_width="match_parent"
          android:id="@+id/tabs"
          android:background="@drawable/stripetab"    <-- create stripe background like example image
          app:tabTextAppearance="@style/CustomTabStyle"/>
```
<br>
<b>NOTES</b><br>
if you want to use scrollable mode ...etc, You need to set the tabs size (i dont know why). If not, it will looks ugly
```java
       int width = 120; // width - width of tabs 
       int tabsize = 120 * tabcount; // tabcount - number of tabs
       ViewGroup vgTab = (ViewGroup) vg.getChildAt(j);
       if (sizeScreen() < tabsize) 
           vgTab.getLayoutParams().width = dpToPx(120);
       
       public int dpToPx(int dp) {
          DisplayMetrics displayMetrics = getResources().getDisplayMetrics();
          int px = Math.round(dp * (displayMetrics.xdpi / DisplayMetrics.DENSITY_DEFAULT));
          return px;
       }
```



