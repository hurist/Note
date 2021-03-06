## BroadcastReceiver

### 注册方式

1. #### 静态注册，清单文件声明

2. #### 通过上下文动态注册

### 注册方式区别

静态注册的即时进程未被启动，在接收到广播之后仍然可以被启动，而动态注册的则是只有被某个上下文注册了才有可能被启动，如果api级别高于26的话，隐式注册的广播除了一些例外的隐式广播和明确针对你的APP的广播，不能使用静态注册的方式，收不到

### BroadcastReceiver对进程的影响

当广播接收器执行到onReceive方法时，它所在的进程会被视为前台进程，一般不会轻易被回收，当执行完之后，进程的状态则取决于进程内其他组件的状态了，如果这个进程只有这个receiver活跃的话，则很可能在执行完后被广播。如果你的receiver内单独开了线程执行任务，不希望系统在onReceive方法执行完后回收receiver，可以通过goAsync()方法拿到一个PendingResult对象，在任务执行完后，通过该对象的finish方法通知系统回收，不过这个任务尽量不要超过10s

### 发送广播

1. sendBroadcast() 随机顺序向所有接收器发送，无法终止，也无法在各个接收器之间传递
2. sendOrderBroadcast()  有序发送广播，顺序依据IntentFilter的priority决定，可以被优先级高的终止传递，也可以往其中添加数据继续传递
3. LocalBroadcastManager.sendBroadcast() 发送本地广播，效率更高

### 通过权限限制广播

#### 带权限的发送

在sendBroadcast中加入权限参数，可以是系统的权限，也可以是自己用<permission>标签声明的权限，接收方想要接收必须用<use-permission>请求权限才可以接收（自定义权限将在安装应用时注册。定义自定义权限的应用必须在使用自定义权限的应用之前安装。）

#### 带权限的接收

在清单文件广播接收器的声明处，用permission属性声明权限，也可以在registerRecciver方法中加入权限参数。广播发送发则必须用<use-permission>请求权限才可以向接收器发送广播

