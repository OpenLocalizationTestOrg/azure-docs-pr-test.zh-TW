---
title: "aaaAzure RemoteApp 映像需求 |Microsoft 文件"
description: "深入了解建立與 Azure RemoteApp 搭配使用的映像 toobe hello 需求"
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
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="f7fe1-103">Azure RemoteApp 映像的需求</span><span class="sxs-lookup"><span data-stu-id="f7fe1-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f7fe1-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f7fe1-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f7fe1-106">Azure RemoteApp 使用 Windows Server 2012 R2 的映像 toohost 所有 hello 程式，您會想 tooshare 與您的使用者。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="f7fe1-107">toocreate 自訂映像，您可以使用現有的映像開始或[建立一個新](remoteapp-create-custom-image.md)。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="f7fe1-108">您知道您 Azure RemoteApp 訂用帳戶可讓您存取 tooa Windows Server 2012 R2 的映像中 hello Azure VM 圖庫，您可以使用 toocreate 您自己的範本映像嗎？</span><span class="sxs-lookup"><span data-stu-id="f7fe1-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="f7fe1-109">[立即使用](remoteapp-image-on-azurevm.md)。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="f7fe1-110">可以上傳 Azure RemoteApp 搭配使用的 hello 映像的 hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="f7fe1-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="f7fe1-111">自訂應用程式不在本機儲存資料，hello 映像上。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="f7fe1-112">這些都是無狀態的映像，而且應該只包含應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="f7fe1-113">hello 影像未包含資料，可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="f7fe1-114">hello 映像大小應該是 mb/s 的倍數。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="f7fe1-115">如果您嘗試 tooupload 不精確的多個映像，hello 上傳將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="f7fe1-116">hello 影像大小必須為 127 GB 或更小。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="f7fe1-117">必須在 VHD 檔案上 (VHDX 檔案目前不受支援)。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="f7fe1-118">hello VHD 不能在第 2 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="f7fe1-119">hello VHD 可以是固定大小或動態擴充。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="f7fe1-120">因為它會採用比固定大小的 VHD 檔案的較少時間 tooupload tooAzure，建議您使用動態擴充的 VHD。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="f7fe1-121">必須使用 hello 主開機記錄 (MBR) 磁碟分割樣式初始化磁碟 hello。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="f7fe1-122">不支援 hello GUID 磁碟分割表格 (GPT) 磁碟分割樣式。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="f7fe1-123">hello VHD 必須包含單一 Windows Server 2012 R2 的安裝。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="f7fe1-124">它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="f7fe1-125">必須安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="f7fe1-126">hello 遠端桌面連線代理人角色必須*不*安裝。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="f7fe1-127">必須停用 hello 加密檔案系統 (EFS)。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="f7fe1-128">hello 映像必須使用 hello 參數 SYSPREPed **/oobe /generalize /shutdown** (請勿使用 hello **/mode: vm**參數)。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="f7fe1-129">不支援從快照鏈結上傳您 VHD。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="f7fe1-130">如需建立 Azure RemoteApp 映像的詳細資訊，請參閱 [建立 Azure RemoteApp 映像](remoteapp-imageoptions.md) 。</span><span class="sxs-lookup"><span data-stu-id="f7fe1-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

