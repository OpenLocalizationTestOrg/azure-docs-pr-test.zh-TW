
1. <span data-ttu-id="5fbf9-101">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [瀏覽全部] > [應用程式服務]，再按一下 [Mobile Apps 後端]。</span><span class="sxs-lookup"><span data-stu-id="5fbf9-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and click your Mobile Apps back end.</span></span> <span data-ttu-id="5fbf9-102">在 [設定] 中，按一下 [App Service 推播]，然後按一下通知中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="5fbf9-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="5fbf9-103">移至 **Windows (WNS)**，輸入您從線上服務網站取得的**安全性金鑰** (用戶端密碼) 和**套件 SID**，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5fbf9-103">Go to **Windows (WNS)**, enter the **Security key** (client secret) and **Package SID** that you obtained from the Live Services site, and then click **Save**.</span></span>

    ![在入口網站中設定 WNS 金鑰](./media/app-service-mobile-configure-wns/mobile-push-wns-credentials.png)

<span data-ttu-id="5fbf9-105">您的後端現在已設定成使用 WNS 傳送來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="5fbf9-105">Your back end is now configured to use WNS to send push notifications.</span></span>
