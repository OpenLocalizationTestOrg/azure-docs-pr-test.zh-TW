---
title: "aaaHow 導向 Azure RemoteApp 中的 USB 裝置嗎？ | Microsoft Docs"
description: "深入了解如何在 Azure RemoteApp 中的 USB 裝置的 toouse 重新導向。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a><span data-ttu-id="e32b8-104">如何在 Azure RemoteApp 中重新導向 QuickBooks？</span><span class="sxs-lookup"><span data-stu-id="e32b8-104">How do you redirect USB devices in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e32b8-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e32b8-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e32b8-106">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e32b8-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e32b8-107">裝置重新導向可以讓使用者使用 Azure RemoteApp 中的 hello 應用程式中的 hello USB 裝置連接的 tootheir 電腦或平板電腦。</span><span class="sxs-lookup"><span data-stu-id="e32b8-107">Device redirection lets users use hello USB devices attached tootheir computer or tablet with hello apps in Azure RemoteApp.</span></span> <span data-ttu-id="e32b8-108">例如，如果您已共用 Skype 透過 Azure RemoteApp，您的使用者需要 toobe 無法 toouse 其裝置相機。</span><span class="sxs-lookup"><span data-stu-id="e32b8-108">For example, if you shared Skype through Azure RemoteApp, your users need toobe able toouse their device cameras.</span></span>

<span data-ttu-id="e32b8-109">您在進一步討論前，請確定您讀取中的 hello USB 重新導向資訊[使用 Azure RemoteApp 中的重新導向](remoteapp-redirection.md)。</span><span class="sxs-lookup"><span data-stu-id="e32b8-109">Before you go further, make sure you read hello USB redirection information in [Using redirection in Azure RemoteApp](remoteapp-redirection.md).</span></span> <span data-ttu-id="e32b8-110">不過 hello 建議 nusbdevicestoredirect:s: * 無法用於 USB 網路攝影機和部分 USB 印表機或 USB multifunctional 裝置可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="e32b8-110">However hello recommended  nusbdevicestoredirect:s:* won't work for USB web cameras and may not work for some USB printers or USB multifunctional devices.</span></span> <span data-ttu-id="e32b8-111">根據設計，並基於安全性理由，hello Azure RemoteApp 管理員有 tooenable 重新導向裝置類別 GUID 或裝置執行個體識別碼之前，您的使用者可以使用這些裝置。</span><span class="sxs-lookup"><span data-stu-id="e32b8-111">By design and for security reasons, hello Azure RemoteApp administrator has tooenable redirection either by device class GUID or by device instance ID before your users can use those devices.</span></span>

<span data-ttu-id="e32b8-112">雖然這篇文章討論有關 web 數位相機重新導向，您可以使用類似的方法 tooredirect USB 印表機和其他 USB multifunctional 裝置不會重新導向的 hello **nusbdevicestoredirect:s:*** 命令。</span><span class="sxs-lookup"><span data-stu-id="e32b8-112">Although this article talks about web camera redirection, you can use a similar approach tooredirect USB printers and other USB multifunctional devices that are not redirected by hello **nusbdevicestoredirect:s:*** command.</span></span>

## <a name="redirection-options-for-usb-devices"></a><span data-ttu-id="e32b8-113">USB 裝置的重新導向選項</span><span class="sxs-lookup"><span data-stu-id="e32b8-113">Redirection options for USB devices</span></span>
<span data-ttu-id="e32b8-114">Azure RemoteApp 使用非常類似的機制，將 USB 裝置重新導向，當 hello 可用的遠端桌面服務。</span><span class="sxs-lookup"><span data-stu-id="e32b8-114">Azure RemoteApp uses very similar mechanisms for redirecting USB devices as hello ones available for Remote Desktop Services.</span></span> <span data-ttu-id="e32b8-115">hello 基礎技術可讓您選擇 hello 正確重新導向方法指定的裝置，最佳的高層級 tooget hello 和使用 hello 的 RemoteFX USB 裝置重新導向**usbdevicestoredirect:s:**命令。</span><span class="sxs-lookup"><span data-stu-id="e32b8-115">hello underlying technology lets you choose hello correct redirection method for a given device, tooget hello best of both high-level and RemoteFX USB device redirection using hello **usbdevicestoredirect:s:** command.</span></span> <span data-ttu-id="e32b8-116">有四個項目 toothis 命令：</span><span class="sxs-lookup"><span data-stu-id="e32b8-116">There are four elements toothis command:</span></span>

