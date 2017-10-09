---
title: "自訂映像的 Azure RemoteApp aaaUpload |Microsoft 文件"
description: "了解如何 tooupload 自訂映像的 Azure RemoteApp"
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
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="937a2-103">上傳 Azure RemoteApp 的自訂映像</span><span class="sxs-lookup"><span data-stu-id="937a2-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="937a2-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="937a2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="937a2-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="937a2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="937a2-106">既然您已建立您的自訂範本映像，或已更新的變更，您需要 tooupload 該映像 tooyour Azure RemoteApp 映像庫。</span><span class="sxs-lookup"><span data-stu-id="937a2-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="937a2-107">使用這些步驟。</span><span class="sxs-lookup"><span data-stu-id="937a2-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="937a2-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="937a2-108">Before you start</span></span>
1. <span data-ttu-id="937a2-109">確認您的自訂映像符合 hello[映像需求](remoteapp-imagereqs.md)和[應用程式的需求](remoteapp-appreqs.md)。</span><span class="sxs-lookup"><span data-stu-id="937a2-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="937a2-110">安裝 hello [Azure PowerShell 模組](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="937a2-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="937a2-111">逐步解說有關 tooupload 自訂映像</span><span class="sxs-lookup"><span data-stu-id="937a2-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="937a2-112">開啟 Azure 管理入口網站，並瀏覽 toohello RemoteApp 頁面。</span><span class="sxs-lookup"><span data-stu-id="937a2-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="937a2-113">在 hello**範本映像**索引標籤上，按一下 **上傳**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="937a2-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="937a2-114">輸入您的映像的易記名稱並指定 hello 儲存體帳戶位置。</span><span class="sxs-lookup"><span data-stu-id="937a2-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="937a2-115">請 hello 位置 hello 與您的 RemoteApp 集合或想 toocreate 其中的位置相同的位置。</span><span class="sxs-lookup"><span data-stu-id="937a2-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="937a2-116">出現提示時，下載 hello 指令碼 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="937a2-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="937a2-117">複製 hello 命令參數中的 hello 文字方塊 tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="937a2-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="937a2-118">開啟提升權限的 Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="937a2-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="937a2-119">Hello 從提高權限的 Windows PowerShell 視窗中，瀏覽 toohello hello 指令碼的下載位置的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="937a2-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="937a2-120">貼上 hello 複製命令並按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="937a2-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="937a2-121">hello 上傳程序就會開始，持續時間取決於許多因素，包括您的網路速度和 hello 映像的大小</span><span class="sxs-lookup"><span data-stu-id="937a2-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="937a2-122">如果您上傳未成功因為網路中斷或項目類似的您一律可以繼續 hello 上傳程序開始。</span><span class="sxs-lookup"><span data-stu-id="937a2-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="937a2-123">tooresume 上傳，執行一次使用的 hello 指令碼 hello 相同命令列。</span><span class="sxs-lookup"><span data-stu-id="937a2-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="937a2-124">永遠不會修改 hello 上傳指令碼。</span><span class="sxs-lookup"><span data-stu-id="937a2-124">Never modify hello upload script.</span></span> <span data-ttu-id="937a2-125">指定檢查已實作 hello 映像符合 hello 映像需求和應用程式需求的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="937a2-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="937a2-126">常見問題</span><span class="sxs-lookup"><span data-stu-id="937a2-126">Common problems</span></span>
* <span data-ttu-id="937a2-127">請確定使用的是 Windows PowerShell，而不是 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="937a2-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="937a2-128">您需要 tooinstall hello Azure PowerShell 模組，因為某些模組會在必要時 hello 上傳程序。</span><span class="sxs-lookup"><span data-stu-id="937a2-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="937a2-129">永遠不會改變 hello 指令碼，驗證是為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="937a2-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="937a2-130">如果 hello vhd 檔案上傳期間取得鎖定，hello 檔案複製或移動它 tooa 新位置，並嘗試上傳一次。</span><span class="sxs-lookup"><span data-stu-id="937a2-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="937a2-131">有些 Windows 程序可能會阻止上傳。</span><span class="sxs-lookup"><span data-stu-id="937a2-131">There might be some Windows process that is preventing upload.</span></span>  

