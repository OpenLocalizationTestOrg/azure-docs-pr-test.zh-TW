
1. <span data-ttu-id="555d2-101">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [瀏覽全部] > [應用程式服務]，再按一下 [Mobile Apps 後端]。</span><span class="sxs-lookup"><span data-stu-id="555d2-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and then click your Mobile Apps back end.</span></span> <span data-ttu-id="555d2-102">在 [設定] 中，按一下 [App Service 推播]，然後按一下通知中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="555d2-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="555d2-103">移至 **Google (GCM)**，輸入在先前程序中透過 Firebase 取得的**伺服器金鑰**值，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="555d2-103">Go to **Google (GCM)**, enter the **Server Key** value that you obtained from Firebase in the previous procedure, and then click **Save**.</span></span>

    ![在入口網站中設定 GCM API 金鑰](./media/app-service-mobile-android-configure-push/mobile-push-api-key.png)

<span data-ttu-id="555d2-105">Mobile Apps 後端現已設定成使用 Firebase 雲端通訊。</span><span class="sxs-lookup"><span data-stu-id="555d2-105">The Mobile Apps back end is now configured to use Firebase Cloud Messaging.</span></span> <span data-ttu-id="555d2-106">這個設定可讓您透過通知中樞，將推播通知傳送到在 Android 裝置上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="555d2-106">This enables you to send push notifications to your app running on an Android device, by using the notification hub.</span></span>

<!-- URLs. -->


<!-- images -->
