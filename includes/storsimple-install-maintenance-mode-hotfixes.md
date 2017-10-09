<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="3ba7a-101">tooinstall 透過 Windows PowerShell for StorSimple 的維護模式 hotfix</span><span class="sxs-lookup"><span data-stu-id="3ba7a-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ba7a-102">在維護模式中，您在一個控制器上第一次需要 tooapply hello hotfix，然後在 hello 另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="3ba7a-103">將 hello 裝置放入維護模式。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="3ba7a-104">請參閱[步驟 2： 輸入的維護模式](../articles/storsimple/storsimple-update-device.md#step2)如需有關指示 tooenter 維護模式。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="3ba7a-105">型別 tooapply hello hotfix:</span><span class="sxs-lookup"><span data-stu-id="3ba7a-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="3ba7a-106">出現提示時，提供 hello 路徑 toohello 網路共用的資料夾，其中包含 hello hotfix 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="3ba7a-107">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="3ba7a-108">型別**Y** tooproceed hello hotfix 安裝。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="3ba7a-109">之後您 hello hotfix 控制器上套用一個，登入 toohello 另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="3ba7a-110">如同 hello 先前控制站，請套用 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="3ba7a-111">套用 hello hotfixes 之後，請退出維護模式。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="3ba7a-112">如需相關指示，請參閱[步驟 4：結束維護模式](../articles/storsimple/storsimple-update-device.md#step4)。</span><span class="sxs-lookup"><span data-stu-id="3ba7a-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

