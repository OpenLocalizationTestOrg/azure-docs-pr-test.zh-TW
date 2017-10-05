---
title: "上傳 Azure RemoteApp 的自訂映像 | Microsoft Docs"
description: "了解如何上傳 Azure RemoteApp 的自訂映像"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="00d3f-103">上傳 Azure RemoteApp 的自訂映像</span><span class="sxs-lookup"><span data-stu-id="00d3f-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="00d3f-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="00d3f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="00d3f-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="00d3f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="00d3f-106">現在，您已建立自訂範本映像或已更新變更，您必須將該映像上傳至您的 Azure RemoteApp 映像庫。</span><span class="sxs-lookup"><span data-stu-id="00d3f-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="00d3f-107">使用這些步驟。</span><span class="sxs-lookup"><span data-stu-id="00d3f-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="00d3f-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="00d3f-108">Before you start</span></span>
1. <span data-ttu-id="00d3f-109">請確認您的自訂映像符合[映像需求](remoteapp-imagereqs.md)和[應用程式需求](remoteapp-appreqs.md)。</span><span class="sxs-lookup"><span data-stu-id="00d3f-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="00d3f-110">安裝 [Azure PowerShell 模組](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="00d3f-110">Install the [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="00d3f-111">逐步解說如何上傳自訂映像</span><span class="sxs-lookup"><span data-stu-id="00d3f-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="00d3f-112">開啟 Azure 管理入口網站，並瀏覽至 [RemoteApp] 頁面。</span><span class="sxs-lookup"><span data-stu-id="00d3f-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="00d3f-113">在 [範本映像] 索引標籤上，按一下頁面底部的 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="00d3f-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="00d3f-114">為您的映像輸入一個易記名稱，並指定儲存體帳戶位置。</span><span class="sxs-lookup"><span data-stu-id="00d3f-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="00d3f-115">請確定此位置會是與 RemoteApp 集合相同的位置或是您要建立 RemoteApp 集合的位置。</span><span class="sxs-lookup"><span data-stu-id="00d3f-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="00d3f-116">當系統出現提示時，請將指令碼下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="00d3f-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="00d3f-117">將文字方塊中的命令參數複製到您的剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="00d3f-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="00d3f-118">開啟提升權限的 Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="00d3f-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="00d3f-119">從提升權限的 Windows PowerShell 視窗，瀏覽至您下載指令碼的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="00d3f-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="00d3f-120">貼上複製的命令，並按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="00d3f-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="00d3f-121">系統便會開始上傳程序，持續時間會取決於許多因素，其中包括您的網路速度和影像的大小</span><span class="sxs-lookup"><span data-stu-id="00d3f-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="00d3f-122">如果因為網路中斷或類似原因導致上傳失敗，您可以繼續您已開始的上傳程序。</span><span class="sxs-lookup"><span data-stu-id="00d3f-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="00d3f-123">若要繼續上傳，您可以再次使用相同的命令列來執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="00d3f-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="00d3f-124">切勿修改上傳指令碼。</span><span class="sxs-lookup"><span data-stu-id="00d3f-124">Never modify the upload script.</span></span> <span data-ttu-id="00d3f-125">已實作可確保映像符合映像需求和應用程式需求的特定檢查。</span><span class="sxs-lookup"><span data-stu-id="00d3f-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="00d3f-126">常見問題</span><span class="sxs-lookup"><span data-stu-id="00d3f-126">Common problems</span></span>
* <span data-ttu-id="00d3f-127">請確定使用的是 Windows PowerShell，而不是 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="00d3f-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="00d3f-128">您必須安裝 Azure PowerShell 模組，因為上傳過程中會需要某些特定模組。</span><span class="sxs-lookup"><span data-stu-id="00d3f-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="00d3f-129">切勿更改指令碼，該指令碼已提供驗證，方便您使用。</span><span class="sxs-lookup"><span data-stu-id="00d3f-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="00d3f-130">如果 vhd 檔案在上傳期間遭到鎖定，請將檔案複製或移動到新位置，並再次嘗試上傳。</span><span class="sxs-lookup"><span data-stu-id="00d3f-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="00d3f-131">有些 Windows 程序可能會阻止上傳。</span><span class="sxs-lookup"><span data-stu-id="00d3f-131">There might be some Windows process that is preventing upload.</span></span>  

