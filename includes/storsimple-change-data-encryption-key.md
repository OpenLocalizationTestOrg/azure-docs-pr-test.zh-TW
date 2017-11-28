<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-to-change-the-service-data-encryption-key-in-the-azure-classic-portal"></a><span data-ttu-id="aa5c8-101">步驟 1：在 Azure 傳統入口網站中授權裝置以變更服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="aa5c8-101">Step 1: Authorize a device to change the service data encryption key in the Azure classic portal</span></span>
<span data-ttu-id="aa5c8-102">一般而言，裝置系統管理員將會要求服務管理員授權裝置，以變更服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-102">Typically, the device administrator will request that the service administrator authorize a device to change service data encryption keys.</span></span> <span data-ttu-id="aa5c8-103">然後服務管理員就會授權裝置來變更金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-103">The service administrator will then authorize the device to change the key.</span></span>

<span data-ttu-id="aa5c8-104">此步驟會在 Azure 傳統入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-104">This step is performed in the Azure classic portal.</span></span> <span data-ttu-id="aa5c8-105">服務管理員可以在有資格獲得授權的裝置顯示清單中選取裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-105">The service administrator can select a device from a displayed list of the devices that are eligible to be authorized.</span></span> <span data-ttu-id="aa5c8-106">然後裝置就會獲得授權，以啟動服務資料加密金鑰變更程序。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-106">The device is then authorized to start the service data encryption key change process.</span></span>

#### <a name="which-devices-can-be-authorized-to-change-service-data-encryption-keys"></a><span data-ttu-id="aa5c8-107">哪些裝置可獲得授權以變更服務資料加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="aa5c8-107">Which devices can be authorized to change service data encryption keys?</span></span>
<span data-ttu-id="aa5c8-108">裝置必須符合下列準則，才能獲得授權以起始服務資料加密金鑰變更：</span><span class="sxs-lookup"><span data-stu-id="aa5c8-108">A device must meet the following criteria before it can be authorized to initiate service data encryption key changes:</span></span>

* <span data-ttu-id="aa5c8-109">裝置必須在線上，才能獲得授權以變更服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-109">The device must be online to be eligible for service data encryption key change authorization.</span></span>
* <span data-ttu-id="aa5c8-110">如果尚未起始金鑰變更，您可以在 30 分鐘後再次授權同一個裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-110">You can authorize the same device again after 30 minutes if the key change has not been initiated.</span></span>
* <span data-ttu-id="aa5c8-111">如果先前獲得授權的裝置尚未起始金鑰變更，則您可以授權另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-111">You can authorize a different device, provided that the key change has not been initiated by the previously authorized device.</span></span> <span data-ttu-id="aa5c8-112">新裝置已獲授權之後，舊裝置就無法起始變更。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-112">After the new device has been authorized, the old device cannot initiate the change.</span></span>
* <span data-ttu-id="aa5c8-113">正在變換服務資料加密金鑰時，無法授權裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-113">You cannot authorize a device while the rollover of the service data encryption key is in progress.</span></span>
* <span data-ttu-id="aa5c8-114">如果有些已向服務註冊的裝置已變換加密，而某些裝置還沒有，則您可以授權裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-114">You can authorize a device when some of the devices registered with the service have rolled over the encryption while others have not.</span></span> <span data-ttu-id="aa5c8-115">在這種情況下，有資格的裝置就是已完成服務資料加密金鑰變更的裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-115">In such cases, the eligible devices are the ones that have completed the service data encryption key change.</span></span>

> [!NOTE]
> <span data-ttu-id="aa5c8-116">在 Azure 傳統入口網站中，可獲授權以啟動金鑰變更的裝置清單不會顯示 StorSimple 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-116">In the Azure classic portal, StorSimple virtual devices are not shown in the list of devices that can be authorized to start the key change.</span></span>
> 
> 

<span data-ttu-id="aa5c8-117">請執行下列步驟，選取並授權裝置以起始服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-117">Perform the following steps to select and authorize a device to initiate the service data encryption key change.</span></span>

