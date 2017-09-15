<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b199e-101">透過 Windows PowerShell for StorSimple 安裝一般 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b199e-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b199e-102">連接到裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="b199e-102">Connect to the device serial console.</span></span> <span data-ttu-id="b199e-103">如需詳細資訊，請參閱[步驟 1：連接到序列主控台](../articles/storsimple/storsimple-update-device.md#step1)。</span><span class="sxs-lookup"><span data-stu-id="b199e-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="b199e-104">在序列主控台功能表中，選取選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="b199e-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b199e-105">輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="b199e-105">Type the password.</span></span> <span data-ttu-id="b199e-106">預設密碼為 **Password1**。</span><span class="sxs-lookup"><span data-stu-id="b199e-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="b199e-107">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="b199e-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="b199e-108">這個命令只適用於一般的 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b199e-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="b199e-109">您只需在某一個控制站上執行此命令，就會更新這兩個控制站。</span><span class="sxs-lookup"><span data-stu-id="b199e-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="b199e-110">您可能在更新程序期間注意到控制站容錯移轉。不過，容錯移轉並不會影響系統的可用性或運作。</span><span class="sxs-lookup"><span data-stu-id="b199e-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="b199e-111">出現提示時，請提供包含 Hotfix 檔案的網路共用資料夾所在路徑。</span><span class="sxs-lookup"><span data-stu-id="b199e-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="b199e-112">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="b199e-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="b199e-113">輸入 **Y** 繼續安裝 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b199e-113">Type **Y** to proceed with the hotfix installation.</span></span>

