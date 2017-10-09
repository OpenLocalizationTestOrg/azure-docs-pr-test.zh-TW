---
title: "在 Azure RemoteApp 中的 aaaUsing 重新導向 |Microsoft 文件"
description: "深入了解如何 tooconfigure 並用 RemoteApp 中的重新導向"
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="6782f-103">在 Azure RemoteApp 中使用重新導向</span><span class="sxs-lookup"><span data-stu-id="6782f-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6782f-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="6782f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6782f-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6782f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6782f-106">裝置重新導向，可讓您與使用 hello 裝置附加的 tootheir 本機電腦、 電話或平板電腦的遠端應用程式互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="6782f-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="6782f-107">比方說，如果您有提供透過 Azure RemoteApp 的 Skype，您的使用者必須安裝在與 Skype 其 PC toowork hello 相機。</span><span class="sxs-lookup"><span data-stu-id="6782f-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="6782f-108">印表機、麥克風、監視器以及各種不同以 USB 連接的周邊裝置也是如此。</span><span class="sxs-lookup"><span data-stu-id="6782f-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="6782f-109">RemoteApp 會利用 hello 遠端桌面通訊協定 (RDP) 和 RemoteFX tooprovide 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6782f-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="6782f-110">依預設會何種重新導向功能？</span><span class="sxs-lookup"><span data-stu-id="6782f-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="6782f-111">當您使用 RemoteApp 時，預設會啟用 hello 遵循重新導向。</span><span class="sxs-lookup"><span data-stu-id="6782f-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="6782f-112">在括號中的 hello 資訊會顯示 hello RDP 設定。</span><span class="sxs-lookup"><span data-stu-id="6782f-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="6782f-113">Hello 本機電腦上播放音效 (**這部電腦上播放**)。</span><span class="sxs-lookup"><span data-stu-id="6782f-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="6782f-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="6782f-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="6782f-115">擷取從 hello 本機電腦，並傳送 toohello 遠端電腦的音訊 (**從這部電腦錄製**)。</span><span class="sxs-lookup"><span data-stu-id="6782f-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="6782f-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="6782f-117">列印 toolocal 印表機 (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="6782f-118">COM 連接埠 (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="6782f-119">智慧卡裝置 (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="6782f-120">剪貼簿 （能力 toocopy 和貼上） (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="6782f-121">清除字型平滑處理 (允許字型平滑處理:i:1)</span><span class="sxs-lookup"><span data-stu-id="6782f-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="6782f-122">重新導向所有支援的隨插即用裝置。</span><span class="sxs-lookup"><span data-stu-id="6782f-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="6782f-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="6782f-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="6782f-124">還有其他哪些重新導向功能？</span><span class="sxs-lookup"><span data-stu-id="6782f-124">What other redirection is available?</span></span>
<span data-ttu-id="6782f-125">預設會停用兩個重新導向選項：</span><span class="sxs-lookup"><span data-stu-id="6782f-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="6782f-126">磁碟機重新導向 （磁碟機對應）： 本機電腦的磁碟機變成 hello 遠端工作階段中的對應磁碟機。</span><span class="sxs-lookup"><span data-stu-id="6782f-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="6782f-127">這可讓您儲存或開啟的檔案從本機磁碟機 hello 遠端工作階段中工作時。</span><span class="sxs-lookup"><span data-stu-id="6782f-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="6782f-128">USB 重新導向： 您可以使用 hello 遠端工作階段中的 hello USB 裝置連接的 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="6782f-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="6782f-129">在 RemoteApp 中變更重新導向設定</span><span class="sxs-lookup"><span data-stu-id="6782f-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="6782f-130">您可以使用 hello Microsoft Azure PowerShell sdk 變更 hello 裝置重新導向設定集合。</span><span class="sxs-lookup"><span data-stu-id="6782f-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="6782f-131">您安裝之後 hello 新 PowerShell 及 SDK，請先設定您的訂閱中所述的 toomanage[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6782f-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="6782f-132">接著，使用下列 tooset hello 自訂 RDP 屬性命令類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="6782f-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="6782f-133">(請注意，  *\`n* 做為個別的屬性之間的分隔符號。)</span><span class="sxs-lookup"><span data-stu-id="6782f-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="6782f-134">tooget 何種自訂 RDP 屬性的設定，執行下列 cmdlet 的 hello 的清單。</span><span class="sxs-lookup"><span data-stu-id="6782f-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="6782f-135">請注意，只能自訂屬性會顯示為輸出結果，並且不 hello 預設屬性：</span><span class="sxs-lookup"><span data-stu-id="6782f-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="6782f-136">當您設定自訂屬性，您必須指定所有自訂屬性每個時間;否則 hello 設定會還原 toodisabled。</span><span class="sxs-lookup"><span data-stu-id="6782f-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="6782f-137">常見範例</span><span class="sxs-lookup"><span data-stu-id="6782f-137">Common examples</span></span>
<span data-ttu-id="6782f-138">使用下列 cmdlet tooenable 磁碟機重新導向的 hello:</span><span class="sxs-lookup"><span data-stu-id="6782f-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="6782f-139">使用這個指令程式 tooenable USB 和磁碟機重新導向：</span><span class="sxs-lookup"><span data-stu-id="6782f-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="6782f-140">使用這個指令程式 toodisable 剪貼簿共用：</span><span class="sxs-lookup"><span data-stu-id="6782f-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="6782f-141">要確定 toocompletely 登出 hello 集合中的所有使用者 （和不只是將它們中斷連線） 測試 hello 變更之前。</span><span class="sxs-lookup"><span data-stu-id="6782f-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="6782f-142">tooensure 使用者會完全登出，請移 toohello**工作階段**hello Azure 入口網站中的 hello 集合中索引標籤，然後中斷連接或登入任何使用者登出。</span><span class="sxs-lookup"><span data-stu-id="6782f-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="6782f-143">有時可能要花幾秒鐘 hello 本機磁碟機 tooshow 在 [總管] 內 hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6782f-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="6782f-144">變更 Windows 用戶端的 USB 重新導向設定</span><span class="sxs-lookup"><span data-stu-id="6782f-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="6782f-145">如果您想 toouse 連線 tooRemoteApp 的電腦上的 USB 重新導向，皆有 2 需要 toohappen 的動作。</span><span class="sxs-lookup"><span data-stu-id="6782f-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="6782f-146">1-您的系統管理員必須使用 Azure PowerShell 的 tooenable hello 集合層級的 USB 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6782f-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="6782f-147">2-每個在裝置上您想要 toouse USB 重新導向，您需要 tooenable 的群組原則，允許它。</span><span class="sxs-lookup"><span data-stu-id="6782f-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="6782f-148">此步驟需要 toobe 完成每個使用者，想 toouse USB 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6782f-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="6782f-149">只支援 Windows 電腦使用 Azure RemoteApp 提供 USB 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6782f-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="6782f-150">啟用 hello RemoteApp 集合的 USB 重新導向</span><span class="sxs-lookup"><span data-stu-id="6782f-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="6782f-151">使用下列 cmdlet tooenable USB 重新導向 hello 集合層級的 hello:</span><span class="sxs-lookup"><span data-stu-id="6782f-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="6782f-152">啟用 hello 用戶端電腦的 USB 重新導向</span><span class="sxs-lookup"><span data-stu-id="6782f-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="6782f-153">在您的電腦上的 tooconfigure USB 重新導向設定：</span><span class="sxs-lookup"><span data-stu-id="6782f-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="6782f-154">開啟 hello 本機群組原則編輯器 (GPEDIT。MSC)。</span><span class="sxs-lookup"><span data-stu-id="6782f-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="6782f-155">(從命令提示字元中執行 gpedit.msc)。</span><span class="sxs-lookup"><span data-stu-id="6782f-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="6782f-156">開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。</span><span class="sxs-lookup"><span data-stu-id="6782f-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="6782f-157">按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。</span><span class="sxs-lookup"><span data-stu-id="6782f-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="6782f-158">選取**啟用**，然後選取**系統管理員和使用者在 hello RemoteFX USB 重新導向的存取權限**。</span><span class="sxs-lookup"><span data-stu-id="6782f-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="6782f-159">以系統管理權限，開啟命令提示字元，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6782f-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="6782f-160">Hello 電腦重新啟動。</span><span class="sxs-lookup"><span data-stu-id="6782f-160">Restart hello computer.</span></span>

<span data-ttu-id="6782f-161">您也可以使用 hello 群組原則管理工具 toocreate 及 hello 所有電腦的 USB 重新導向原則套用在網域中：</span><span class="sxs-lookup"><span data-stu-id="6782f-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="6782f-162">Hello 網域系統管理員身分登入 hello 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="6782f-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="6782f-163">開啟 hello 群組原則管理主控台。</span><span class="sxs-lookup"><span data-stu-id="6782f-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="6782f-164">(按一下 [開始] > [系統管理工具] > [群組員則管理]。)</span><span class="sxs-lookup"><span data-stu-id="6782f-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="6782f-165">瀏覽 toohello 網域或組織單位，您會想 toocreate hello 原則。</span><span class="sxs-lookup"><span data-stu-id="6782f-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="6782f-166">以滑鼠右鍵按一下 預設網域原則，然後按一下編輯。</span><span class="sxs-lookup"><span data-stu-id="6782f-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="6782f-167">開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。</span><span class="sxs-lookup"><span data-stu-id="6782f-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="6782f-168">按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。</span><span class="sxs-lookup"><span data-stu-id="6782f-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="6782f-169">選取**啟用**，然後選取**系統管理員和使用者在 hello RemoteFX USB 重新導向的存取權限**。</span><span class="sxs-lookup"><span data-stu-id="6782f-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="6782f-170">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6782f-170">Click **OK**.</span></span>  

