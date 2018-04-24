使用步骤：
======

在项目根目录的build.gradle中使用如下代码：
------

allprojects {<br>
    repositories {<br>
        maven {<br>
            url "https://github.com/downloadMoreApp/downloadApp/raw/master"<br>
        }<br>
    }<br>
}<br>


在app目录下的build.gradle添加如下代码：
-------------

dependencies {<br>
    compile 'com.zh.download:version:1.0.0' exclude group: 'com.android.support'<br>
}<br>


使用示例：
-----------------

new DownLoadUtils.Builder(MainActivity.this)<br>
                 .setApkName("123.apk")//apk名字<br>
                 .setUpdateUrl("http://imtt.dd.qq.com/16891/C03D2C1DA1C6015287F1FE1F2D2DAAD1.apk?fsname=com.tencent.mobileqq_7.5.8_818.apk&csr=1bbd")//下载地址<br>
                 .setBreakpoint(false)//是否断点续下，默认 false<br>
                 .setBecomeSilent(true)//是否静默下载,默认 false<br>
                 .setWifiUpdate(true)//是否wifi下载，默认true<br>
                 .setDownLoadResultImpl(new DownLoadResultImpl() {<br>
                    @Override<br>
                    public void downLoadError(String errorMsg) {<br>
                        //下载失败，错误原因errorMsg<br>
                    }<br>

                    @Override
                    public void downLoading(float fraction) {
                        //下载中，进度fraction 例如：0.5
                    }

                    @Override
                    public void downLoadComplete(String apkFilePath) {
                        //apkFilePath 下载的apk保存的本地地址
                        //下载完成，自己处理
                        EquipmentInfUtils.installApk(MainActivity.this, apkFilePath);//安装apk
                    }
                }).build();
