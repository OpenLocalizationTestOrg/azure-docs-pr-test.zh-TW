#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="88059-101">toostop 並啟動雲端應用裝置</span><span class="sxs-lookup"><span data-stu-id="88059-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="88059-102">toostop 雲端應用裝置跳 toohello VM，您的雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="88059-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="88059-103">![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="88059-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="88059-104">在 hello 命令列中，按一下**停止**。</span><span class="sxs-lookup"><span data-stu-id="88059-104">From hello command bar, click **Stop**.</span></span>

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="88059-106">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="88059-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="88059-108">當您停止 VM 時，它就會加以解除配置。</span><span class="sxs-lookup"><span data-stu-id="88059-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="88059-109">正在停止 hello 雲端應用裝置，其狀態即**Deallocating**。</span><span class="sxs-lookup"><span data-stu-id="88059-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="88059-110">停止 hello 雲端應用裝置之後，其狀態是**已停止 （取消配置）**。</span><span class="sxs-lookup"><span data-stu-id="88059-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="88059-112">一旦停止 VM，請按一下**啟動**（按鈕會變成可用） toostart hello VM。</span><span class="sxs-lookup"><span data-stu-id="88059-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="88059-113">Hello 雲端應用裝置啟動後，其狀態是**已啟動**。</span><span class="sxs-lookup"><span data-stu-id="88059-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="88059-115">使用下列 cmdlet toostop hello，並啟動雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="88059-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="88059-116">toorestart 雲端應用裝置</span><span class="sxs-lookup"><span data-stu-id="88059-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="88059-117">toorestart 雲端應用裝置跳 toohello VM，您的雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="88059-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="88059-118">在 hello 命令列中，按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="88059-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="88059-119">出現提示時，請確認 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="88059-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="88059-120">供您 toouse hello 雲端應用裝置時，其狀態會是**執行**。</span><span class="sxs-lookup"><span data-stu-id="88059-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="88059-122">使用下列 cmdlet toorestart 雲端應用裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="88059-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

