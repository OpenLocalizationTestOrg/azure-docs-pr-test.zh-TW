<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="62303-101">透過 Windows PowerShell for StorSimple tooinstall 定期 hotfix</span><span class="sxs-lookup"><span data-stu-id="62303-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="62303-102">Toohello 裝置序列主控台連線。</span><span class="sxs-lookup"><span data-stu-id="62303-102">Connect toohello device serial console.</span></span> <span data-ttu-id="62303-103">如需詳細資訊，請參閱[步驟 1: toohello 序列主控台連接](../articles/storsimple/storsimple-update-device.md#step1)。</span><span class="sxs-lookup"><span data-stu-id="62303-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="62303-104">在 hello 序列主控台功能表中，選取選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="62303-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="62303-105">型別 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="62303-105">Type hello password.</span></span> <span data-ttu-id="62303-106">hello 預設密碼為**Password1**。</span><span class="sxs-lookup"><span data-stu-id="62303-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="62303-107">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="62303-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="62303-108">此命令適用於僅 tooregular hotfix。</span><span class="sxs-lookup"><span data-stu-id="62303-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="62303-109">您只需在某一個控制站上執行此命令，就會更新這兩個控制站。</span><span class="sxs-lookup"><span data-stu-id="62303-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="62303-110">您可能會發現控制器容錯移轉期間 hello 更新程序。不過，hello 容錯移轉不會影響系統可用性或運作。</span><span class="sxs-lookup"><span data-stu-id="62303-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="62303-111">出現提示時，提供 hello 路徑 toohello 網路共用的資料夾，其中包含 hello hotfix 檔案。</span><span class="sxs-lookup"><span data-stu-id="62303-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="62303-112">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="62303-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="62303-113">型別**Y** tooproceed hello hotfix 安裝。</span><span class="sxs-lookup"><span data-stu-id="62303-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

