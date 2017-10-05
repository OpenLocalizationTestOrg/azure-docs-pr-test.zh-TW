---
title: "如何在 Azure RemoteApp 中重新導向 QuickBooks？ | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中對 USB 裝置使用重新導向。"
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
ms.openlocfilehash: 3d7165d2c3dafe87b829e588b9e7f2c377552a35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a><span data-ttu-id="b7441-104">如何在 Azure RemoteApp 中重新導向 QuickBooks？</span><span class="sxs-lookup"><span data-stu-id="b7441-104">How do you redirect USB devices in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b7441-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="b7441-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b7441-106">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="b7441-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b7441-107">裝置重新導向可讓使用者在 Azure RemoteApp 中透過應用程式使用連接到電腦或平板電腦的 USB 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-107">Device redirection lets users use the USB devices attached to their computer or tablet with the apps in Azure RemoteApp.</span></span> <span data-ttu-id="b7441-108">例如，如果您透過 Azure RemoteApp 共用 Skype，您的使用者必須能夠使用其裝置相機。</span><span class="sxs-lookup"><span data-stu-id="b7441-108">For example, if you shared Skype through Azure RemoteApp, your users need to be able to use their device cameras.</span></span>

<span data-ttu-id="b7441-109">進一步執行之前，請確定您已閱讀 [在 Azure RemoteApp 中使用重新導向](remoteapp-redirection.md)中的 USB 重新導向資訊。</span><span class="sxs-lookup"><span data-stu-id="b7441-109">Before you go further, make sure you read the USB redirection information in [Using redirection in Azure RemoteApp](remoteapp-redirection.md).</span></span> <span data-ttu-id="b7441-110">不過，建議的 nusbdevicestoredirect:s: * 並不適用於 USB 網路攝影機，也可能不適用於某些 USB 印表機或 USB 多工裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-110">However the recommended  nusbdevicestoredirect:s:* won't work for USB web cameras and may not work for some USB printers or USB multifunctional devices.</span></span> <span data-ttu-id="b7441-111">基於設計和安全性理由，Azure RemoteApp 系統管理員必須先依裝置類別 GUID 或依裝置執行個體識別碼啟用重新導向，您的使用者才能使用這些裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-111">By design and for security reasons, the Azure RemoteApp administrator has to enable redirection either by device class GUID or by device instance ID before your users can use those devices.</span></span>

<span data-ttu-id="b7441-112">雖然這篇文章討論網路攝影機重新導向，但您仍可使用類似的方法來重新導向 **nusbdevicestoredirect:s:*** 命令不會重新導向的 USB 印表機和其他 USB 多工裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-112">Although this article talks about web camera redirection, you can use a similar approach to redirect USB printers and other USB multifunctional devices that are not redirected by the **nusbdevicestoredirect:s:*** command.</span></span>

## <a name="redirection-options-for-usb-devices"></a><span data-ttu-id="b7441-113">USB 裝置的重新導向選項</span><span class="sxs-lookup"><span data-stu-id="b7441-113">Redirection options for USB devices</span></span>
<span data-ttu-id="b7441-114">如同遠端桌面服務可用的機制一樣，Azure RemoteApp 會使用非常類似的機制重新導向 USB 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-114">Azure RemoteApp uses very similar mechanisms for redirecting USB devices as the ones available for Remote Desktop Services.</span></span> <span data-ttu-id="b7441-115">此基礎技術可讓您為指定的裝置選擇正確的重新導向方法，以使用 **usbdevicestoredirect:s:** 命令充分發揮高層級和 RemoteFX USB 裝置重新導向。</span><span class="sxs-lookup"><span data-stu-id="b7441-115">The underlying technology lets you choose the correct redirection method for a given device, to get the best of both high-level and RemoteFX USB device redirection using the **usbdevicestoredirect:s:** command.</span></span> <span data-ttu-id="b7441-116">此命令有四個元素：</span><span class="sxs-lookup"><span data-stu-id="b7441-116">There are four elements to this command:</span></span>