| <span data-ttu-id="e32b8-117">處理順序</span><span class="sxs-lookup"><span data-stu-id="e32b8-117">Processing order</span></span> | <span data-ttu-id="e32b8-118">參數</span><span class="sxs-lookup"><span data-stu-id="e32b8-118">Parameter</span></span> | <span data-ttu-id="e32b8-119">說明</span><span class="sxs-lookup"><span data-stu-id="e32b8-119">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e32b8-120">1</span><span class="sxs-lookup"><span data-stu-id="e32b8-120">1</span></span> |* |<span data-ttu-id="e32b8-121">選取高層級重新導向未挑選的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="e32b8-121">Selects all devices that aren't picked up by high-level redirection.</span></span> <span data-ttu-id="e32b8-122">附註：根據設計，* 不適用於 USB 網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="e32b8-122">Note: By design, * doesn't work for USB web cameras.</span></span> |
| <span data-ttu-id="e32b8-123">{Device class GUID}</span><span class="sxs-lookup"><span data-stu-id="e32b8-123">{Device class GUID}</span></span> |<span data-ttu-id="e32b8-124">選取 所有裝置都符合指定的 hello 裝置安裝類別。</span><span class="sxs-lookup"><span data-stu-id="e32b8-124">Selects all devices that match hello specified device setup class.</span></span> | |
| <span data-ttu-id="e32b8-125">USB\InstanceID</span><span class="sxs-lookup"><span data-stu-id="e32b8-125">USB\InstanceID</span></span> |<span data-ttu-id="e32b8-126">選取指定的給定執行個體識別碼 hello 的 USB 裝置</span><span class="sxs-lookup"><span data-stu-id="e32b8-126">Selects a USB device specified for hello given instance ID.</span></span> | |
| <span data-ttu-id="e32b8-127">2</span><span class="sxs-lookup"><span data-stu-id="e32b8-127">2</span></span> |<span data-ttu-id="e32b8-128">-USB\Instance ID</span><span class="sxs-lookup"><span data-stu-id="e32b8-128">-USB\Instance ID</span></span> |<span data-ttu-id="e32b8-129">移除 hello hello 指定裝置的重新導向設定。</span><span class="sxs-lookup"><span data-stu-id="e32b8-129">Removes hello redirection settings for hello specified device.</span></span> |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a><span data-ttu-id="e32b8-130">將 USB 裝置重新導向使用 hello 裝置類別 GUID</span><span class="sxs-lookup"><span data-stu-id="e32b8-130">Redirecting a USB device by using hello device class GUID</span></span>
<span data-ttu-id="e32b8-131">有兩種方式 toofind hello 裝置類別 GUID，可用於重新導向。</span><span class="sxs-lookup"><span data-stu-id="e32b8-131">There are two ways toofind hello device class GUID that can be used for redirection.</span></span> 

