<span data-ttu-id="53f52-101">hello 行動應用程式功能的 Azure 應用程式服務會使用[Azure 通知中樞]toosend 推播通知，因此您要在您的行動裝置應用程式設定通知中樞。</span><span class="sxs-lookup"><span data-stu-id="53f52-101">hello Mobile Apps feature of Azure App Service uses [Azure Notification Hubs] toosend pushes, so you will be configuring a notification hub for your mobile app.</span></span>

1. <span data-ttu-id="53f52-102">在 hello [Azure 入口網站]，跳過**應用程式服務**，然後按一下應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="53f52-102">In hello [Azure portal], go too**App Services**, and then click your app back end.</span></span> <span data-ttu-id="53f52-103">在 [設定] 下方，按一下 [推送]。</span><span class="sxs-lookup"><span data-stu-id="53f52-103">Under **Settings**, click **Push**.</span></span>
2. <span data-ttu-id="53f52-104">按一下**連接**tooadd 通知中樞資源 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53f52-104">Click **Connect** tooadd a notification hub resource toohello app.</span></span> <span data-ttu-id="53f52-105">您可以建立中樞，或連接 tooan 現有的指引。</span><span class="sxs-lookup"><span data-stu-id="53f52-105">You can either create a hub or connect tooan existing one.</span></span>

    ![](./media/app-service-mobile-create-notification-hub/configure-hub-flow.png)

<span data-ttu-id="53f52-106">現在您已連接的通知中樞 tooyour 行動應用程式後端專案。</span><span class="sxs-lookup"><span data-stu-id="53f52-106">Now you have connected a notification hub tooyour Mobile Apps back-end project.</span></span> <span data-ttu-id="53f52-107">稍後您將設定此通知中樞 tooconnect tooa 平台通知系統 (PNS) toopush toodevices。</span><span class="sxs-lookup"><span data-stu-id="53f52-107">Later you will configure this notification hub tooconnect tooa platform notification system (PNS) toopush toodevices.</span></span>

[Azure 入口網站]: https://portal.azure.com/
[Azure 通知中樞]: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-push-notification-overview/
