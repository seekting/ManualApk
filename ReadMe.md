
###生成R文件
```cmd
aapt package -f -m -J E:/develop/git/ManualApk/gen ^
-S E:/develop/git/ManualApk/app/src/main/res ^
-I E:/develop/android-sdk/platforms/android-23/android.jar ^
-M E:/develop/git/ManualApk/app/src/main/AndroidManifest.xml

```




### 生成class文件
> 必需是java 1.7，android 23用的jdk1.7
```cmd
javac -target 1.7 ^
-encoding UTF-8 ^
-bootclasspath ^
E:/develop/android-sdk/platforms/android-23/android.jar -d ^
E:/develop/git/ManualApk/bin ^
E:/develop/git/ManualApk/gen/com/seekting/manualapk/*.java ^
E:/develop/git/ManualApk/app/src/main/java/com/seekting/manualapk/*.java

```
### dex命令

```cmd
dx –-dex -–output=E:/develop/git/ManualApk/output/classes.dex ^
E:/develop/git/ManualApk/bin


```

### 资源文件
```cmd
aapt package -f ^
-A E:/develop/git/ManualApk/app/assets ^
-S E:/develop/git/ManualApk/app/src/main/res ^
-I ^
E:/develop/android-sdk/platforms/android-23/android.jar ^
-M E:/develop/git/ManualApk/app/src/main/AndroidManifest.xml ^
-F E:/develop/git/ManualApk/output/debut.apk

```
### 把dex打包到apk中
> 这里会找不到apkbuilder，在tools里有apkbuilder
先把E:\develop\android-sdk\tools\lib\sdklib-25.3.2.jar copy重命名为sdklib.jar
```cmd
E:/develop/android-sdk/tools/apkbuilder.bat ^
E:/develop/git/ManualApk/output/unsigned.apk ^
-u -z E:/develop/git/ManualApk/output/debut.apk ^
-f E:/develop/git/ManualApk/output/classes.dex

```

### 签名
```cmd

jarsigner -verbose ^
-keystore E:\develop\git\ManualApk\keystore\appkey ^
-storepass zxt_yhy ^
-keypass zxt_yhy ^
E:\develop\git\ManualApk\output/unsigned.apk  seekting

```