#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="ed9ab-101">toostop 並啟動虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="ed9ab-101">toostop and start a virtual device</span></span>
<span data-ttu-id="ed9ab-102">toostop 是虛擬裝置，請按一下其名稱，然後按一下**關機**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="ed9ab-103">Hello 虛擬裝置正在關機而關閉，其狀態即**停止**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="ed9ab-104">停止 hello 虛擬裝置之後，其狀態是**已停止**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="ed9ab-105">使用下列 cmdlet toostop hello 和啟動虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="ed9ab-106">toorestart 虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="ed9ab-106">toorestart a virtual device</span></span>
<span data-ttu-id="ed9ab-107">虛擬裝置正在執行，而且您想 toorestart 時，按一下其名稱，然後按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="ed9ab-108">Hello 虛擬裝置重新啟動時，其狀態即**正在重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="ed9ab-109">Hello 虛擬裝置就緒可供您 toouse 時，其狀態會是**執行**。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="ed9ab-110">使用下列 cmdlet toorestart 虛擬裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="ed9ab-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

