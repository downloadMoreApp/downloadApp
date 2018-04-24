使用步骤：
======

在项目根目录的build.gradle中使用如下代码：
------

    allprojects {
        repositories {
            maven {
                url "https://github.com/downloadMoreApp/downloadApp/raw/master"
            }
        }
    }


在app目录下的build.gradle添加如下代码：
-------------

    dependencies {
        compile 'com.zh.download:version:1.0.0' exclude group: 'com.android.support'
    }


使用示例：
-----------------
    new DownLoadUtils.Builder(MainActivity.this)
                 .setApkName("123.apk")//apk名字
                 .setUpdateUrl("http://imtt.dd.qq.com/16891/C03D2C1DA1C6015287F1FE1F2D2DAAD1.apk?fsname=com.tencent.mobileqq_7.5.8_818.apk&csr=1bbd")//下载地址
                 .setBreakpoint(false)//是否断点续下，默认 false
                 .setBecomeSilent(true)//是否静默下载,默认 false
                 .setWifiUpdate(true)//是否wifi下载，默认true
                 .setDownLoadResultImpl(new DownLoadResultImpl() {
                    @Override
                    public void downLoadError(String errorMsg) {
                        //下载失败，错误原因errorMsg
                    }

                    @Override
                    public void downLoading(float fraction) {
                        //下载中，进度fraction，进度由0.0～1.0 例如：0.5
                    }

                    @Override
                    public void downLoadComplete(String apkFilePath) {
                        //apkFilePath 下载的apk保存的本地地址
                        //下载完成，自己处理
                        EquipmentInfUtils.installApk(MainActivity.this, apkFilePath);//安装apk
                    }
                }).build();
