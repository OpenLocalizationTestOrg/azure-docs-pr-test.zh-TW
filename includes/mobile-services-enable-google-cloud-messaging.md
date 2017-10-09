
1. 瀏覽 toohello [Google 雲端主控台](https://console.developers.google.com/project)，使用您的 Google 帳戶認證登入。 
2. 按一下 [建立專案]，輸入專案名稱，接著按 [建立]。 如果要求中，執行 hello SMS 驗證，並按一下**建立**一次。
   
    ![建立新專案](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     輸入新的**專案名稱**並按一下 [建立專案]。
3. 按一下 hello**公用程式及其他**按鈕，然後按一下**專案資訊**。 請記下 hello**專案編號**。 您將需要 tooset 這個值為 hello `SenderId` hello 用戶端應用程式中的變數。
   
    ![公用程式及其他資訊](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. 在 hello 專案儀表板，在**Mobile Api**，按一下**Google Cloud Messaging**，然後在 hello 下一個頁面上按一下**啟用 API**並接受服務條款 hello。 
   
    ![啟用 GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![啟用 GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. 在 hello 專案儀表板中，按一下 **認證** > **Create Credential** > **API 金鑰**。 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. 在 [建立新的金鑰] 中，按一下 [伺服器金鑰]，輸入金鑰的名稱，然後按一下 [建立]。
7. 請記下 hello **API 金鑰**值。
   
    您將使用此 API 金鑰值 tooenable Azure tooauthenticate GCM，並代表您的應用程式中傳送推播通知。

