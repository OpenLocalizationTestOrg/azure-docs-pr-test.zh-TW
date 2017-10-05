---
title: "從 Azure RemoteApp 移轉使用者資料 | Microsoft Docs"
description: "了解如何將使用者資料轉入或轉出 Azure RemoteApp。"
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
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="7d237-103">如何將資料轉入或轉出 Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7d237-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d237-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7d237-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7d237-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="7d237-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7d237-106">您可以使用許多不同的工具和方法，將 [使用者資料](remoteapp-upd.md) 傳入和傳出 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="7d237-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="7d237-107">以下是幾個方法︰</span><span class="sxs-lookup"><span data-stu-id="7d237-107">Here are a few methods:</span></span>

* <span data-ttu-id="7d237-108">使用剪貼簿共用複製並貼上</span><span class="sxs-lookup"><span data-stu-id="7d237-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="7d237-109">將檔案和資料複製到檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="7d237-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="7d237-110">透過瀏覽器，將檔案複製到商務用 OneDrive</span><span class="sxs-lookup"><span data-stu-id="7d237-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="7d237-111">使用重新導向複製檔案</span><span class="sxs-lookup"><span data-stu-id="7d237-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="7d237-112">您無法啟用商務用 OneDrive 或消費者同步處理代理程式 - Azure RemoteApp 中 [不支援](remoteapp-onedrive.md) 。</span><span class="sxs-lookup"><span data-stu-id="7d237-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="7d237-113">在 [檔案總管] 中使用複製及貼上</span><span class="sxs-lookup"><span data-stu-id="7d237-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="7d237-114">[依預設](remoteapp-redirection.md)，RemoteApp 部署中已啟用使用剪貼簿複製和貼上。</span><span class="sxs-lookup"><span data-stu-id="7d237-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="7d237-115">這可讓使用者在他們的本機電腦和 RemoteApp 應用程式之間複製檔案。</span><span class="sxs-lookup"><span data-stu-id="7d237-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="7d237-116">通常，透過在 RemoteApp 中使用應用程式的正常過程，使用者已將檔案儲存到他們的 UPD - 將該資料移出 RemoteApp 很容易：</span><span class="sxs-lookup"><span data-stu-id="7d237-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="7d237-117">在 RemoteApp 集合中[將 [檔案總管] 發佈為應用程式](remoteapp-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="7d237-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="7d237-118">(請注意，這是系統管理工作。)</span><span class="sxs-lookup"><span data-stu-id="7d237-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="7d237-119">將使用者導向至啟動您所發佈的 [檔案總管] 應用程式，並使用它來從其 UPD 複製與貼上檔案。</span><span class="sxs-lookup"><span data-stu-id="7d237-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="7d237-120">透過使用標準網路檔案複製將檔案與資料上傳至檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="7d237-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="7d237-121">通常組織會使用檔案伺服器儲存一般資料。</span><span class="sxs-lookup"><span data-stu-id="7d237-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="7d237-122">如果您知道伺服器名稱或位置，您的使用者可以瀏覽伺服器的區域網路，並複製他們的檔案，類似他們上述的作法。</span><span class="sxs-lookup"><span data-stu-id="7d237-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="7d237-123">同樣的，您會希望將 [檔案總管] 發佈至 RemoteApp，然後與您的使用者共用。</span><span class="sxs-lookup"><span data-stu-id="7d237-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="7d237-124">檔案伺服器必須位在部署 RemoteApp 的可路由網路上。</span><span class="sxs-lookup"><span data-stu-id="7d237-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="7d237-125">將檔案複製到商務用 OneDrive</span><span class="sxs-lookup"><span data-stu-id="7d237-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="7d237-126">雖然您無法在 RemoteApp 中啟用商務用 OneDrive 同步代理程式，您仍然可以透過瀏覽器將檔案從您的 UPD 複製到商務用 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="7d237-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="7d237-127">將 [檔案總管] 發佈至 RemoteApp，然後告知使用者透過該應用程式存取檔案。</span><span class="sxs-lookup"><span data-stu-id="7d237-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="7d237-128">如果檔案已壓縮會更容易傳輸，因此使用者應該建立一個包含所有檔案的 .zip 檔案，以移動至商務用 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="7d237-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="7d237-129">要求使用者移至 Office 365 入口網站，然後移至 OneDrive 並上傳該 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d237-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="7d237-130">使用磁碟重新導向複製檔案</span><span class="sxs-lookup"><span data-stu-id="7d237-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="7d237-131">如果您已啟用 [磁碟重新導向](remoteapp-redirection.md)，您已為您的使用者建立對應磁碟機。</span><span class="sxs-lookup"><span data-stu-id="7d237-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="7d237-132">在此情況下，他們可以在已重新導向的磁碟機上壓縮他們的檔案，然後儲存到他們的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d237-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="7d237-133">系統管理員如何匯出資料</span><span class="sxs-lookup"><span data-stu-id="7d237-133">How administrators can export data</span></span>

<span data-ttu-id="7d237-134">Azure RemoteApp 的管理員可以使用 Azure PowerShell Cmdlet Export-AzureRemoteAppUserDisk，匯出 Azure 儲存體訂用帳戶內所有集合的所有使用者設定檔磁碟 (UPD)。</span><span class="sxs-lookup"><span data-stu-id="7d237-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="7d237-135">無法選取個別 UPD。</span><span class="sxs-lookup"><span data-stu-id="7d237-135">There is no ability to select individual UPD's.</span></span>  <span data-ttu-id="7d237-136">執行 PowerShell 命令時，每個使用者磁碟的固定磁碟大小都會是 50 GB，並且會匯出至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d237-136">When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.</span></span>  <span data-ttu-id="7d237-137">會立即對此儲存體產生 Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="7d237-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="7d237-138">執行此命令時，請確定沒有工作階段，否則匯出會失敗。</span><span class="sxs-lookup"><span data-stu-id="7d237-138">When running this command ensure there are no sessions otherwise the export will fail.</span></span>

<span data-ttu-id="7d237-139">只能在 RDS 部署中重新使用已加入網域之 Azure RemoteApp 部署的 UPD，並無法使用未加入網域的部署。</span><span class="sxs-lookup"><span data-stu-id="7d237-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="7d237-140">如果這些磁碟將用於 RDS 部署中，建議使用[自動化指令碼](https://github.com/arcadiahlyy/aramigration)，以匯出、轉換並將 UPD 匯入 RDS 部署。</span><span class="sxs-lookup"><span data-stu-id="7d237-140">If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.</span></span>