#### <a name="to-authorize-a-device-to-change-the-key"></a><span data-ttu-id="aa5c8-118">授權裝置以變更索引鍵</span><span class="sxs-lookup"><span data-stu-id="aa5c8-118">To authorize a device to change the key</span></span>
1. <span data-ttu-id="aa5c8-119">在服務儀表板頁面上，按一下 [ **變更服務資料加密金鑰**]。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-119">On the service dashboard page, click **Change service data encryption key**.</span></span>
   
    ![變更服務加密金鑰](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. <span data-ttu-id="aa5c8-121">在 [ **變更服務資枓加密金鑰** ] 對話方塊中，選取並授權裝置以起始服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-121">In the **Change service data encryption key** dialog box, select and authorize a device to initiate the service data encryption key change.</span></span> <span data-ttu-id="aa5c8-122">下拉式清單包含有資格獲得授權的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-122">The drop-down list has all the eligible devices that can be authorized.</span></span>
3. <span data-ttu-id="aa5c8-123">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="aa5c8-123">Click the check icon</span></span> ![核取圖示](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png)<span data-ttu-id="aa5c8-125">。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-125">.</span></span>

### <a name="step-2-use-windows-powershell-for-storsimple-to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="aa5c8-126">步驟 2：使用 Windows PowerShell for StorSimple 起始服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="aa5c8-126">Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change</span></span>
<span data-ttu-id="aa5c8-127">這個步驟是在 Windows PowerShell for StorSimple 介面中，對已獲授權的 StorSimple 裝置執行。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-127">This step is performed in the Windows PowerShell for StorSimple interface on the authorized StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="aa5c8-128">除非金鑰變換完成，否則無法在 Azure  傳統入口網站對 StorSimple Manager 服務執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-128">No operations can be performed in the Azure classic portal of your StorSimple Manager service until the key rollover is completed.</span></span>
> 
> 

<span data-ttu-id="aa5c8-129">如果您使用裝置序列主控台連接到 Windows PowerShell 介面，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-129">If you are using the device serial console to connect to the Windows PowerShell interface, perform the following steps.</span></span>

#### <a name="to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="aa5c8-130">起始服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="aa5c8-130">To initiate the service data encryption key change</span></span>
1. <span data-ttu-id="aa5c8-131">選取選項 1 以使用完整存取權登入。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-131">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="aa5c8-132">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="aa5c8-132">At the command prompt, type:</span></span>
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. <span data-ttu-id="aa5c8-133">Cmdlet 順利完成之後，您就會得到新的服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-133">After the cmdlet has successfully completed, you will get a new service data encryption key.</span></span> <span data-ttu-id="aa5c8-134">複製並儲存此金鑰，以供此程序的步驟 3 使用。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-134">Copy and save this key for use in step 3 of this process.</span></span> <span data-ttu-id="aa5c8-135">此金鑰將用來更新已向 StorSimple Manager 服務註冊的其餘所有裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-135">This key will be used to update all the remaining devices registered with the StorSimple Manager service.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="aa5c8-136">此程序必須在授權 StorSimple 裝置後的四個小時內起始。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-136">This process must be initiated within four hours of authorizing a StorSimple device.</span></span>
   > 
   > 
   
   <span data-ttu-id="aa5c8-137">然後，新金鑰就會傳送至服務並推播至所有已向服務註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-137">This new key is then sent to the service to be pushed to all the devices that are registered with the service.</span></span> <span data-ttu-id="aa5c8-138">之後，服務儀表板上將出現警示。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-138">An alert will then appear on the service dashboard.</span></span> <span data-ttu-id="aa5c8-139">此服務會停用已註冊的裝置上的所有作業，然後裝置管理員就必須在其他裝置上更新服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-139">The service will disable all the operations on the registered devices, and the device administrator will then need to update the service data encryption key on the other devices.</span></span> <span data-ttu-id="aa5c8-140">不過，不會中斷 I/O (將資料傳送至雲端的主機)。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-140">However, the I/Os (hosts sending data to the cloud) will not be disrupted.</span></span>
   
   <span data-ttu-id="aa5c8-141">如果只有一個裝置向您的服務註冊，則變換程序現在已完成，您可以略過下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-141">If you have a single device registered to your service, the rollover process is now complete and you can skip the next step.</span></span> <span data-ttu-id="aa5c8-142">如果有多個裝置向您的服務註冊，請繼續步驟 3。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-142">If you have multiple devices registered to your service, proceed to step 3.</span></span>

### <a name="step-3-update-the-service-data-encryption-key-on-other-storsimple-devices"></a><span data-ttu-id="aa5c8-143">步驟 3：在其他 StorSimple 裝置上更新服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="aa5c8-143">Step 3: Update the service data encryption key on other StorSimple devices</span></span>
<span data-ttu-id="aa5c8-144">如果有多個裝置向您的 StorSimple Manager 服務註冊，您就必須在 StorSimple 裝置的 Windows PowerShell 介面中執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-144">These steps must be performed in the Windows PowerShell interface of your StorSimple device if you have multiple devices registered to your StorSimple Manager service.</span></span> <span data-ttu-id="aa5c8-145">您必須使用您在「步驟 2：使用 Windows PowerShell for StorSimple 起始服務資料加密金鑰變更」中取得的金鑰，更新已向 StorSimple Manager 服務註冊的其餘所有 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-145">The key that you obtained in Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change must be used to update all the remaining StorSimple device registered with the StorSimple Manager service.</span></span>

<span data-ttu-id="aa5c8-146">請執行下列步驟，在您的裝置上更新服務資料加密。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-146">Perform the following steps to update the service data encryption on your device.</span></span>

#### <a name="to-update-the-service-data-encryption-key"></a><span data-ttu-id="aa5c8-147">更新服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="aa5c8-147">To update the service data encryption key</span></span>
1. <span data-ttu-id="aa5c8-148">使用 Windows PowerShell for StorSimple 連線到主控台。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-148">Use Windows PowerShell for StorSimple to connect to the console.</span></span> <span data-ttu-id="aa5c8-149">選取選項 1 以使用完整存取權登入。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-149">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="aa5c8-150">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="aa5c8-150">At the command prompt, type:</span></span>
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. <span data-ttu-id="aa5c8-151">提供您在 [步驟 2：使用 Windows PowerShell for StorSimple 起始服務資料加密金鑰變更](#to-initiate-the-service-data-encryption-key-change)中取得的服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa5c8-151">Provide the service data encryption key that you obtained in [Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change](#to-initiate-the-service-data-encryption-key-change).</span></span>

