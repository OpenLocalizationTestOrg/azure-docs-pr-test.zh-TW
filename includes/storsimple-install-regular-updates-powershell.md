<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b24e5-101">透過 Windows PowerShell for StorSimple 安裝一般更新</span><span class="sxs-lookup"><span data-stu-id="b24e5-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b24e5-102">開啟裝置序列主控台，然後選取選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="b24e5-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b24e5-103">輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="b24e5-103">Type the password.</span></span> <span data-ttu-id="b24e5-104">預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="b24e5-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="b24e5-105">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="b24e5-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="b24e5-106">系統將通知您是否有可用的更新，以及更新是否為破壞性或非破壞性更新。</span><span class="sxs-lookup"><span data-stu-id="b24e5-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="b24e5-107">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="b24e5-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="b24e5-108">更新程序將隨即開始。</span><span class="sxs-lookup"><span data-stu-id="b24e5-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b24e5-109">這個命令只適用於一般更新。</span><span class="sxs-lookup"><span data-stu-id="b24e5-109">This command applies only to regular updates.</span></span> <span data-ttu-id="b24e5-110">您只需在某一個控制站上執行此命令，就會更新這兩個控制站。</span><span class="sxs-lookup"><span data-stu-id="b24e5-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="b24e5-111">您可能在更新程序期間注意到控制站容錯移轉。不過，容錯移轉並不會影響系統的可用性或運作。</span><span class="sxs-lookup"><span data-stu-id="b24e5-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

