# EasyLog
Easy to use and lightweight logger for Android
print the caller [class name][method name][line number] from the StackTrace


### Usage

enable and init the logger

``` java

    EasyLog.showLogs(BuildConfig.DEBUG);
    EasyLog.setDefaultText("default");
    EasyLog.setTag("Logger");

```

examples:

``` java

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        .
        .
        .
        EasyLog.d();
        EasyLog.e(new RuntimeException("Exception example"));
        InnerClass test = new InnerClass();
        test.log();

        findViewById(R.id.main_btn).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                EasyLog.d();
            }
        });
        .
        .
        .
	}

    private class InnerClass {

        void log(){
            EasyLog.i(this);
        }

        @Override
        public String toString() {
            return "InnerClass{}";
        }
    }

```

Default log:
D/Logger: [MainActivity][onCreate()][20]=> default

Log Exception:
E/Logger: [MainActivity][onCreate()][21]=> Exception example
          java.lang.RuntimeException: Exception example
              at dev.yamin.easylog.MainActivity.onCreate(MainActivity.java:23)
              at android.app.Activity.performCreate(Activity.java:6662)
              at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1118)
              at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2599)
              at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2707)
              at android.app.ActivityThread.-wrap12(ActivityThread.java)
              at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1460)
              at android.os.Handler.dispatchMessage(Handler.java:102)
              at android.os.Looper.loop(Looper.java:154)
              at android.app.ActivityThread.main(ActivityThread.java:6077)
              at java.lang.reflect.Method.invoke(Native Method)
              at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:866)
              at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:756)

Inner Class example:
I/Logger: [MainActivity$InnerClass][log()][36]=> InnerClass{}

Anonymous Inner Class example:
D/Logger: [MainActivity$1][onClick()][28]=> default