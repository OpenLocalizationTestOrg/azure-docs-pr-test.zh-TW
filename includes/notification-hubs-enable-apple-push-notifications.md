

## <a name="generate-hello-certificate-signing-request-file"></a>產生 hello 憑證簽署要求檔案
hello Apple Push Notification Service (APNS) 會使用憑證 tooauthenticate 推播通知。 請遵循這些指示 toocreate hello 必要的推播憑證 toosend，接收通知。 如需這些概念的詳細資訊，請參閱 hello 官方[Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584)文件。

產生 hello 憑證簽署要求 (CSR) 檔案，它是由 Apple toogenerate 帶正負號的推播憑證。

1. 您在 Mac 上，執行 hello 金鑰鏈存取 工具。 您可以開啟從 hello**公用程式**資料夾或 hello**其他**hello 啟動平台上的資料夾。
2. 按一下 [金鑰鏈存取]，並展開 [憑證助理]，然後按一下 [從憑證授權單位要求憑證...]。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. 選取您**使用者電子郵件地址**和**一般名稱**，請確定**儲存 toodisk**已選取，然後按一下**繼續**。 保留 hello **CA 電子郵件地址**空白，因為它不是必要欄位。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. 輸入中的 hello 憑證簽署要求 (CSR) 檔案的名稱**存**，hello 中選取位置**其中**，然後按一下 **儲存**。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      這樣可以節省 hello 選取位置; hello CSR 檔案hello 預設位置是在 hello 桌面。 請記住 hello 選擇此檔案的位置。

接下來，您會註冊 Apple 應用程式、 啟用推播通知，並上傳此匯出的 CSR toocreate 推播憑證。

## <a name="register-your-app-for-push-notifications"></a>針對推播通知註冊應用程式
toobe 無法 toosend 推播通知 tooan iOS 應用程式，您必須向 Apple 以及註冊推播通知註冊您的應用程式。  

1. 如果您沒有註冊您的應用程式，請瀏覽 toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 佈建入口網站</a>hello Apple 開發人員中心上的記錄檔，以您的 Apple ID，在按一下**識別碼**，然後按一下 **應用程式識別碼**，最後按一下 hello  **+** 簽署 tooregister 新的應用程式。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. 更新 hello 下列新的應用程式的三個欄位，然後按一下**繼續**:
   
   * **名稱**： 輸入您的應用程式的描述性名稱在 hello**名稱**欄位 hello**應用程式識別碼說明**> 一節。
   * **套件組合識別碼**: hello 下**明確的應用程式識別碼**區段中，輸入**配套識別碼**hello 形式`<Organization Identifier>.<Product Name>`hello 中所述[應用程式發佈指南](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8)。 hello*組織識別碼*和*產品名稱*使用必須符合 hello 組織識別碼和建立您的 XCode 專案時要使用的產品名稱。 在下面的 hello screeshot*通知中樞*做為組織 idenitifier 和*GetStarted*作為 hello 產品名稱。 確定這符合您將使用您的 XCode 專案中的 hello 值可讓您 toouse hello 正確發行設定檔使用 XCode。 
   * **推播通知**： 核取 hello**推播通知**hello 中的選項**應用程式服務**一節。
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      這樣會產生您應用程式識別碼，並要求您 tooconfirm hello 資訊。 按一下**註冊**tooconfirm hello 新應用程式識別碼。
     
      一旦您按一下**註冊**，您會看到 hello**登錄完成**畫面上，如下所示。 按一下 [完成] 。
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. 在 hello 開發人員中心，在應用程式識別碼，找出 hello 應用程式識別碼，只需要建立，並按一下其資料列。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      按一下 hello 應用程式識別碼會顯示 hello 應用程式詳細資料。 按一下 hello**編輯**hello 底部的按鈕。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. 捲動 toohello hello 螢幕底部，然後按一下 hello**建立憑證...** hello 區段下方的按鈕**開發推入的 SSL 憑證**。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      這會顯示 hello 「 新增 iOS 憑證 」 小幫手。
   
   > [!NOTE]
   > 本教學課程使用開發憑證。 hello 註冊生產憑證時，使用相同程序。 請確定您使用 hello 相同憑證時傳送通知的類型。
   > 
   > 
3. 按一下**選擇檔案**，瀏覽 toohello 位置儲存在 hello 第一個工作中，您建立的 hello CSR 檔案的位置，然後按一下 **產生**。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Hello 入口網站建立 hello 憑證之後，請按一下 hello**下載**按鈕，然後按一下**完成**。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      此下載 hello 憑證，並儲存它 tooyour 電腦在下載資料夾中。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > 根據預設，hello 下載的檔案開發憑證的名稱為**aps_development.cer**。
   > 
   > 
5. 按兩下 hello 下載推播憑證**aps_development.cer**。
   
      這會安裝新憑證的 hello hello 鑰匙圈，如下所示：
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > 您的憑證中的 hello 名稱可能會不同，但將會加**Apple 開發 iOS 推送服務：**。
   > 
   > 
6. 在 金鑰鏈存取，以滑鼠右鍵按一下 hello 新推播憑證在 hello 中建立**憑證**類別目錄。 按一下**匯出**hello 檔案名稱、 選取 hello **.p12**格式，然後再按一下**儲存**。
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    請記下 hello 檔案名稱和 hello.p12 匯出的憑證的位置。 它將會使用的 tooenable APNS 驗證。
   
   > [!NOTE]
   > 本教學課程會建立 QuickStart.p12 檔案。 Your file name and location might be different.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>建立 hello 應用程式的佈建設定檔
1. 在 hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 佈建入口網站</a>，選取**佈建的設定檔**，選取**所有**，然後按一下hello  **+** 按鈕 toocreate 新的設定檔。 這會啟動 hello**新增 iOS Provisiong 設定檔**精靈
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. 選取**iOS 應用程式開發**下**開發**為 hello provisiong 設定檔類型，然後按**繼續**。 
3. 接下來，選取您剛才建立的 hello hello 應用程式識別碼**應用程式識別碼**下拉式清單，然後按一下**繼續**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. 在 hello**選取憑證**畫面上，選取您的一般開發憑證用於簽章的程式碼，然後按一下**繼續**。 這不是您剛才建立的 hello 推播憑證。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. 接下來，選取 hello**裝置**測試，然後按一下 toouse**繼續**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. 最後，挑選 hello 設定檔中的名稱**設定檔名稱**，按一下 **產生**。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. 建立新的佈建設定檔的 hello 時按一下 toodownload 它並安裝它在 Xcode 開發電腦上。 然後按一下 [完成]。
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