| <span data-ttu-id="b7441-117">處理順序</span><span class="sxs-lookup"><span data-stu-id="b7441-117">Processing order</span></span> | <span data-ttu-id="b7441-118">參數</span><span class="sxs-lookup"><span data-stu-id="b7441-118">Parameter</span></span> | <span data-ttu-id="b7441-119">說明</span><span class="sxs-lookup"><span data-stu-id="b7441-119">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b7441-120">1</span><span class="sxs-lookup"><span data-stu-id="b7441-120">1</span></span> |* |<span data-ttu-id="b7441-121">選取高層級重新導向未挑選的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-121">Selects all devices that aren't picked up by high-level redirection.</span></span> <span data-ttu-id="b7441-122">附註：根據設計，* 不適用於 USB 網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="b7441-122">Note: By design, * doesn't work for USB web cameras.</span></span> |
| <span data-ttu-id="b7441-123">{Device class GUID}</span><span class="sxs-lookup"><span data-stu-id="b7441-123">{Device class GUID}</span></span> |<span data-ttu-id="b7441-124">選取所有符合指定之裝置安裝類別的裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-124">Selects all devices that match the specified device setup class.</span></span> | |
| <span data-ttu-id="b7441-125">USB\InstanceID</span><span class="sxs-lookup"><span data-stu-id="b7441-125">USB\InstanceID</span></span> |<span data-ttu-id="b7441-126">選取針對指定之執行個體識別碼指定的 USB 裝置</span><span class="sxs-lookup"><span data-stu-id="b7441-126">Selects a USB device specified for the given instance ID.</span></span> | |
| <span data-ttu-id="b7441-127">2</span><span class="sxs-lookup"><span data-stu-id="b7441-127">2</span></span> |<span data-ttu-id="b7441-128">-USB\Instance ID</span><span class="sxs-lookup"><span data-stu-id="b7441-128">-USB\Instance ID</span></span> |<span data-ttu-id="b7441-129">移除指定之裝置的重新導向設定。</span><span class="sxs-lookup"><span data-stu-id="b7441-129">Removes the redirection settings for the specified device.</span></span> |

## <a name="redirecting-a-usb-device-by-using-the-device-class-guid"></a><span data-ttu-id="b7441-130">使用裝置類別 GUID 重新導向 USB 裝置</span><span class="sxs-lookup"><span data-stu-id="b7441-130">Redirecting a USB device by using the device class GUID</span></span>
<span data-ttu-id="b7441-131">尋找可用於重新導向的裝置類別 GUID 的方式有兩種。</span><span class="sxs-lookup"><span data-stu-id="b7441-131">There are two ways to find the device class GUID that can be used for redirection.</span></span> 

