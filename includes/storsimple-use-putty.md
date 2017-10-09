<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="db51e-101">tooconnect 透過 hello 序列主控台</span><span class="sxs-lookup"><span data-stu-id="db51e-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="db51e-102">（直接或透過 USB 序列介面卡），請將序列纜線 toohello 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="db51e-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="db51e-103">開啟 hello**控制台**，然後開啟 hello**裝置管理員**。</span><span class="sxs-lookup"><span data-stu-id="db51e-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="db51e-104">Hello 下列圖例所示，請找出 hello COM 連接埠。</span><span class="sxs-lookup"><span data-stu-id="db51e-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![透過序列主控台連接](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="db51e-106">啟動 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="db51e-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="db51e-107">Hello 右窗格中，變更 hello**連線類型**太**序列**。</span><span class="sxs-lookup"><span data-stu-id="db51e-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="db51e-108">Hello 右窗格中，輸入 hello 適當的 COM 連接埠。</span><span class="sxs-lookup"><span data-stu-id="db51e-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="db51e-109">請確定 hello 序列組態參數設定如下：</span><span class="sxs-lookup"><span data-stu-id="db51e-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="db51e-110">速度：115200</span><span class="sxs-lookup"><span data-stu-id="db51e-110">Speed: 115,200</span></span>
   * <span data-ttu-id="db51e-111">資料位元：8</span><span class="sxs-lookup"><span data-stu-id="db51e-111">Data bits: 8</span></span>
   * <span data-ttu-id="db51e-112">停止位元：1</span><span class="sxs-lookup"><span data-stu-id="db51e-112">Stop bits: 1</span></span>
   * <span data-ttu-id="db51e-113">同位檢查：無</span><span class="sxs-lookup"><span data-stu-id="db51e-113">Parity: None</span></span>
   * <span data-ttu-id="db51e-114">流量控制：無</span><span class="sxs-lookup"><span data-stu-id="db51e-114">Flow control: None</span></span>
     
     <span data-ttu-id="db51e-115">Hello 下列圖例顯示這些設定。</span><span class="sxs-lookup"><span data-stu-id="db51e-115">These settings are shown in hello following illustration.</span></span>
     
     ![PuTTY 設定](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="db51e-117">如果 hello 預設流程控制設定無法運作，請嘗試設定 hello 流程控制 tooXON/XOFF。</span><span class="sxs-lookup"><span data-stu-id="db51e-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="db51e-118">按一下**開啟**toostart 序列工作階段。</span><span class="sxs-lookup"><span data-stu-id="db51e-118">Click **Open** toostart a serial session.</span></span>

