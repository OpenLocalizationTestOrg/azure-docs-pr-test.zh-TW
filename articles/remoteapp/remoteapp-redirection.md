---
title: "在 Azure RemoteApp 中使用重新導向 | Microsoft Docs"
description: "了解如何在 RemoteApp 中設定和使用重新導向"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="d2895-103">在 Azure RemoteApp 中使用重新導向</span><span class="sxs-lookup"><span data-stu-id="d2895-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d2895-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="d2895-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d2895-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="d2895-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d2895-106">裝置重新導向可讓您的使用者使用與其本機電腦、手機或平板電腦連接的裝置，來與遠端應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="d2895-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="d2895-107">l比方說，如果您透過 Azure RemoteApp 提供 Skype，您的使用者就必須在電腦安裝相機才能使用 Skype。</span><span class="sxs-lookup"><span data-stu-id="d2895-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="d2895-108">印表機、麥克風、監視器以及各種不同以 USB 連接的周邊裝置也是如此。</span><span class="sxs-lookup"><span data-stu-id="d2895-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="d2895-109">RemoteApp 會利用遠端桌面通訊協定 (RDP) 與 RemoteFX 來提供重新導向功能。</span><span class="sxs-lookup"><span data-stu-id="d2895-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="d2895-110">依預設會何種重新導向功能？</span><span class="sxs-lookup"><span data-stu-id="d2895-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="d2895-111">當您使用 RemoteApp 時，預設會啟用下列重新導向功能。</span><span class="sxs-lookup"><span data-stu-id="d2895-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="d2895-112">括號中的資訊顯示 RDP 設定。</span><span class="sxs-lookup"><span data-stu-id="d2895-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="d2895-113">在本機電腦上播放聲音 (**在這部電腦上播放**)。</span><span class="sxs-lookup"><span data-stu-id="d2895-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="d2895-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="d2895-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="d2895-115">從本機電腦擷取音訊並傳送到遠端電腦 (**從這部電腦錄製**)。</span><span class="sxs-lookup"><span data-stu-id="d2895-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="d2895-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="d2895-117">列印到本機印表機 (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="d2895-118">COM 連接埠 (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="d2895-119">智慧卡裝置 (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="d2895-120">剪貼簿 (能夠複製和貼上) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="d2895-121">清除字型平滑處理 (允許字型平滑處理:i:1)</span><span class="sxs-lookup"><span data-stu-id="d2895-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="d2895-122">重新導向所有支援的隨插即用裝置。</span><span class="sxs-lookup"><span data-stu-id="d2895-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="d2895-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="d2895-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="d2895-124">還有其他哪些重新導向功能？</span><span class="sxs-lookup"><span data-stu-id="d2895-124">What other redirection is available?</span></span>
<span data-ttu-id="d2895-125">預設會停用兩個重新導向選項：</span><span class="sxs-lookup"><span data-stu-id="d2895-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="d2895-126">磁碟機重新導向 (磁碟機對應)：您本機電腦的磁碟機會與遠端作業階段中的磁碟機對應。</span><span class="sxs-lookup"><span data-stu-id="d2895-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="d2895-127">這可讓您在遠端工作階段工作時，儲存或開啟本機磁碟機中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d2895-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="d2895-128">USB 重新導向：您可以在遠端工作階段期間使用與本機電腦連接的 USB 裝置。</span><span class="sxs-lookup"><span data-stu-id="d2895-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="d2895-129">在 RemoteApp 中變更重新導向設定</span><span class="sxs-lookup"><span data-stu-id="d2895-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="d2895-130">您可以使用 Microsoft Azure PowerShell 搭配 SDK，變更集合的裝置重新導向設定。</span><span class="sxs-lookup"><span data-stu-id="d2895-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="d2895-131">在您安裝新的 PowerShell 與 SDK 之後，請先依照 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)中所述進行設定以管理您的訂閱。</span><span class="sxs-lookup"><span data-stu-id="d2895-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d2895-132">接著使用和下面類似的命令來設定自訂 RDP 屬性：</span><span class="sxs-lookup"><span data-stu-id="d2895-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="d2895-133">(請注意，  *\`n* 做為個別的屬性之間的分隔符號。)</span><span class="sxs-lookup"><span data-stu-id="d2895-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="d2895-134">若要取得已設定的自訂 RDP 屬性清單，請執行下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d2895-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="d2895-135">請注意，只會將自訂屬性顯示為輸出，而預設屬性則否：</span><span class="sxs-lookup"><span data-stu-id="d2895-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="d2895-136">當您設定自訂屬性時，每次都要指定所有自訂屬性，不然就會將設定恢復成停用。</span><span class="sxs-lookup"><span data-stu-id="d2895-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="d2895-137">常見範例</span><span class="sxs-lookup"><span data-stu-id="d2895-137">Common examples</span></span>
<span data-ttu-id="d2895-138">使用下列 Cmdlet 可啟用磁碟機重新導向：</span><span class="sxs-lookup"><span data-stu-id="d2895-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="d2895-139">使用這個 Cmdlet 可同時啟用 USB 與磁碟機重新導向：</span><span class="sxs-lookup"><span data-stu-id="d2895-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="d2895-140">使用這個 Cmdlet 可停用剪貼簿共用：</span><span class="sxs-lookup"><span data-stu-id="d2895-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="d2895-141">在您測試變更之前，請務必將集合中的所有使用者完全登出 (而非僅中斷連線)。</span><span class="sxs-lookup"><span data-stu-id="d2895-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="d2895-142">為確保將使用者完全登出，請在 Azure 入口網站移至該集合中的 [工作階段]  索引標籤，然後將已中斷連線或已登入的任何使用者登出。</span><span class="sxs-lookup"><span data-stu-id="d2895-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="d2895-143">有時候可能需要花費數秒的時間，磁碟機才能顯示在工作階段內的檔案總管中。</span><span class="sxs-lookup"><span data-stu-id="d2895-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="d2895-144">變更 Windows 用戶端的 USB 重新導向設定</span><span class="sxs-lookup"><span data-stu-id="d2895-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="d2895-145">如果您想要在與 RemoteApp 連線的電腦上使用 USB 重新導向，必須進行 2 個動作。</span><span class="sxs-lookup"><span data-stu-id="d2895-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="d2895-146">1 - 您的系統管理員必須使用 Azure PowerShell 在集合層級啟用 USB 重新導向。</span><span class="sxs-lookup"><span data-stu-id="d2895-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="d2895-147">2 - 在您想要使用 USB 重新導向的每個裝置上，都必須啟用允許重新導向的群組原則。</span><span class="sxs-lookup"><span data-stu-id="d2895-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="d2895-148">每個想要使用 USB 重新導向的使用者都必須完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="d2895-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="d2895-149">只支援 Windows 電腦使用 Azure RemoteApp 提供 USB 重新導向。</span><span class="sxs-lookup"><span data-stu-id="d2895-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="d2895-150">為 RemoteApp 集合啟用 USB 重新導向</span><span class="sxs-lookup"><span data-stu-id="d2895-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="d2895-151">使用下列 Cmdlet，在集合層級啟用 USB 重新導向：</span><span class="sxs-lookup"><span data-stu-id="d2895-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="d2895-152">為用戶端電腦啟用 USB 重新導向</span><span class="sxs-lookup"><span data-stu-id="d2895-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="d2895-153">若要在電腦設定 USB 重新導向設定：</span><span class="sxs-lookup"><span data-stu-id="d2895-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="d2895-154">開啟本機群組原則編輯器 (GPEDIT.MSC)。</span><span class="sxs-lookup"><span data-stu-id="d2895-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="d2895-155">(從命令提示字元中執行 gpedit.msc)。</span><span class="sxs-lookup"><span data-stu-id="d2895-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="d2895-156">開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。</span><span class="sxs-lookup"><span data-stu-id="d2895-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="d2895-157">按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。</span><span class="sxs-lookup"><span data-stu-id="d2895-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="d2895-158">選取 [已啟用]，然後在 [RemoteFX USB 重新導向存取權限] 中選取系統管理員與使用者。</span><span class="sxs-lookup"><span data-stu-id="d2895-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="d2895-159">以系統管理權限開啟命令提示字元，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d2895-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="d2895-160">重新啟動電腦。</span><span class="sxs-lookup"><span data-stu-id="d2895-160">Restart the computer.</span></span>

<span data-ttu-id="d2895-161">您也可以使用群組原則管理工具，為網域中的所有電腦建立和套用 USB 重新導向原則：</span><span class="sxs-lookup"><span data-stu-id="d2895-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="d2895-162">以網域管理員的身分登入網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d2895-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="d2895-163">開啟 [群組原則管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="d2895-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="d2895-164">(按一下 [開始] > [系統管理工具] > [群組員則管理]。)</span><span class="sxs-lookup"><span data-stu-id="d2895-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="d2895-165">瀏覽到您想要建立原則的網域或組織單位。</span><span class="sxs-lookup"><span data-stu-id="d2895-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="d2895-166">以滑鼠右鍵按一下 [預設網域原則]，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="d2895-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="d2895-167">開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。</span><span class="sxs-lookup"><span data-stu-id="d2895-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="d2895-168">按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。</span><span class="sxs-lookup"><span data-stu-id="d2895-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="d2895-169">選取 [已啟用]，然後在 [RemoteFX USB 重新導向存取權限] 中選取系統管理員與使用者。</span><span class="sxs-lookup"><span data-stu-id="d2895-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="d2895-170">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d2895-170">Click **OK**.</span></span>  

