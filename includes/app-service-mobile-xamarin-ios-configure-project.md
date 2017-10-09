#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="14f90-101">在 Xamarin Studio 中設定 hello iOS 專案</span><span class="sxs-lookup"><span data-stu-id="14f90-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="14f90-102">在 Xamarin.Studio，開啟**Info.plist**，並更新 hello**配套識別碼**以 hello 配套識別碼您先前建立並提供新的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="14f90-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="14f90-103">向下捲動太**背景模式**。</span><span class="sxs-lookup"><span data-stu-id="14f90-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="14f90-104">選取 hello**啟用背景模式**方塊和 hello**遠端通知**方塊。</span><span class="sxs-lookup"><span data-stu-id="14f90-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="14f90-105">按兩下您的專案中 hello 方案面板 tooopen**專案選項**。</span><span class="sxs-lookup"><span data-stu-id="14f90-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="14f90-106">在下**建置**，選擇**iOS 套件組合簽署**，並選取 hello 對應身分識別和佈建設定檔只需要設定此專案。</span><span class="sxs-lookup"><span data-stu-id="14f90-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="14f90-107">這可確保該 hello 專案會使用 hello 新設定檔的程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="14f90-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="14f90-108">Hello 官方 Xamarin 裝置佈建文件，請參閱[Xamarin 裝置佈建]。</span><span class="sxs-lookup"><span data-stu-id="14f90-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="14f90-109">設定 Visual Studio 中的 hello iOS 專案</span><span class="sxs-lookup"><span data-stu-id="14f90-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="14f90-110">在 Visual Studio 中，hello 專案上按一下滑鼠右鍵，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="14f90-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="14f90-111">在 hello 屬性頁中，按一下 hello **iOS 應用程式**索引標籤，然後更新 hello**識別碼**您稍早建立的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="14f90-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="14f90-112">在 hello **iOS 套件組合簽署**索引標籤上，選取 hello 對應身分識別和佈建設定檔，您剛才設定註冊這個專案。</span><span class="sxs-lookup"><span data-stu-id="14f90-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="14f90-113">這可確保該 hello 專案會使用 hello 新設定檔的程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="14f90-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="14f90-114">Hello 官方 Xamarin 裝置佈建文件，請參閱[Xamarin 裝置佈建]。</span><span class="sxs-lookup"><span data-stu-id="14f90-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="14f90-115">按兩下 Info.plist tooopen，並再啟用**RemoteNotifications**下**背景模式**。</span><span class="sxs-lookup"><span data-stu-id="14f90-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin 裝置佈建]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
