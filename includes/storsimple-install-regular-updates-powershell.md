<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b457f-101">透過 Windows PowerShell for StorSimple tooinstall 定期更新</span><span class="sxs-lookup"><span data-stu-id="b457f-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b457f-102">開啟 hello 裝置序列主控台，然後選取選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="b457f-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b457f-103">型別 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b457f-103">Type hello password.</span></span> <span data-ttu-id="b457f-104">hello 預設密碼為*Password1*。</span><span class="sxs-lookup"><span data-stu-id="b457f-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="b457f-105">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="b457f-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="b457f-106">如果有可用更新時，是否 hello 更新具有干擾性或非干擾性，將會通知您。</span><span class="sxs-lookup"><span data-stu-id="b457f-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="b457f-107">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="b457f-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="b457f-108">hello 更新程序將會啟動。</span><span class="sxs-lookup"><span data-stu-id="b457f-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b457f-109">此命令只會套用 tooregular 更新。</span><span class="sxs-lookup"><span data-stu-id="b457f-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="b457f-110">您只需在某一個控制站上執行此命令，就會更新這兩個控制站。</span><span class="sxs-lookup"><span data-stu-id="b457f-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="b457f-111">您可能會發現控制器容錯移轉期間 hello 更新程序。不過，hello 容錯移轉不會影響系統可用性或運作。</span><span class="sxs-lookup"><span data-stu-id="b457f-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

