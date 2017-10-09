1. <span data-ttu-id="03be6-101">開啟 hello Android SDK Manager 按一下 hello hello Android Studio 工具列上的圖示，或按一下**工具** -> **Android** -> **SDK Manager**hello 功能表上。</span><span class="sxs-lookup"><span data-stu-id="03be6-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="03be6-102">在您的專案中找出 hello 的 hello 使用 Android SDK 的目標版本中，依序按一下**顯示封裝詳細資料**，然後選擇  **Google APIs**，如果尚未安裝。</span><span class="sxs-lookup"><span data-stu-id="03be6-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="03be6-103">按一下 hello **SDK 工具** 索引標籤。如果您尚未安裝 Google Play 服務，按一下 Google Play 服務，如下所示。</span><span class="sxs-lookup"><span data-stu-id="03be6-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="03be6-104">然後按一下 **套用**tooinstall。</span><span class="sxs-lookup"><span data-stu-id="03be6-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="03be6-105">請注意 hello SDK 的路徑，供稍後步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="03be6-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="03be6-106">開啟 hello **build.gradle** hello 應用程式目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="03be6-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="03be6-107">新增此行至 *相依項目*下方：</span><span class="sxs-lookup"><span data-stu-id="03be6-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="03be6-108">按一下 hello **Gradle 檔案同步處理專案**hello 工具列中的圖示。</span><span class="sxs-lookup"><span data-stu-id="03be6-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="03be6-109">開啟**AndroidManifest.xml**並加入此標記 toohello*應用程式*標記。</span><span class="sxs-lookup"><span data-stu-id="03be6-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

