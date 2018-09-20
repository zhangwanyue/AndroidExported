## exported activity test

#### set exported in manifest

```xml
<activity
    android:name="com.example.vera.exportedactivity.ExportedActivity"
    android:exported="true">
</activity>
```
default exported="false"

#### using adb start activity

* ExportedActivity is exported so it can be start

```shell
adb shell am start -n com.example.vera.exportedactivity/.ExportedActivity 
```

* NotExportedActivity is not exported so it can not be start

```shell
adb shell am start -n com.example.vera.exportedactivity/.NotExportedActivity
```
显示的错误结果：
```shell
java.lang.SecurityException: Permission Denial: starting Intent { flg=0x10000000 cmp=com.example.vera.exportedactivity/.NotExportedActivity } from null (pid=821, uid=2000) not exported from uid 10305
```

#### if has `applicationIdSuffix`

```groovy
debug{
    //add build config field, find in app/build/generated/source/buildConfig/debug/com/example/vera/gradlebuildconfig/BuildConfig.java
    applicationIdSuffix ".debug"
}
```

* start ExportedActivity 

```shell
adb shell am start -n com.example.vera.exportedactivity.debug/com.example.vera.exportedactivity.ExportedActivity 
```


