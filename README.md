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
           return Math.round(dp * (displayMetrics.xdpi / DisplayMetrics.DENSITY_DEFAULT));
       }

       public int sizeScreen(){
           return (int)((Resources.getSystem().getDisplayMetrics().widthPixels)/ Resources.getSystem().getDisplayMetrics().density);
       }
```

<br>
<br>
This is example of what im doing

```java
    private void setupTabLayout(final TabLayout tabs) {
        tabs.setTabTextColors(ContextCompat.getColor(this, R.color.md_grey_500), ContextCompat.getColor(this, R.color.white));
        tabs.setSelectedTabIndicatorColor(getResources().getColor(android.R.color.transparent));

        if (sizeScreen()<tabsize){
            tabs.setTabMode(TabLayout.MODE_SCROLLABLE);
            tabs.setTabGravity(TabLayout.GRAVITY_FILL);
        }
        else{
            tabs.setTabMode(TabLayout.MODE_FIXED);
            tabs.setTabGravity(TabLayout.GRAVITY_FILL);
        }

        // CHANGE TAB TEXT FONT
        Typeface tf = Typeface.createFromAsset(getAssets(), "fonts/knockout-htf49-liteweight.ttf");
        ViewGroup vg = (ViewGroup) tabs.getChildAt(0);
        int tabsCount = vg.getChildCount();
        for (int j = 0; j < tabsCount; j++) {
            ViewGroup vgTab = (ViewGroup) vg.getChildAt(j);

            if (j==0){
                View view = vg.getChildAt(j);
                view.setBackgroundResource(R.drawable.backgroundtabs);
            }

            if (sizeScreen()<tabsize) {
                vgTab.getLayoutParams().width = dpToPx(120);
            }

            int tabChildsCount = vgTab.getChildCount();
            for (int i = 0; i < tabChildsCount; i++) {
                View tabViewChild = vgTab.getChildAt(i);
                if (tabViewChild instanceof TextView) {
                    ((TextView) tabViewChild).setTypeface(tf);
                    ((TextView) tabViewChild).setTextSize(18);
                    ((TextView) tabViewChild).setAllCaps(true);
                    ((TextView) tabViewChild).setSingleLine(true);
                    ((TextView) tabViewChild).setEllipsize(TextUtils.TruncateAt.MARQUEE);
                    ((TextView) tabViewChild).setMarqueeRepeatLimit(100);
                    if (j==0){
                        tabViewChild.setPadding(0, 0, 0, 0);
                    }
                    else {
                        tabViewChild.setPadding(0, padding, 0, 0);
                    }
                }
            }
        }

        tabs.setOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
            ViewGroup vg = (ViewGroup) tabs.getChildAt(0);

            @Override
            public void onTabSelected(TabLayout.Tab tab) {
                ViewGroup vgTab = (ViewGroup) vg.getChildAt(tab.getPosition());
                if (tab.getPosition()==0)
                    vg.getChildAt(tab.getPosition()).setBackgroundResource(R.drawable.backgroundtabs);

                else if (tab.getPosition()==tabcount-1)
                    vg.getChildAt(tab.getPosition()).setBackgroundResource(R.drawable.backgroundtabs_last);

                else
                    vg.getChildAt(tab.getPosition()).setBackgroundResource(R.drawable.backgroundtabs_middle);

                int tabChildsCount = vgTab.getChildCount();
                for (int i = 0; i < tabChildsCount; i++) {
                    View tabViewChild = vgTab.getChildAt(i);
                    if (tabViewChild instanceof TextView) {
                        tabViewChild.setPadding(0, 0, 0, 0);
                    }
                }
                viewPager.setCurrentItem(tab.getPosition());
            }

            @Override
            public void onTabUnselected(TabLayout.Tab tab) {
                ViewGroup vgTab = (ViewGroup) vg.getChildAt(tab.getPosition());
                vg.getChildAt(tab.getPosition()).setBackgroundResource(0);
                int tabChildsCount = vgTab.getChildCount();
                for (int i = 0; i < tabChildsCount; i++) {
                    View tabViewChild = vgTab.getChildAt(i);
                    if (tabViewChild instanceof TextView) {
                        tabViewChild.setPadding(0, padding, 0, 0);
                    }
                }
            }

            @Override
            public void onTabReselected(TabLayout.Tab tab) {

            }
        });
    }
```
