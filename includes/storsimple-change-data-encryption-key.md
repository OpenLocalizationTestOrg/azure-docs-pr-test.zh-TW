<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a><span data-ttu-id="750b0-101">步驟 1： 授權裝置 toochange hello 服務資料加密金鑰在 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="750b0-101">Step 1: Authorize a device toochange hello service data encryption key in hello Azure classic portal</span></span>
<span data-ttu-id="750b0-102">一般而言，hello 裝置系統管理員會要求該 hello 服務系統管理員授權裝置 toochange 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="750b0-102">Typically, hello device administrator will request that hello service administrator authorize a device toochange service data encryption keys.</span></span> <span data-ttu-id="750b0-103">然後 hello 服務系統管理員將授權 hello 裝置 toochange hello 機碼。</span><span class="sxs-lookup"><span data-stu-id="750b0-103">hello service administrator will then authorize hello device toochange hello key.</span></span>

<span data-ttu-id="750b0-104">Hello Azure 傳統入口網站中，會執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="750b0-104">This step is performed in hello Azure classic portal.</span></span> <span data-ttu-id="750b0-105">hello 服務系統管理員可以從顯示授權的合格 toobe hello 裝置的清單中選取裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-105">hello service administrator can select a device from a displayed list of hello devices that are eligible toobe authorized.</span></span> <span data-ttu-id="750b0-106">hello 裝置處於已授權的 toostart hello 服務資料加密金鑰變更程序。</span><span class="sxs-lookup"><span data-stu-id="750b0-106">hello device is then authorized toostart hello service data encryption key change process.</span></span>

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a><span data-ttu-id="750b0-107">哪些裝置可以被授權 toochange 服務資料加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="750b0-107">Which devices can be authorized toochange service data encryption keys?</span></span>
<span data-ttu-id="750b0-108">裝置必須符合下列準則，它可以是授權的 tooinitiate 服務資料加密金鑰變更之前的 hello:</span><span class="sxs-lookup"><span data-stu-id="750b0-108">A device must meet hello following criteria before it can be authorized tooinitiate service data encryption key changes:</span></span>

* <span data-ttu-id="750b0-109">hello 裝置必須是線上 toobe 適合服務資料加密金鑰變更授權。</span><span class="sxs-lookup"><span data-stu-id="750b0-109">hello device must be online toobe eligible for service data encryption key change authorization.</span></span>
* <span data-ttu-id="750b0-110">您可以授權的 hello 相同裝置一次在 30 分鐘後如果 hello 金鑰變更未起始。</span><span class="sxs-lookup"><span data-stu-id="750b0-110">You can authorize hello same device again after 30 minutes if hello key change has not been initiated.</span></span>
* <span data-ttu-id="750b0-111">您可以授權另一個裝置，前提 hello 金鑰變更未起始 hello 先前授權的裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-111">You can authorize a different device, provided that hello key change has not been initiated by hello previously authorized device.</span></span> <span data-ttu-id="750b0-112">已獲授權 hello 新裝置之後，hello 舊裝置無法起始 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="750b0-112">After hello new device has been authorized, hello old device cannot initiate hello change.</span></span>
* <span data-ttu-id="750b0-113">Hello hello 服務資料加密金鑰變換正在進行時，您無法授權裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-113">You cannot authorize a device while hello rollover of hello service data encryption key is in progress.</span></span>
* <span data-ttu-id="750b0-114">某些 hello hello 服務中註冊的裝置已變換 hello 加密而其他裝置尚未時，您可以授權裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-114">You can authorize a device when some of hello devices registered with hello service have rolled over hello encryption while others have not.</span></span> <span data-ttu-id="750b0-115">在這種情況下，hello 合格裝置為 hello 已完成 hello 服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="750b0-115">In such cases, hello eligible devices are hello ones that have completed hello service data encryption key change.</span></span>

