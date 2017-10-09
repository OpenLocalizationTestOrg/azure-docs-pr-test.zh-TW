1. 開啟 hello Android SDK Manager 按一下 hello hello Android Studio 工具列上的圖示，或按一下**工具** -> **Android** -> **SDK Manager**hello 功能表上。 在您的專案中找出 hello 的 hello 使用 Android SDK 的目標版本中，依序按一下**顯示封裝詳細資料**，然後選擇  **Google APIs**，如果尚未安裝。
2. 按一下 hello **SDK 工具** 索引標籤。如果您尚未安裝 Google Play 服務，按一下 Google Play 服務，如下所示。 然後按一下 **套用**tooinstall。 
   
    請注意 hello SDK 的路徑，供稍後步驟中使用。 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. 開啟 hello **build.gradle** hello 應用程式目錄中的檔案。
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. 新增此行至 *相依項目*下方： 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. 按一下 hello **Gradle 檔案同步處理專案**hello 工具列中的圖示。
6. 開啟**AndroidManifest.xml**並加入此標記 toohello*應用程式*標記。
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

