
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="92834-101">更新資訊清單檔案 tooenable 通知</span><span class="sxs-lookup"><span data-stu-id="92834-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="92834-102">將下列 hello 應用程式內訊息資源複製到您 Manifest.xml 之間 hello`<application>`和`</application>`標記。</span><span class="sxs-lookup"><span data-stu-id="92834-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="92834-103">指定通知的圖示</span><span class="sxs-lookup"><span data-stu-id="92834-103">Specify an icon for notifications</span></span>
<span data-ttu-id="92834-104">下列 XML 程式碼片段中您 Manifest.xml hello 之間貼上 hello`<application>`和`</application>`標記。</span><span class="sxs-lookup"><span data-stu-id="92834-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="92834-105">這會定義顯示在系統和應用程式內通知的 hello 圖示。</span><span class="sxs-lookup"><span data-stu-id="92834-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="92834-106">這是 App 內通知的選用功能，但對系統通知是必要功能。</span><span class="sxs-lookup"><span data-stu-id="92834-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="92834-107">Android 將會拒絕具有無效圖示的系統通知。</span><span class="sxs-lookup"><span data-stu-id="92834-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="92834-108">請確定您使用的圖示會存在其中一種 hello **drawable**資料夾 (例如``engagement_close.png``)。</span><span class="sxs-lookup"><span data-stu-id="92834-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="92834-109">**Mipmap** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="92834-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="92834-110">您不應該使用 hello**啟動器**圖示。</span><span class="sxs-lookup"><span data-stu-id="92834-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="92834-111">它具有不同的解析度，通常在 hello mipmap 資料夾中，我們不支援的。</span><span class="sxs-lookup"><span data-stu-id="92834-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="92834-112">對於真正的應用程式，您可以根據 [Android 設計指導方針](http://developer.android.com/design/patterns/notifications.html)使用適合通知功能的圖示。</span><span class="sxs-lookup"><span data-stu-id="92834-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="92834-113">toobe 確定 toouse 正確圖示的解析度上，您可以查看[這些範例](https://www.google.com/design/icons)。</span><span class="sxs-lookup"><span data-stu-id="92834-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="92834-114">捲動 toohello**通知**區段中，按一下圖示，然後再按一下`PNGS`toodownload hello 圖示 drawable 集。</span><span class="sxs-lookup"><span data-stu-id="92834-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="92834-115">您可以查看與每個版本的 hello 圖示的解析度 toouse drawable 資料夾。</span><span class="sxs-lookup"><span data-stu-id="92834-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="92834-116">啟用您應用程式 tooreceive GCM 推播通知</span><span class="sxs-lookup"><span data-stu-id="92834-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="92834-117">Hello 下列貼入您 Manifest.xml 之間 hello`<application>`和`</application>`標記取代 hello 後的**寄件者識別碼**取自 Firebase 專案主控台。</span><span class="sxs-lookup"><span data-stu-id="92834-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="92834-118">hello \n 是刻意設計以確定您結束 hello 專案與其數字。</span><span class="sxs-lookup"><span data-stu-id="92834-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="92834-119">Hello 下列的程式碼貼入您 Manifest.xml 之間 hello`<application>`和`</application>`標記。</span><span class="sxs-lookup"><span data-stu-id="92834-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="92834-120">取代 hello 封裝名稱<Your package name>。</span><span class="sxs-lookup"><span data-stu-id="92834-120">Replace hello package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="92834-121">新增 hello 最後一組權限之前 hello 反白顯示`<application>`標記。</span><span class="sxs-lookup"><span data-stu-id="92834-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="92834-122">取代`<Your package name>`依您的應用程式的 hello 實際封裝名稱。</span><span class="sxs-lookup"><span data-stu-id="92834-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

