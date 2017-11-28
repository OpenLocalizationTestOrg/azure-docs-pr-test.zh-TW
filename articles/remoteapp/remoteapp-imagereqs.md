---
title: "Azure RemoteApp 映像需求 | Microsoft Docs"
description: "深入了解建立可用於 Azure RemoteApp 的映像需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="cfbdf-103">Azure RemoteApp 映像的需求</span><span class="sxs-lookup"><span data-stu-id="cfbdf-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cfbdf-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cfbdf-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cfbdf-106">Azure RemoteApp 會使用 Windows Server 2012 R2 映像來主控您要與使用者共用的所有程式。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="cfbdf-107">若要建立自訂映像，您可以從現有的映像建立，或 [建立新映像](remoteapp-create-custom-image.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="cfbdf-108">您是否知道 Azure RemoteApp 訂用帳戶可讓您存取 Azure VM 資源庫中可用來建立專屬範本映像的 Windows Server 2012 R2 映像？</span><span class="sxs-lookup"><span data-stu-id="cfbdf-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="cfbdf-109">[立即使用](remoteapp-image-on-azurevm.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="cfbdf-110">可上傳用於 Azure RemoteApp 的映像有下列需求：</span><span class="sxs-lookup"><span data-stu-id="cfbdf-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="cfbdf-111">自訂應用程式不會在映像上本機儲存資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="cfbdf-112">這些都是無狀態的映像，而且應該只包含應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="cfbdf-113">映像不包含可能會遺失的資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="cfbdf-114">映像大小應為 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="cfbdf-115">如果您嘗試上傳的映像大小不是正確的倍數，上傳作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="cfbdf-116">映像大小必須為 127 GB 或更小。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="cfbdf-117">必須在 VHD 檔案上 (VHDX 檔案目前不受支援)。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="cfbdf-118">VHD 不能是第 2 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="cfbdf-119">VHD 可以固定大小或動態擴充。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="cfbdf-120">建議採用動態擴充 VHD 的做法，因為這會比固定大小 VHD 檔案更快速地上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="cfbdf-121">磁碟必須使用主開機記錄 (MBR) 分割樣式進行初始化。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="cfbdf-122">GUID 磁碟分割資料表 (GPT) 磁碟分割樣式不受支援。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="cfbdf-123">VHD 必須包含單一 Windows Server 2012 R2 安裝。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="cfbdf-124">它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="cfbdf-125">必須安裝「遠端桌面工作階段主機 (RDSH)」角色和「桌面體驗」功能。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="cfbdf-126">*請勿* 安裝「遠端桌面連線代理人」角色。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="cfbdf-127">必須停用「加密檔案系統 (EFS)」。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="cfbdf-128">映像必須使用參數 **/oobe /generalize /shutdown** 進行 SYSPREP 處理 (請不要使用 **/mode:vm** 參數)。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="cfbdf-129">不支援從快照鏈結上傳您 VHD。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="cfbdf-130">如需建立 Azure RemoteApp 映像的詳細資訊，請參閱 [建立 Azure RemoteApp 映像](remoteapp-imageoptions.md) 。</span><span class="sxs-lookup"><span data-stu-id="cfbdf-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

