---
title: "aaaMigrate 使用者資料與 Azure RemoteApp |Microsoft 文件"
description: "深入了解如何 toomigrate 您的使用者資料和 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="9888d-103">如何 toomigrate 資料傳入活動和從 Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9888d-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9888d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="9888d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9888d-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9888d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9888d-106">您可以使用許多不同的工具和方法 tootransfer[使用者資料](remoteapp-upd.md)進出 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="9888d-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="9888d-107">以下是幾個方法︰</span><span class="sxs-lookup"><span data-stu-id="9888d-107">Here are a few methods:</span></span>

* <span data-ttu-id="9888d-108">使用剪貼簿共用複製並貼上</span><span class="sxs-lookup"><span data-stu-id="9888d-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="9888d-109">複製檔案和資料 tooa 檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="9888d-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="9888d-110">複製檔案 tooOneDrive 商務透過瀏覽器</span><span class="sxs-lookup"><span data-stu-id="9888d-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="9888d-111">使用重新導向複製檔案</span><span class="sxs-lookup"><span data-stu-id="9888d-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="9888d-112">您無法啟用 hello OneDrive for Business 或取用者的同步處理代理程式-它們[不支援](remoteapp-onedrive.md)Azure RemoteApp 中。</span><span class="sxs-lookup"><span data-stu-id="9888d-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="9888d-113">在 [檔案總管] 中使用複製及貼上</span><span class="sxs-lookup"><span data-stu-id="9888d-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="9888d-114">RemoteApp 部署中已啟用複製與貼上使用 hello 剪貼簿[預設](remoteapp-redirection.md)。</span><span class="sxs-lookup"><span data-stu-id="9888d-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="9888d-115">這可讓使用者在他們的本機電腦和 RemoteApp 應用程式之間複製檔案。</span><span class="sxs-lookup"><span data-stu-id="9888d-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="9888d-116">通常，hello 正常操作程序使用 RemoteApp 中的應用程式，透過使用者儲存檔案 tootheir Upd-移動 RemoteApp 中的資料很容易：</span><span class="sxs-lookup"><span data-stu-id="9888d-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="9888d-117">在 RemoteApp 集合中[將 [檔案總管] 發佈為應用程式](remoteapp-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="9888d-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="9888d-118">(請注意，這是系統管理工作。)</span><span class="sxs-lookup"><span data-stu-id="9888d-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="9888d-119">直接您使用者 toolaunch hello 檔案總管 中您發行應用程式和 toouse 該 toocopy 和貼上檔案到其 UPD 和不使用。</span><span class="sxs-lookup"><span data-stu-id="9888d-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="9888d-120">上傳檔案及資料 tooa 檔案伺服器，方法是使用標準網路檔案複本</span><span class="sxs-lookup"><span data-stu-id="9888d-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="9888d-121">通常組織使用檔案伺服器 toostore 一般資料。</span><span class="sxs-lookup"><span data-stu-id="9888d-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="9888d-122">如果您知道 hello 伺服器名稱或位置，您的使用者可以瀏覽 hello hello 伺服器的區域網路，並方式一樣上方，然後複製其檔案。</span><span class="sxs-lookup"><span data-stu-id="9888d-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="9888d-123">再次將想 toopublish 檔案總管 tooRemoteApp，然後分享您的使用者。</span><span class="sxs-lookup"><span data-stu-id="9888d-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="9888d-124">hello 檔案伺服器必須位於 RemoteApp 部署進入 hello 可路由網路上。</span><span class="sxs-lookup"><span data-stu-id="9888d-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="9888d-125">複製檔案 tooOneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="9888d-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="9888d-126">雖然您無法啟用 RemoteApp 的商務同步代理程式 」 的 hello OneDrive，您還是可以複製檔案從 UPD tooOneDrive 商務透過瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9888d-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="9888d-127">發行 tooRemoteApp 檔案總管]，然後告訴 [使用者 tooaccess hello 透過該應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="9888d-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="9888d-128">如果它是最簡單的 tootransfer 檔案壓縮，因此使用者應該建立.zip 檔案，其中包含所有 hello 檔案 toomove tooOneDrive 商務。</span><span class="sxs-lookup"><span data-stu-id="9888d-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="9888d-129">詢問使用者 toogo toohello Office 365 入口網站，並前往 tooOneDrive 及上傳 hello.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="9888d-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="9888d-130">使用磁碟重新導向複製檔案</span><span class="sxs-lookup"><span data-stu-id="9888d-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="9888d-131">如果您已啟用 [磁碟重新導向](remoteapp-redirection.md)，您已為您的使用者建立對應磁碟機。</span><span class="sxs-lookup"><span data-stu-id="9888d-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="9888d-132">在此情況下，它們可以 zip hello 重新導向磁碟機上的檔案，然後將它們儲存 tootheir 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="9888d-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="9888d-133">系統管理員如何匯出資料</span><span class="sxs-lookup"><span data-stu-id="9888d-133">How administrators can export data</span></span>

<span data-ttu-id="9888d-134">管理訂用帳戶 tooAzure 使用 Azure PowerShell 的儲存體中的所有集合的 Azure RemoteApp 可以匯出所有的使用者設定檔磁碟 (UPD) 的 cmdlet，匯出 AzureRemoteAppUserDisk。</span><span class="sxs-lookup"><span data-stu-id="9888d-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="9888d-135">沒有任何能力 tooselect 個別 UPD 的。</span><span class="sxs-lookup"><span data-stu-id="9888d-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="9888d-136">Hello PowerShell 命令執行時，每個使用者磁碟會為固定的磁碟大小的 50 gb，並匯出的 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9888d-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="9888d-137">會立即對此儲存體產生 Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="9888d-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="9888d-138">當執行這個命令，請確定沒有否則 hello 匯出將會失敗的工作階段。</span><span class="sxs-lookup"><span data-stu-id="9888d-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="9888d-139">只能在 RDS 部署中重新使用已加入網域之 Azure RemoteApp 部署的 UPD，並無法使用未加入網域的部署。</span><span class="sxs-lookup"><span data-stu-id="9888d-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="9888d-140">如果這些磁碟將會使用 RDS 部署建議 toouse 我們[自動化指令碼](https://github.com/arcadiahlyy/aramigration)，以便匯出、 轉換，並且 hello UPD 的匯入 RDS 部署。</span><span class="sxs-lookup"><span data-stu-id="9888d-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

