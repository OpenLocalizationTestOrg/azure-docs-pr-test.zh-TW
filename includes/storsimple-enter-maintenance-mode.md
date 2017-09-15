<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="c1476-101">進入維護模式</span><span class="sxs-lookup"><span data-stu-id="c1476-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="c1476-102">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="c1476-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="c1476-103">輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="c1476-103">Type the password.</span></span> <span data-ttu-id="c1476-104">預設密碼為 **Password1**。</span><span class="sxs-lookup"><span data-stu-id="c1476-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="c1476-105">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="c1476-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="c1476-106">您將會看到警告訊息，告知您維護模式將中斷所有 I/O 要求並提供與 Azure 傳統入口網站的連線，而系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="c1476-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="c1476-107">輸入 **Y** 以進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="c1476-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="c1476-108">這兩個控制站都將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c1476-108">Both controllers will restart.</span></span> <span data-ttu-id="c1476-109">完成重新啟動時，會出現另一個訊息，指出裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="c1476-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>