> [!NOTE]
> <span data-ttu-id="750b0-116">StorSimple 虛擬裝置不會顯示在 hello 可能是裝置清單中的 hello Azure 傳統入口網站，在權限 toostart hello 金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="750b0-116">In hello Azure classic portal, StorSimple virtual devices are not shown in hello list of devices that can be authorized toostart hello key change.</span></span>
> 
> 

<span data-ttu-id="750b0-117">執行下列步驟 tooselect hello，並授權裝置 tooinitiate hello 服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="750b0-117">Perform hello following steps tooselect and authorize a device tooinitiate hello service data encryption key change.</span></span>

#### <a name="tooauthorize-a-device-toochange-hello-key"></a><span data-ttu-id="750b0-118">tooauthorize 裝置 toochange hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="750b0-118">tooauthorize a device toochange hello key</span></span>
1. <span data-ttu-id="750b0-119">在 hello 服務儀表板頁面上，按一下 **變更服務資料加密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="750b0-119">On hello service dashboard page, click **Change service data encryption key**.</span></span>
   
    ![變更服務加密金鑰](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. <span data-ttu-id="750b0-121">在 hello**變更服務資料加密金鑰**對話方塊方塊中，選取並授權裝置 tooinitiate hello 服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="750b0-121">In hello **Change service data encryption key** dialog box, select and authorize a device tooinitiate hello service data encryption key change.</span></span> <span data-ttu-id="750b0-122">hello 下拉式清單具有所有可授權 hello 合格裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-122">hello drop-down list has all hello eligible devices that can be authorized.</span></span>
3. <span data-ttu-id="750b0-123">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="750b0-123">Click hello check icon</span></span> ![核取圖示](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png)<span data-ttu-id="750b0-125">.</span><span class="sxs-lookup"><span data-stu-id="750b0-125">.</span></span>

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a><span data-ttu-id="750b0-126">步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="750b0-126">Step 2: Use Windows PowerShell for StorSimple tooinitiate hello service data encryption key change</span></span>
<span data-ttu-id="750b0-127">StorSimple 介面上 hello 授權 StorSimple 裝置的 hello Windows PowerShell 會執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="750b0-127">This step is performed in hello Windows PowerShell for StorSimple interface on hello authorized StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="750b0-128">Hello 金鑰變換完成之前，可以在 hello Azure 傳統入口網站，您的 StorSimple Manager 服務中不執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="750b0-128">No operations can be performed in hello Azure classic portal of your StorSimple Manager service until hello key rollover is completed.</span></span>
> 
> 

<span data-ttu-id="750b0-129">如果您使用 hello 裝置序列主控台 tooconnect toohello Windows PowerShell 介面，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="750b0-129">If you are using hello device serial console tooconnect toohello Windows PowerShell interface, perform hello following steps.</span></span>

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a><span data-ttu-id="750b0-130">tooinitiate hello 服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="750b0-130">tooinitiate hello service data encryption key change</span></span>
1. <span data-ttu-id="750b0-131">選取選項 1 toolog 上，具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="750b0-131">Select option 1 toolog on with full access.</span></span>
2. <span data-ttu-id="750b0-132">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="750b0-132">At hello command prompt, type:</span></span>
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. <span data-ttu-id="750b0-133">Hello cmdlet 順利完成之後，您會得到新的服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="750b0-133">After hello cmdlet has successfully completed, you will get a new service data encryption key.</span></span> <span data-ttu-id="750b0-134">複製並儲存此金鑰，以供此程序的步驟 3 使用。</span><span class="sxs-lookup"><span data-stu-id="750b0-134">Copy and save this key for use in step 3 of this process.</span></span> <span data-ttu-id="750b0-135">此金鑰將會使用所有剩餘 hello StorSimple Manager 服務註冊裝置的 hello tooupdate。</span><span class="sxs-lookup"><span data-stu-id="750b0-135">This key will be used tooupdate all hello remaining devices registered with hello StorSimple Manager service.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="750b0-136">此程序必須在授權 StorSimple 裝置後的四個小時內起始。</span><span class="sxs-lookup"><span data-stu-id="750b0-136">This process must be initiated within four hours of authorizing a StorSimple device.</span></span>
   > 
   > 
   
   <span data-ttu-id="750b0-137">這個新的金鑰，然後會傳送 toohello 服務推入 toobe tooall hello 登錄的裝置與 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="750b0-137">This new key is then sent toohello service toobe pushed tooall hello devices that are registered with hello service.</span></span> <span data-ttu-id="750b0-138">Hello 服務儀表板上，即會出現警示。</span><span class="sxs-lookup"><span data-stu-id="750b0-138">An alert will then appear on hello service dashboard.</span></span> <span data-ttu-id="750b0-139">hello 服務將會停用所有 hello hello 註冊裝置上的作業，hello 裝置系統管理員將必須 tooupdate hello 服務資料加密金鑰 hello 上的其他裝置。</span><span class="sxs-lookup"><span data-stu-id="750b0-139">hello service will disable all hello operations on hello registered devices, and hello device administrator will then need tooupdate hello service data encryption key on hello other devices.</span></span> <span data-ttu-id="750b0-140">不過，hello I/o （傳送資料 toohello 雲端的主機） 不會被中斷。</span><span class="sxs-lookup"><span data-stu-id="750b0-140">However, hello I/Os (hosts sending data toohello cloud) will not be disrupted.</span></span>
   
   <span data-ttu-id="750b0-141">如果您有單一裝置註冊 tooyour 服務 hello 變換程序現在已完成，可以略過 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="750b0-141">If you have a single device registered tooyour service, hello rollover process is now complete and you can skip hello next step.</span></span> <span data-ttu-id="750b0-142">如果您有多個裝置已註冊的 tooyour 服務時，繼續 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="750b0-142">If you have multiple devices registered tooyour service, proceed toostep 3.</span></span>

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a><span data-ttu-id="750b0-143">步驟 3： 更新其他 StorSimple 裝置上的 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="750b0-143">Step 3: Update hello service data encryption key on other StorSimple devices</span></span>
<span data-ttu-id="750b0-144">如果您有多個裝置已註冊的 tooyour StorSimple Manager 服務，必須在您的 StorSimple 裝置 hello Windows PowerShell 介面中執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="750b0-144">These steps must be performed in hello Windows PowerShell interface of your StorSimple device if you have multiple devices registered tooyour StorSimple Manager service.</span></span> <span data-ttu-id="750b0-145">您在步驟 2 中取得的 hello 金鑰： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更必須使用的 tooupdate 所有 hello 剩餘 StorSimple 裝置向 StorSimple Manager 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="750b0-145">hello key that you obtained in Step 2: Use Windows PowerShell for StorSimple tooinitiate hello service data encryption key change must be used tooupdate all hello remaining StorSimple device registered with hello StorSimple Manager service.</span></span>

<span data-ttu-id="750b0-146">執行下列步驟 tooupdate hello 服務資料加密在裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="750b0-146">Perform hello following steps tooupdate hello service data encryption on your device.</span></span>

#### <a name="tooupdate-hello-service-data-encryption-key"></a><span data-ttu-id="750b0-147">tooupdate hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="750b0-147">tooupdate hello service data encryption key</span></span>
1. <span data-ttu-id="750b0-148">使用 Windows PowerShell for StorSimple tooconnect toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="750b0-148">Use Windows PowerShell for StorSimple tooconnect toohello console.</span></span> <span data-ttu-id="750b0-149">選取選項 1 toolog 上，具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="750b0-149">Select option 1 toolog on with full access.</span></span>
2. <span data-ttu-id="750b0-150">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="750b0-150">At hello command prompt, type:</span></span>
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. <span data-ttu-id="750b0-151">提供 hello 服務資料加密金鑰，您在取得[步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更](#to-initiate-the-service-data-encryption-key-change)。</span><span class="sxs-lookup"><span data-stu-id="750b0-151">Provide hello service data encryption key that you obtained in [Step 2: Use Windows PowerShell for StorSimple tooinitiate hello service data encryption key change](#to-initiate-the-service-data-encryption-key-change).</span></span>

