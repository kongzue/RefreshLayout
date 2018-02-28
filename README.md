# RefreshLayout
基于SwipeRefreshLayout的改良版

原版为 @zhangtian6691844 的《实现滑动到底部时上拉加载更多的功能的listview》：http://blog.csdn.net/zhangtian6691844/article/details/52346160

但其存在Bug，例如：
“是否是上拉操作”方法应：
```
return (mYDown - mLastY) >= mTouchSlop;
```
改为：
```
return mLastY == 0 ? false : (mYDown - mLastY) >= mTouchSlop;
```
另外，上拉加载和下拉刷新也没有互斥，将其loadData()方法判断条件由：
```
if (mOnLoadListener != null)
```
改为
```
if (mOnLoadListener != null && !isLoading && !isRefreshing()) 
```
以增加其在下拉刷新的过程中不能再上拉加载操作的互斥条件。


使用Demo：
```
        <com.kongzue.example.view.RefreshLayout
            android:id="@+id/refreshLayout"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <ListView
                android:id="@+id/list"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:paddingVertical="15dp"
                android:paddingHorizontal="10dp"
                android:clipToPadding="false"></ListView>

        </com.paac.driver.view.RefreshLayout>
```
