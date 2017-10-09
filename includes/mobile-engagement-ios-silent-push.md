> [!IMPORTANT]
> <span data-ttu-id="27871-101">tooreceive 從 Mobile Engagement 的推播通知，您需要 tooenable`Silent Remote Notifications`應用程式中。</span><span class="sxs-lookup"><span data-stu-id="27871-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="27871-102">您需要 tooadd hello 遠端通知值 toohello UIBackgroundModes 陣列 Info.plist 檔案中。</span><span class="sxs-lookup"><span data-stu-id="27871-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="27871-103">開啟`info.plist`hello 專案中的檔案</span><span class="sxs-lookup"><span data-stu-id="27871-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="27871-104">以滑鼠右鍵按一下 hello hello 清單中的最上層項目 (`Information Property List`) 並加入新的資料列</span><span class="sxs-lookup"><span data-stu-id="27871-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="27871-105">在 hello 輸入新的資料列`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="27871-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="27871-106">按一下 hello 向左箭號 tooexpand hello 資料列</span><span class="sxs-lookup"><span data-stu-id="27871-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="27871-107">新增下列值 toohello 項目 0 的 hello`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="27871-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="27871-108">一旦您進行變更的 hello，XML 應該包含下列 hello hello info.plist 索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="27871-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="27871-109">如果您使用 **Xcode 7 +** 和 **iOS 9 +**：</span><span class="sxs-lookup"><span data-stu-id="27871-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="27871-110">在 [目標] > [目標名稱] > [功能]，啟用 [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="27871-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

