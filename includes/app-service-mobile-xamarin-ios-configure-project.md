#### <a name="configure-the-ios-project-in-xamarin-studio"></a><span data-ttu-id="a0844-101">在 Xamarin Studio 中設定 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="a0844-101">Configure the iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="a0844-102">在 Xamarin.Studio 中，開啟 **Info.plist**，然後使用您稍早以新應用程式識別碼建立的套件組合識別碼，來更新 [套件組合識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a0844-102">In Xamarin.Studio, open **Info.plist**, and update the **Bundle Identifier** with the bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="a0844-103">向下捲動到 [背景模式]。</span><span class="sxs-lookup"><span data-stu-id="a0844-103">Scroll down to **Background Modes**.</span></span> <span data-ttu-id="a0844-104">選取 [啟用背景模式] 方塊與 **[遠端通知]** 方塊。</span><span class="sxs-lookup"><span data-stu-id="a0844-104">Select the **Enable Background Modes** box and the **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="a0844-105">按兩下 [方案面板] 中的專案，以開啟 [專案選項]。</span><span class="sxs-lookup"><span data-stu-id="a0844-105">Double-click your project in the Solution Panel to open **Project Options**.</span></span>
4. <span data-ttu-id="a0844-106">選擇 [建置] 下的 [iOS 套件組合簽署]，然後選取對應的身分識別以及您為此專案設定的 [佈建設定檔]。</span><span class="sxs-lookup"><span data-stu-id="a0844-106">Under **Build**, choose **iOS Bundle Signing**, and select the corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="a0844-107">這將確保專案使用新的設定檔進行程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="a0844-107">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="a0844-108">如需官方 Xamarin 裝置佈建文件，請參閱 [Xamarin 裝置佈建]。</span><span class="sxs-lookup"><span data-stu-id="a0844-108">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-the-ios-project-in-visual-studio"></a><span data-ttu-id="a0844-109">在 Visual Studio 中設定 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="a0844-109">Configure the iOS project in Visual Studio</span></span>
1. <span data-ttu-id="a0844-110">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="a0844-110">In Visual Studio, right-click the project, and then click **Properties**.</span></span>
2. <span data-ttu-id="a0844-111">在 [屬性] 頁面中，按一下 [iOS 應用程式] 索引標籤，然後使用您稍早建立的識別碼更新 [識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a0844-111">In the properties pages, click the **iOS Application** tab, and update the **Identifier** with the ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="a0844-112">在 [iOS 套件組合簽署] 索引標籤中，選取對應的身分識別以及您為此專案設定的佈建設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0844-112">In the **iOS Bundle Signing** tab, select the corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="a0844-113">這將確保專案使用新的設定檔進行程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="a0844-113">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="a0844-114">如需官方 Xamarin 裝置佈建文件，請參閱 [Xamarin 裝置佈建]。</span><span class="sxs-lookup"><span data-stu-id="a0844-114">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="a0844-115">按兩下 Info.plist 以開啟，並啟用 [背景模式] 下的 **RemoteNotifications**。</span><span class="sxs-lookup"><span data-stu-id="a0844-115">Double-click Info.plist to open it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

<span data-ttu-id="a0844-116">[Xamarin 裝置佈建]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span><span class="sxs-lookup"><span data-stu-id="a0844-116">[Xamarin Device Provisioning]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span></span>
