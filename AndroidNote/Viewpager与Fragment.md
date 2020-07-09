# Viewpager与Fragment的懒加载

#### 在AndroidX中，[FragmentPagerAdapter](https://developer.android.google.cn/reference/androidx/fragment/app/FragmentPagerAdapter?hl=en)与[FragmentStatePagerAdapter](https://developer.android.google.cn/reference/kotlin/androidx/fragment/app/FragmentStatePagerAdapter?hl=en)的构造函数中新增加了一个Behavior参数，用来描述fragment切换时生命周期如何发生变化

Behavior有两个值：

1. ### [BEHAVIOR_RESUME_ONLY_CURRENT_FRAGMENT](https://developer.android.google.cn/reference/androidx/fragment/app/FragmentPagerAdapter?hl=en#BEHAVIOR_RESUME_ONLY_CURRENT_FRAGMENT)

   当前显示的Fragment生命周期会调用到onResume，其他的Fragment则只会调用至onStart，此外，设置了此参数之后setUserVisibleHint方法将不再被调用

2. ### [BEHAVIOR_SET_USER_VISIBLE_HINT](https://developer.android.google.cn/reference/androidx/fragment/app/FragmentPagerAdapter?hl=en#BEHAVIOR_SET_USER_VISIBLE_HINT)

   当前显示的Fragment会调用setUserVisibleHint(true)，而被切走的Fragment则会调用setUserVisibleHint(false)，同时，所以被加载进来的fragment的生命周期函数都会被调用至onResume。这个值已经被废弃，不推荐使用

#### 带来的影响：

​	原先利用setUserVisibleHint方法来做懒加载的方法已经不推荐使用了，可以将Behavior设置为BEHAVIOR_RESUME_ONLY_CURRENT_FRAGMENT，然后在onCreate中（或者其他不会在每次切换fragment时都会被调用的函数）中做初次的数据加载，如果要每次进入页面都刷新数据，则可以在onResume中进行





