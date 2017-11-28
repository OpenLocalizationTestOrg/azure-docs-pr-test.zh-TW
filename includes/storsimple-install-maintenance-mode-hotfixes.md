<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b1788-101">透過 Windows PowerShell for StorSimple 安裝維護模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b1788-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b1788-102">在維護模式中，您需要先在某一個控制站上套用 Hotfix，然後在另一個控制站上套用 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b1788-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span></span>
> 
> 

1. <span data-ttu-id="b1788-103">使裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="b1788-103">Place the device into Maintenance mode.</span></span> <span data-ttu-id="b1788-104">如需如何進入維護模式的相關指示，請參閱[步驟 2：進入維護模式](../articles/storsimple/storsimple-update-device.md#step2)。</span><span class="sxs-lookup"><span data-stu-id="b1788-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span></span>
2. <span data-ttu-id="b1788-105">若要套用 Hotfix，請輸入：</span><span class="sxs-lookup"><span data-stu-id="b1788-105">To apply the hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="b1788-106">出現提示時，請提供包含 Hotfix 檔案的網路共用資料夾所在路徑。</span><span class="sxs-lookup"><span data-stu-id="b1788-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
4. <span data-ttu-id="b1788-107">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="b1788-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="b1788-108">輸入 **Y** 繼續安裝 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b1788-108">Type **Y** to proceed with the hotfix installation.</span></span>
5. <span data-ttu-id="b1788-109">在某一個控制站上套用 Hotfix 之後，請登入另一個控制站。</span><span class="sxs-lookup"><span data-stu-id="b1788-109">After you have applied the hotfix on one controller, log on to the other controller.</span></span> <span data-ttu-id="b1788-110">使用您為前一個控制站所做的方式來套用 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b1788-110">Apply the hotfix as you did for the previous controller.</span></span>
6. <span data-ttu-id="b1788-111">套用 Hotfix 之後，結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="b1788-111">After the hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="b1788-112">如需相關指示，請參閱[步驟 4：結束維護模式](../articles/storsimple/storsimple-update-device.md#step4)。</span><span class="sxs-lookup"><span data-stu-id="b1788-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

