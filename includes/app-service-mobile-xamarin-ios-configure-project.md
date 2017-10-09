#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>在 Xamarin Studio 中設定 hello iOS 專案
1. 在 Xamarin.Studio，開啟**Info.plist**，並更新 hello**配套識別碼**以 hello 配套識別碼您先前建立並提供新的應用程式識別碼。

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. 向下捲動太**背景模式**。 選取 hello**啟用背景模式**方塊和 hello**遠端通知**方塊。

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. 按兩下您的專案中 hello 方案面板 tooopen**專案選項**。
4. 在下**建置**，選擇**iOS 套件組合簽署**，並選取 hello 對應身分識別和佈建設定檔只需要設定此專案。

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   這可確保該 hello 專案會使用 hello 新設定檔的程式碼簽署。 Hello 官方 Xamarin 裝置佈建文件，請參閱[Xamarin 裝置佈建]。

#### <a name="configure-hello-ios-project-in-visual-studio"></a>設定 Visual Studio 中的 hello iOS 專案
1. 在 Visual Studio 中，hello 專案上按一下滑鼠右鍵，然後按一下**屬性**。
2. 在 hello 屬性頁中，按一下 hello **iOS 應用程式**索引標籤，然後更新 hello**識別碼**您稍早建立的 hello 識別碼。

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. 在 hello **iOS 套件組合簽署**索引標籤上，選取 hello 對應身分識別和佈建設定檔，您剛才設定註冊這個專案。

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    這可確保該 hello 專案會使用 hello 新設定檔的程式碼簽署。 Hello 官方 Xamarin 裝置佈建文件，請參閱[Xamarin 裝置佈建]。
4. 按兩下 Info.plist tooopen，並再啟用**RemoteNotifications**下**背景模式**。

[Xamarin 裝置佈建]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
