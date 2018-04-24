使用步骤：
======================

在项目build.gradle中添加如下代码：
------------
    allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url "https://github.com/downloadMoreApp/downloadApp/raw/master"
        }
      }
    }


在app的build.gradle中添加如下代码：
---------------
    dependencies {
        compile 'com.zh.download:version:1.0.4' exclude group: 'com.android.support'
    }
    
    
使用用例：
---------------

      new DownLoadUtils.Builder(MainActivity.this)
                       .setApkName("123.apk")//下载apk名字
                       .setUpdateUrl("http://imtt.dd.qq.com/16891/C03D2C1DA1C6015287F1FE1F2D2DAAD1.apk?fsname=com.tencent.mobileqq_7.5.8_818.apk&csr=1bbd")//下载apk地址
                       .setBreakpoint(true)//是否断点续下；默认 false
                       .setBecomeSilent(true)//是否静默下载；默认 false
                       .setWifiUpdate(true)//是否wifi下载；默认 true
                       .setDownLoadResultImpl(new DownLoadResultImpl() {
                         @Override
                        public void downLoadError(String errorMsg) {
                            Toast.makeText(MainActivity.this,errorMsg,Toast.LENGTH_LONG).show();
                        }

                         @Override
                         public void downLoading(float fraction) {
                            Toast.makeText(MainActivity.this,"下载进度："+fraction,Toast.LENGTH_LONG).show();
                        }

                        @Override
                        public void downLoadComplete(String apkFilePath) {
                            EquipmentInfUtils.installApk(MainActivity.this, apkFilePath);
                        }
                    }).build();
