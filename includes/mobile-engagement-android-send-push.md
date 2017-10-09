
### <a name="update-manifest-file-tooenable-notifications"></a>更新資訊清單檔案 tooenable 通知
將下列 hello 應用程式內訊息資源複製到您 Manifest.xml 之間 hello`<application>`和`</application>`標記。

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a>指定通知的圖示
下列 XML 程式碼片段中您 Manifest.xml hello 之間貼上 hello`<application>`和`</application>`標記。

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

這會定義顯示在系統和應用程式內通知的 hello 圖示。 這是 App 內通知的選用功能，但對系統通知是必要功能。 Android 將會拒絕具有無效圖示的系統通知。

請確定您使用的圖示會存在其中一種 hello **drawable**資料夾 (例如``engagement_close.png``)。 **Mipmap** 資料夾。

> [!NOTE]
> 您不應該使用 hello**啟動器**圖示。 它具有不同的解析度，通常在 hello mipmap 資料夾中，我們不支援的。
> 
> 

對於真正的應用程式，您可以根據 [Android 設計指導方針](http://developer.android.com/design/patterns/notifications.html)使用適合通知功能的圖示。

> [!TIP]
> toobe 確定 toouse 正確圖示的解析度上，您可以查看[這些範例](https://www.google.com/design/icons)。
> 捲動 toohello**通知**區段中，按一下圖示，然後再按一下`PNGS`toodownload hello 圖示 drawable 集。 您可以查看與每個版本的 hello 圖示的解析度 toouse drawable 資料夾。
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>啟用您應用程式 tooreceive GCM 推播通知
1. Hello 下列貼入您 Manifest.xml 之間 hello`<application>`和`</application>`標記取代 hello 後的**寄件者識別碼**取自 Firebase 專案主控台。 hello \n 是刻意設計以確定您結束 hello 專案與其數字。
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Hello 下列的程式碼貼入您 Manifest.xml 之間 hello`<application>`和`</application>`標記。 取代 hello 封裝名稱<Your package name>。
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. 新增 hello 最後一組權限之前 hello 反白顯示`<application>`標記。 取代`<Your package name>`依您的應用程式的 hello 實際封裝名稱。
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

