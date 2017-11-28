> [!IMPORTANT]
> <span data-ttu-id="d8f08-101">若要透過 Mobile Engagement 接收推播通知，您必須在應用程式中啟用 `Silent Remote Notifications`。</span><span class="sxs-lookup"><span data-stu-id="d8f08-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="d8f08-102">您需要將遠端通知值新增到 Info.plist 檔案中的 UIBackgroundModes 陣列。</span><span class="sxs-lookup"><span data-stu-id="d8f08-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="d8f08-103">開啟專案中的 `info.plist` 檔案</span><span class="sxs-lookup"><span data-stu-id="d8f08-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="d8f08-104">以滑鼠右鍵按一下清單中最上方的項目 (`Information Property List`)，然後新增新的資料列</span><span class="sxs-lookup"><span data-stu-id="d8f08-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="d8f08-105">在新的資料列中輸入 `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="d8f08-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="d8f08-106">按一下向左鍵以展開資料列</span><span class="sxs-lookup"><span data-stu-id="d8f08-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="d8f08-107">將下列的值加入至項目 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="d8f08-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="d8f08-108">變更後，info.plist XML 應該包含下列索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="d8f08-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="d8f08-109">如果您使用 **Xcode 7 +** 和 **iOS 9 +**：</span><span class="sxs-lookup"><span data-stu-id="d8f08-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="d8f08-110">在 [目標] > [目標名稱] > [功能]，啟用 [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="d8f08-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

