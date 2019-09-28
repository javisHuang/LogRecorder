# LogRecorder
Record system or application log to sdcard on Android device.

# Usage
直接複製 [LogRecorder.java](https://github.com/dxjia/LogRecorder/blob/master/LogRecorder.java) 檔到你的工程中，使用方式如下：
<br>首先在`AndroidManifest.xml`中增加許可權：
```
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_LOGS" />
```

然後在代碼中合適的地方使用，之後Log就會自動開始記錄，直到調用`logRecorder.stop()`，或者進程結束：
```
	LogRecorder logRecorder
			 = new LogRecorder.Builder(context)
	               .setLogFolderName("foldername")
	               .setLogFolderPath("/sdcard/foldername")
	               .setLogFileNameSuffix("filesuffix")
	               .setLogFileSizeLimitation(256)
	               .setLogLevel(4)
	               .setLogFileLiveDay(1)
	               .addLogFilterTag("ActivityManager")
	               .setPID(android.os.Process.myPid())
	               .build();

	logRecorder.start();
```

## setLogFolderName()
> 設定log輸出目錄名，如果該值與folder path都沒有設定的話，會默認使用應用包名在sdcard下新建目錄。

## setLogFolderPath()
> 設置Log輸出目錄絕對路徑，該值會優先使用，會忽略folder name的設置。

## setLogFileNameSuffix()
> log檔案名首碼，檔案名會使用時間的形式，該值的設定會自動追加在時間之前，如setLogFileNameSuffix("mylog") 則最後的檔案名為`mylog-2016-02-04-12-26-53.log`

## setLogFileSizeLimitation()
> 單個log檔的大小限制，超過設置的限制時，會自動新起新的檔記錄log，**`注意`**: 是以`KB`為單位的。

## setLogLevel()
> 設置記錄的log級別，預設2<br>
>   2 = verbose <br>
>   3 = debug <br>
>   4 = info <br>
>   5 = warning <br>
>   6 = error <br>
>   7 = silent(不輸出任何log)

## setLogFileLiveDay()
> 單個log檔的儲存時間，是以`天`為單位的。

## addLogFilterTag()
> 設置log過濾的tag，可以add多個，如`addLogFilterTag("ActivityManager")`表示只過濾“ActivityManager”的log 

## setPID()
> 通過該方法可以指定一個特定的進程的log，如通過`setPID(android.os.Process.myPid())` 即可只輸出自己的APP的log。