<span data-ttu-id="e32b8-132">hello 第一個選項是 toouse hello [System-Defined 裝置安裝類別可以使用 tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e32b8-132">hello first option is toouse hello [System-Defined Device Setup Classes Available tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx).</span></span> <span data-ttu-id="e32b8-133">挑選最能符合 hello 裝置附加的 toohello 本機電腦的 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="e32b8-133">Pick hello class that most closely matches hello device attached toohello local computer.</span></span> <span data-ttu-id="e32b8-134">若為數位相機，這可能是 [影像裝置] 類別或 [視訊擷取裝置] 類別。</span><span class="sxs-lookup"><span data-stu-id="e32b8-134">For digital cameras this could be an Imaging Device class or Video Capture Device class.</span></span> <span data-ttu-id="e32b8-135">您將需要 toodo 某些實驗 hello 裝置類別 toofind hello 正確類別可搭配本機 hello GUID 附加 （在我們的案例 hello 網路攝影機） 的 USB 裝置。</span><span class="sxs-lookup"><span data-stu-id="e32b8-135">You'll need toodo some experimentation with hello device classes toofind hello correct class GUID that works with hello locally attached USB device (in our case hello web camera).</span></span>

<span data-ttu-id="e32b8-136">更好的方法或 hello 第二個選項，是 toofollow 這些步驟 toofind hello 特定裝置類別 GUID:</span><span class="sxs-lookup"><span data-stu-id="e32b8-136">A better way, or hello second option, is toofollow these steps toofind hello specific device class GUID:</span></span>

1. <span data-ttu-id="e32b8-137">開啟裝置管理員 hello，找出 hello 裝置會被重新導向，以滑鼠右鍵按一下，並開啟 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="e32b8-137">Open hello Device Manager, locate hello device that will be redirected and right-click it, and then open hello properties.</span></span>
   <span data-ttu-id="e32b8-138">![開啟裝置管理員 hello](./media/remoteapp-usbredir/ra-devicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="e32b8-138">![Open hello Device Manager](./media/remoteapp-usbredir/ra-devicemanager.png)</span></span>
2. <span data-ttu-id="e32b8-139">在 hello**詳細資料**索引標籤上，選擇 hello 屬性**類別 Guid**。</span><span class="sxs-lookup"><span data-stu-id="e32b8-139">On hello **Details** tab, choose hello property **Class Guid**.</span></span> <span data-ttu-id="e32b8-140">會顯示 hello 值為 hello 為該類型的裝置類別 GUID。</span><span class="sxs-lookup"><span data-stu-id="e32b8-140">hello value which appears is hello Class GUID for that type of device.</span></span>
   <span data-ttu-id="e32b8-141">![攝影機屬性](./media/remoteapp-usbredir/ra-classguid.png)</span><span class="sxs-lookup"><span data-stu-id="e32b8-141">![Camera properties](./media/remoteapp-usbredir/ra-classguid.png)</span></span>
3. <span data-ttu-id="e32b8-142">使用 hello 類別 Guid 值 tooredirect 裝置加以比對。</span><span class="sxs-lookup"><span data-stu-id="e32b8-142">Use hello Class Guid value tooredirect devices that match it.</span></span>

<span data-ttu-id="e32b8-143">例如：</span><span class="sxs-lookup"><span data-stu-id="e32b8-143">For example:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="e32b8-144">您可以結合多個裝置重新導向 hello 中的相同的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e32b8-144">You can combine multiple device redirections in hello same cmdlet.</span></span> <span data-ttu-id="e32b8-145">例如： tooredirect 本機儲存體和 USB web 相機，指令程式看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="e32b8-145">For example: tooredirect local storage and a USB web camera, cmdlet looks like this:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="e32b8-146">當您將裝置重新導向設定由類別 GUID 符合類別 GUID hello 中的指定的集合的所有裝置重新都導向。</span><span class="sxs-lookup"><span data-stu-id="e32b8-146">When you set device redirection by class GUID all devices that match that class GUID in hello specified collection are redirected.</span></span> <span data-ttu-id="e32b8-147">例如，如果沒有 hello 區域網路上的多部電腦具有 hello 相同 USB 網路攝影機，您可以執行單一 cmdlet tooredirect 所有 hello 網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="e32b8-147">For example, if there are multiple computers on hello local network that have hello same USB web cameras, you can run a single cmdlet tooredirect all of hello web cameras.</span></span>

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a><span data-ttu-id="e32b8-148">將 USB 裝置重新導向使用 hello 裝置執行個體識別碼</span><span class="sxs-lookup"><span data-stu-id="e32b8-148">Redirecting a USB device by using hello device instance ID</span></span>
<span data-ttu-id="e32b8-149">如果您想要更細微的控制，而且想 toocontrol 每一裝置的重新導向，您可以使用 hello **USB\InstanceID**重新導向參數。</span><span class="sxs-lookup"><span data-stu-id="e32b8-149">If you want more fine-grained control and want toocontrol redirection per device, you can use hello **USB\InstanceID** redirection parameter.</span></span>

<span data-ttu-id="e32b8-150">hello 最困難的部分，這個方法尋找 hello USB 裝置執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="e32b8-150">hello hardest part of this method is finding hello USB device instance ID.</span></span> <span data-ttu-id="e32b8-151">您需要存取 toohello 電腦與 hello 特定 USB 裝置。</span><span class="sxs-lookup"><span data-stu-id="e32b8-151">You'll need access toohello computer and hello specific USB device.</span></span> <span data-ttu-id="e32b8-152">接著，遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e32b8-152">Then follow these steps:</span></span>

1. <span data-ttu-id="e32b8-153">中所述，啟用遠端桌面工作階段中的 hello 裝置重新導向[如何使用我的裝置和資源的遠端桌面工作階段中？](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)</span><span class="sxs-lookup"><span data-stu-id="e32b8-153">Enable hello device redirection in Remote Desktop Session as described in [How can I use my devices and resources in a Remote Desktop session?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)</span></span>
2. <span data-ttu-id="e32b8-154">開啟遠端桌面連線，然後按一下 [顯示選項] 。</span><span class="sxs-lookup"><span data-stu-id="e32b8-154">Open a Remote Desktop Connection and click **Show Options**.</span></span>
3. <span data-ttu-id="e32b8-155">按一下**存**toosave hello 目前連線的設定 tooan RDP 檔。</span><span class="sxs-lookup"><span data-stu-id="e32b8-155">Click **Save as** toosave hello current connection settings tooan RDP file.</span></span>  
    <span data-ttu-id="e32b8-156">![將 hello 設定儲存為 RDP 檔案](./media/remoteapp-usbredir/ra-saveasrdp.png)</span><span class="sxs-lookup"><span data-stu-id="e32b8-156">![Save hello settings as an RDP file](./media/remoteapp-usbredir/ra-saveasrdp.png)</span></span>
4. <span data-ttu-id="e32b8-157">選擇 檔案名稱和位置，例如 MyConnection.rdp 和此 PC\Documents，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e32b8-157">Choose a file name and a location, for example MyConnection.rdp and This PC\Documents, and save hello file.</span></span>
5. <span data-ttu-id="e32b8-158">開啟 hello MyConnection.rdp 檔案使用文字編輯器，並尋找 hello 執行個體識別碼的裝置 hello 想 tooredirect。</span><span class="sxs-lookup"><span data-stu-id="e32b8-158">Open hello MyConnection.rdp file using a text editor and find hello instance ID of hello device you want tooredirect.</span></span>

<span data-ttu-id="e32b8-159">現在，在下列指令程式的 hello 使用 hello 執行個體識別碼：</span><span class="sxs-lookup"><span data-stu-id="e32b8-159">Now, use hello instance ID in hello following cmdlet:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a><span data-ttu-id="e32b8-160">幫我們來協助您</span><span class="sxs-lookup"><span data-stu-id="e32b8-160">Help us help you</span></span>
<span data-ttu-id="e32b8-161">您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？</span><span class="sxs-lookup"><span data-stu-id="e32b8-161">Did you know that in addition toorating this article and making comments down below, you can make changes toohello article itself?</span></span> <span data-ttu-id="e32b8-162">有所遺漏？</span><span class="sxs-lookup"><span data-stu-id="e32b8-162">Something missing?</span></span> <span data-ttu-id="e32b8-163">有所錯誤？</span><span class="sxs-lookup"><span data-stu-id="e32b8-163">Something wrong?</span></span> <span data-ttu-id="e32b8-164">我是否撰寫了令人混淆的內容？</span><span class="sxs-lookup"><span data-stu-id="e32b8-164">Did I write something that's just confusing?</span></span> <span data-ttu-id="e32b8-165">向上捲動，然後按一下  **GitHub 上編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。</span><span class="sxs-lookup"><span data-stu-id="e32b8-165">Scroll up and click **Edit on GitHub** toomake changes - those will come toous for review, and then, once we sign off on them, you'll see your changes and improvements right here.</span></span>