<span data-ttu-id="b7441-132">第一個選項是使用 [供應商可用的系統定義裝置安裝類別](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b7441-132">The first option is to use the [System-Defined Device Setup Classes Available to Vendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx).</span></span> <span data-ttu-id="b7441-133">選擇最符合連接到本機電腦之裝置的類別。</span><span class="sxs-lookup"><span data-stu-id="b7441-133">Pick the class that most closely matches the device attached to the local computer.</span></span> <span data-ttu-id="b7441-134">若為數位相機，這可能是 [影像裝置] 類別或 [視訊擷取裝置] 類別。</span><span class="sxs-lookup"><span data-stu-id="b7441-134">For digital cameras this could be an Imaging Device class or Video Capture Device class.</span></span> <span data-ttu-id="b7441-135">您必須以裝置類別進行一些實驗，以尋找適用於本機連接 USB 裝置 (在我們的案例中為網路攝影機) 的正確類別 GUID。</span><span class="sxs-lookup"><span data-stu-id="b7441-135">You'll need to do some experimentation with the device classes to find the correct class GUID that works with the locally attached USB device (in our case the web camera).</span></span>

<span data-ttu-id="b7441-136">比較好的方法或第二個選項，就是遵循下列步驟來尋找特定裝置類別 GUID：</span><span class="sxs-lookup"><span data-stu-id="b7441-136">A better way, or the second option, is to follow these steps to find the specific device class GUID:</span></span>

1. <span data-ttu-id="b7441-137">開啟裝置管理員、找出要重新導向的裝置並按一下滑鼠右鍵，然後開啟屬性。</span><span class="sxs-lookup"><span data-stu-id="b7441-137">Open the Device Manager, locate the device that will be redirected and right-click it, and then open the properties.</span></span>
   <span data-ttu-id="b7441-138">![開啟裝置管理員](./media/remoteapp-usbredir/ra-devicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="b7441-138">![Open the Device Manager](./media/remoteapp-usbredir/ra-devicemanager.png)</span></span>
2. <span data-ttu-id="b7441-139">在 [詳細資料] 索引標籤上，選擇 [類別 Guid] 屬性。</span><span class="sxs-lookup"><span data-stu-id="b7441-139">On the **Details** tab, choose the property **Class Guid**.</span></span> <span data-ttu-id="b7441-140">出現的值就是該類型裝置的類別 GUID。</span><span class="sxs-lookup"><span data-stu-id="b7441-140">The value which appears is the Class GUID for that type of device.</span></span>
   <span data-ttu-id="b7441-141">![攝影機屬性](./media/remoteapp-usbredir/ra-classguid.png)</span><span class="sxs-lookup"><span data-stu-id="b7441-141">![Camera properties](./media/remoteapp-usbredir/ra-classguid.png)</span></span>
3. <span data-ttu-id="b7441-142">使用類別 Guid 值來重新導向相符的裝置。</span><span class="sxs-lookup"><span data-stu-id="b7441-142">Use the Class Guid value to redirect devices that match it.</span></span>

<span data-ttu-id="b7441-143">例如：</span><span class="sxs-lookup"><span data-stu-id="b7441-143">For example:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="b7441-144">您可以在相同 Cmdlet 中合併多個裝置重新導向。</span><span class="sxs-lookup"><span data-stu-id="b7441-144">You can combine multiple device redirections in the same cmdlet.</span></span> <span data-ttu-id="b7441-145">例如：若要重新導向本機儲存體和 USB 網路攝影機，Cmdlet 會如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7441-145">For example: to redirect local storage and a USB web camera, cmdlet looks like this:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="b7441-146">當您依類別 GUID 設定裝置重新導向時，指定的集合中符合該類別 GUID 的所有裝置都會重新導向。</span><span class="sxs-lookup"><span data-stu-id="b7441-146">When you set device redirection by class GUID all devices that match that class GUID in the specified collection are redirected.</span></span> <span data-ttu-id="b7441-147">比方說，如果本機網路上有多部具有相同 USB 網路攝影機的電腦，您可以執行單一 Cmdlet 來重新導向所有網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="b7441-147">For example, if there are multiple computers on the local network that have the same USB web cameras, you can run a single cmdlet to redirect all of the web cameras.</span></span>

## <a name="redirecting-a-usb-device-by-using-the-device-instance-id"></a><span data-ttu-id="b7441-148">使用裝置執行個體識別碼重新導向 USB 裝置</span><span class="sxs-lookup"><span data-stu-id="b7441-148">Redirecting a USB device by using the device instance ID</span></span>
<span data-ttu-id="b7441-149">如果您想要更細微的控制而且想要控制每個裝置的重新導向，您可以使用 **USB\InstanceID** 重新導向參數。</span><span class="sxs-lookup"><span data-stu-id="b7441-149">If you want more fine-grained control and want to control redirection per device, you can use the **USB\InstanceID** redirection parameter.</span></span>

<span data-ttu-id="b7441-150">此方法最困難的部分是尋找 USB 裝置執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="b7441-150">The hardest part of this method is finding the USB device instance ID.</span></span> <span data-ttu-id="b7441-151">您需要有電腦和特定 USB 裝置的存取權。</span><span class="sxs-lookup"><span data-stu-id="b7441-151">You'll need access to the computer and the specific USB device.</span></span> <span data-ttu-id="b7441-152">接著，遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b7441-152">Then follow these steps:</span></span>

1. <span data-ttu-id="b7441-153">如[如何在遠端桌面工作階段中使用我的裝置和資源？](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)所述，在遠端桌面工作階段中啟用裝置重新導向。</span><span class="sxs-lookup"><span data-stu-id="b7441-153">Enable the device redirection in Remote Desktop Session as described in [How can I use my devices and resources in a Remote Desktop session?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)</span></span>
2. <span data-ttu-id="b7441-154">開啟遠端桌面連線，然後按一下 [顯示選項] 。</span><span class="sxs-lookup"><span data-stu-id="b7441-154">Open a Remote Desktop Connection and click **Show Options**.</span></span>
3. <span data-ttu-id="b7441-155">按一下 [另存新檔]  將目前的連線設定儲存至 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7441-155">Click **Save as** to save the current connection settings to an RDP file.</span></span>  
    <span data-ttu-id="b7441-156">![將設定儲存為 RDP 檔案](./media/remoteapp-usbredir/ra-saveasrdp.png)</span><span class="sxs-lookup"><span data-stu-id="b7441-156">![Save the settings as an RDP file](./media/remoteapp-usbredir/ra-saveasrdp.png)</span></span>
4. <span data-ttu-id="b7441-157">選擇檔案名稱和位置，例如 MyConnection.rdp 和 This PC\Documents，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="b7441-157">Choose a file name and a location, for example MyConnection.rdp and This PC\Documents, and save the file.</span></span>
5. <span data-ttu-id="b7441-158">使用文字編輯器開啟 MyConnection.rdp 檔案，並尋找您要重新導向之裝置的執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="b7441-158">Open the MyConnection.rdp file using a text editor and find the instance ID of the device you want to redirect.</span></span>

<span data-ttu-id="b7441-159">現在，在下列 Cmdlet 中使用執行個體識別碼：</span><span class="sxs-lookup"><span data-stu-id="b7441-159">Now, use the instance ID in the following cmdlet:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a><span data-ttu-id="b7441-160">幫我們來協助您</span><span class="sxs-lookup"><span data-stu-id="b7441-160">Help us help you</span></span>
<span data-ttu-id="b7441-161">您知道除了評比這篇文章以及在下面留言以外，您可以變更文件本身嗎？</span><span class="sxs-lookup"><span data-stu-id="b7441-161">Did you know that in addition to rating this article and making comments down below, you can make changes to the article itself?</span></span> <span data-ttu-id="b7441-162">有所遺漏？</span><span class="sxs-lookup"><span data-stu-id="b7441-162">Something missing?</span></span> <span data-ttu-id="b7441-163">有所錯誤？</span><span class="sxs-lookup"><span data-stu-id="b7441-163">Something wrong?</span></span> <span data-ttu-id="b7441-164">我是否撰寫了令人混淆的內容？</span><span class="sxs-lookup"><span data-stu-id="b7441-164">Did I write something that's just confusing?</span></span> <span data-ttu-id="b7441-165">向上捲動並按一下 [在 GitHub 上編輯]  以進行變更 - 系統會顯示這些變更以供我們檢閱，而我們簽核後，您就會在這裡看到您所進行的變更和改良。</span><span class="sxs-lookup"><span data-stu-id="b7441-165">Scroll up and click **Edit on GitHub** to make changes - those will come to us for review, and then, once we sign off on them, you'll see your changes and improvements right here.</span></span>

