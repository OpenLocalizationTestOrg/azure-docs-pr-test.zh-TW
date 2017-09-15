1. <span data-ttu-id="0957b-101">按一下 Android Studio 工具列上的圖示以開啟 Android SDK Manager，或按一下工能表上的 [工具]  ->  [Android]  ->  [SDK Manager]。</span><span class="sxs-lookup"><span data-stu-id="0957b-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="0957b-102">尋找專案中使用之 Android SDK 的目標版本，請按一下[顯示套件詳細資料] 來開啟該版本，然後選擇 Google API \(如果尚未安裝的話)。</span><span class="sxs-lookup"><span data-stu-id="0957b-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="0957b-103">按一下 [SDK 工具] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0957b-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="0957b-104">如果您尚未安裝 Google Play 服務，按一下 [Google Play 服務]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0957b-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="0957b-105">然後按一下 [套用] 來安裝。</span><span class="sxs-lookup"><span data-stu-id="0957b-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="0957b-106">請注意在稍後步驟中使用的 SDK 路徑。</span><span class="sxs-lookup"><span data-stu-id="0957b-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="0957b-107">開啟應用程式目錄中的 **build.gradle** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0957b-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="0957b-108">新增此行至 *相依項目*下方：</span><span class="sxs-lookup"><span data-stu-id="0957b-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="0957b-109">按一下工具列中的 [ **同步處理專案與 Gradle 檔案** ] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0957b-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="0957b-110">開啟 **AndroidManifest.xml** 並將此標記新增至「應用程式」標記。</span><span class="sxs-lookup"><span data-stu-id="0957b-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

