---
title: "StorSimple Virtual Array 的 aaaPortal 準備 |Microsoft 文件"
description: "第一個教學課程 toodeploy StorSimple 虛擬陣列包括準備 hello Azure 入口網站"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a><span data-ttu-id="26f1e-103">部署 StorSimple 虛擬陣列-準備 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="26f1e-103">Deploy StorSimple Virtual Array - Prepare hello Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="26f1e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="26f1e-104">Overview</span></span>

<span data-ttu-id="26f1e-105">這是 hello 第一篇文章 hello 數列中的 部署教學課程所需 toocompletely 部署您的虛擬陣列做為檔案伺服器或 iSCSI 伺服器使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="26f1e-105">This is hello first article in hello series of deployment tutorials required toocompletely deploy your virtual array as a file server or an iSCSI server using hello Resource Manager model.</span></span> <span data-ttu-id="26f1e-106">本文描述 hello 所需的準備 toocreate，並設定您 StorSimple 裝置管理員服務之前 tooprovisioning 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="26f1e-106">This article describes hello preparation required toocreate and configure your StorSimple Device Manager service prior tooprovisioning a virtual array.</span></span> <span data-ttu-id="26f1e-107">本文也會連結出 tooa 部署組態檢查清單及設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="26f1e-107">This article also links out tooa deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="26f1e-108">您需要系統管理員權限 toocomplete hello 安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="26f1e-108">You need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="26f1e-109">我們建議您先檢閱 hello 部署組態檢查清單。</span><span class="sxs-lookup"><span data-stu-id="26f1e-109">We recommend that you review hello deployment configuration checklist before you begin.</span></span> <span data-ttu-id="26f1e-110">hello 入口網站的準備工作會小於 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="26f1e-110">hello portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="26f1e-111">這篇文章中發行的 hello 資訊適用於 StorSimple hello Azure 入口網站中的虛擬陣列和 Microsoft Azure 政府雲端 toohello 部署。</span><span class="sxs-lookup"><span data-stu-id="26f1e-111">hello information published in this article applies toohello deployment of StorSimple Virtual Arrays in hello Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="26f1e-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="26f1e-112">Get started</span></span>
<span data-ttu-id="26f1e-113">hello 部署工作流程包含準備 hello 入口網站中，佈建您的虛擬化環境中的虛擬陣列和 hello 安裝完成。</span><span class="sxs-lookup"><span data-stu-id="26f1e-113">hello deployment workflow consists of preparing hello portal, provisioning a virtual array in your virtualized environment, and completing hello setup.</span></span> <span data-ttu-id="26f1e-114">tooget 入門 hello StorSimple Virtual Array 部署為檔案伺服器或 iSCSI 伺服器，您需要下列資料表的資源 toorefer toohello。</span><span class="sxs-lookup"><span data-stu-id="26f1e-114">tooget started with hello StorSimple Virtual Array deployment as a file server or an iSCSI server, you need toorefer toohello following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="26f1e-115">部署相關文章</span><span class="sxs-lookup"><span data-stu-id="26f1e-115">Deployment articles</span></span>

<span data-ttu-id="26f1e-116">toodeploy StorSimple 虛擬陣列，請參閱下列文章中 hello 規定順序 toohello。</span><span class="sxs-lookup"><span data-stu-id="26f1e-116">toodeploy your StorSimple Virtual Array, refer toohello following articles in hello prescribed sequence.</span></span>

| **#** | <span data-ttu-id="26f1e-117">**在此步驟中**</span><span class="sxs-lookup"><span data-stu-id="26f1e-117">**In this step**</span></span> | <span data-ttu-id="26f1e-118">**執行此動作...**</span><span class="sxs-lookup"><span data-stu-id="26f1e-118">**You do this …**</span></span> | <span data-ttu-id="26f1e-119">**並使用這些文件。**</span><span class="sxs-lookup"><span data-stu-id="26f1e-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26f1e-120">1.</span><span class="sxs-lookup"><span data-stu-id="26f1e-120">1.</span></span> |<span data-ttu-id="26f1e-121">**設定 hello Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="26f1e-121">**Set up hello Azure portal**</span></span> |<span data-ttu-id="26f1e-122">建立並設定您 StorSimple 裝置管理員服務之前 tooprovisioning StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="26f1e-122">Create and configure your StorSimple Device Manager service prior tooprovisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="26f1e-123">準備 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="26f1e-123">Prepare hello portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="26f1e-124">2.</span><span class="sxs-lookup"><span data-stu-id="26f1e-124">2.</span></span> |<span data-ttu-id="26f1e-125">**佈建 hello 虛擬陣列**</span><span class="sxs-lookup"><span data-stu-id="26f1e-125">**Provision hello Virtual Array**</span></span> |<span data-ttu-id="26f1e-126">HYPER-V，佈建，並連接 tooa StorSimple Virtual Array 在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。</span><span class="sxs-lookup"><span data-stu-id="26f1e-126">For Hyper-V, provision and connect tooa StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="26f1e-127">適用於 VMware，佈建，並連接 tooa StorSimple Virtual Array 和更新版本上執行 VMware ESXi 5.5 主機系統。</span><span class="sxs-lookup"><span data-stu-id="26f1e-127">For VMware, provision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="26f1e-128">在 Hyper-V 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="26f1e-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="26f1e-129">在 VMware 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="26f1e-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="26f1e-130">3.</span><span class="sxs-lookup"><span data-stu-id="26f1e-130">3.</span></span> |<span data-ttu-id="26f1e-131">**設定 hello 虛擬陣列**</span><span class="sxs-lookup"><span data-stu-id="26f1e-131">**Set up hello Virtual Array**</span></span> |<span data-ttu-id="26f1e-132">檔案伺服器，執行初始設定，註冊您的 StorSimple 檔案伺服器，並完成 hello 裝置設定。</span><span class="sxs-lookup"><span data-stu-id="26f1e-132">For your file server, perform initial setup, register your StorSimple file server, and complete hello device setup.</span></span> <span data-ttu-id="26f1e-133">接下來，您可以佈建 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="26f1e-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="26f1e-134">為您的 iSCSI 伺服器執行初始設定，註冊您的 StorSimple iSCSI 伺服器，並完成 hello 裝置設定。</span><span class="sxs-lookup"><span data-stu-id="26f1e-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete hello device setup.</span></span> <span data-ttu-id="26f1e-135">接下來，您可以佈建 iSCSI 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="26f1e-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="26f1e-136">將虛擬陣列設定為檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="26f1e-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="26f1e-137">將虛擬陣列設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="26f1e-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="26f1e-138">您現在可以開始 tooset 向上 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="26f1e-138">You can now begin tooset up hello Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="26f1e-139">設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="26f1e-139">Configuration checklist</span></span>

<span data-ttu-id="26f1e-140">hello 組態檢查清單描述在您的 StorSimple Virtual Array 設定 hello 軟體之前，需要 toocollect hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="26f1e-140">hello configuration checklist describes hello information that you need toocollect before you configure hello software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="26f1e-141">正在準備時間有助於此資訊的部署環境中的 hello StorSimple 裝置的簡化 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="26f1e-141">Preparing this information ahead of time helps streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="26f1e-142">根據您的 StorSimple Virtual Array 是否為檔案伺服器或 iSCSI 伺服器部署，需要一個 hello 下列檢查清單。</span><span class="sxs-lookup"><span data-stu-id="26f1e-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of hello following checklists.</span></span>

* <span data-ttu-id="26f1e-143">下載 hello [StorSimple 虛擬陣列檔案伺服器設定檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-143">Download hello [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="26f1e-144">下載 hello [StorSimple Virtual Array iSCSI 伺服器組態檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-144">Download hello [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26f1e-145">必要條件</span><span class="sxs-lookup"><span data-stu-id="26f1e-145">Prerequisites</span></span>

<span data-ttu-id="26f1e-146">您在這裡找到您的 StorSimple 裝置管理員服務、 StorSimple Virtual Array 和 hello 資料中心網路的 hello 組態必要條件。</span><span class="sxs-lookup"><span data-stu-id="26f1e-146">Here you find hello configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and hello datacenter network.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="26f1e-147">Hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="26f1e-147">For hello StorSimple Device Manager service</span></span>

<span data-ttu-id="26f1e-148">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="26f1e-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="26f1e-149">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="26f1e-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="26f1e-150">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="26f1e-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="26f1e-151">您的 Microsoft Azure 訂用帳戶應該已啟用來使用 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="26f1e-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="26f1e-152">Hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="26f1e-152">For hello StorSimple Virtual Array</span></span>

<span data-ttu-id="26f1e-153">在您部署虛擬陣列之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="26f1e-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="26f1e-154">您可以存取 tooa 主機系統執行 HYPER-V 的 Windows Server 2008 R2 或更新版本，或是 VMware (ESXi 5.5 或更新版本) 可以使用的 tooa 佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="26f1e-154">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="26f1e-155">hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="26f1e-155">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>
  
  * <span data-ttu-id="26f1e-156">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="26f1e-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="26f1e-157">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="26f1e-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="26f1e-158">如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="26f1e-158">If you plan tooconfigure hello virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="26f1e-159">您需要 16 GB RAM toosupport 2-4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="26f1e-159">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="26f1e-160">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="26f1e-160">One network interface.</span></span>
  * <span data-ttu-id="26f1e-161">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="26f1e-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-datacenter-network"></a><span data-ttu-id="26f1e-162">Hello 資料中心網路</span><span class="sxs-lookup"><span data-stu-id="26f1e-162">For hello datacenter network</span></span>

<span data-ttu-id="26f1e-163">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="26f1e-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="26f1e-164">資料中心中的 hello 網路設定根據您的 StorSimple 裝置 hello 網路需求。</span><span class="sxs-lookup"><span data-stu-id="26f1e-164">hello network in your datacenter is configured as per hello networking requirements for your StorSimple device.</span></span> <span data-ttu-id="26f1e-165">如需詳細資訊，請參閱 hello [StorSimple 虛擬陣列系統需求](storsimple-ova-system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-165">For more information, see hello [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="26f1e-166">StorSimple Virtual Array 隨時都有專用的 5 Mbps 網際網路頻寬 (或更多) 可用。</span><span class="sxs-lookup"><span data-stu-id="26f1e-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="26f1e-167">此頻寬不應與任何其他應用程式共用。</span><span class="sxs-lookup"><span data-stu-id="26f1e-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="26f1e-168">逐步的準備程序</span><span class="sxs-lookup"><span data-stu-id="26f1e-168">Step-by-step preparation</span></span>

<span data-ttu-id="26f1e-169">使用您的入口網站 hello 遵循逐步指示 tooprepare hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="26f1e-169">Use hello following step-by-step instructions tooprepare your portal for hello StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="26f1e-170">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="26f1e-170">Step 1: Create a new service</span></span>

<span data-ttu-id="26f1e-171">Hello StorSimple 裝置管理員服務的單一執行個體可以管理多個 StorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="26f1e-171">A single instance of hello StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="26f1e-172">執行下列步驟 toocreate hello StorSimple 裝置管理員服務的執行個體的 hello。</span><span class="sxs-lookup"><span data-stu-id="26f1e-172">Perform hello following steps toocreate an instance of hello StorSimple Device Manager service.</span></span> <span data-ttu-id="26f1e-173">如果您有現有的 StorSimple 裝置管理員服務 toomanage 您的虛擬陣列，略過此步驟中，然後太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-173">If you have an existing StorSimple Device Manager service toomanage your virtual arrays, skip this step and go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="26f1e-174">如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。</span><span class="sxs-lookup"><span data-stu-id="26f1e-174">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="26f1e-175">如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#optional-step-configure-a-new-storage-account-for-the-service)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="26f1e-175">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="26f1e-176">如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-176">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="26f1e-177">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="26f1e-177">Step 2: Get hello service registration key</span></span>

<span data-ttu-id="26f1e-178">Hello StorSimple 裝置管理員服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="26f1e-178">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="26f1e-179">這個金鑰是使用的 tooregister，而且與 hello 服務連接您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="26f1e-179">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="26f1e-180">執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-180">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="26f1e-181">hello 服務註冊金鑰是使用的 tooregister 所有 hello 必須與您的 StorSimple 裝置管理員服務 tooregister StorSimple 裝置管理員裝置。</span><span class="sxs-lookup"><span data-stu-id="26f1e-181">hello service registration key is used tooregister all hello StorSimple Device Manager devices that need tooregister with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a><span data-ttu-id="26f1e-182">步驟 3： 下載 hello 虛擬陣列映像</span><span class="sxs-lookup"><span data-stu-id="26f1e-182">Step 3: Download hello virtual array image</span></span>

<span data-ttu-id="26f1e-183">您已擁有 hello 服務註冊金鑰之後，您必須 toodownload hello 適當的虛擬陣列映像 tooprovision 虛擬陣列主機系統上。</span><span class="sxs-lookup"><span data-stu-id="26f1e-183">After you have hello service registration key, you will need toodownload hello appropriate virtual array image tooprovision a virtual array on your host system.</span></span> <span data-ttu-id="26f1e-184">hello 虛擬陣列影像都是特定的作業系統，而且可以從 hello Azure 入口網站中的 hello 快速入門頁面下載。</span><span class="sxs-lookup"><span data-stu-id="26f1e-184">hello virtual array images are operating system specific and can be downloaded from hello Quick Start page in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26f1e-185">hello StorSimple Virtual Array 上所執行的 hello 軟體只能搭配 hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="26f1e-185">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="26f1e-186">執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-186">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="tooget-hello-virtual-array-image"></a><span data-ttu-id="26f1e-187">tooget hello 虛擬陣列映像</span><span class="sxs-lookup"><span data-stu-id="26f1e-187">tooget hello virtual array image</span></span>

1. <span data-ttu-id="26f1e-188">登入 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="26f1e-188">Sign into hello [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="26f1e-189">在 hello Azure 入口網站，按一下 **瀏覽 > StorSimple 裝置管理員**。</span><span class="sxs-lookup"><span data-stu-id="26f1e-189">In hello Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="26f1e-190">選取現有的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="26f1e-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="26f1e-191">在 hello **StorSimple 裝置管理員**刀鋒視窗中，按一下 **快速入門**。</span><span class="sxs-lookup"><span data-stu-id="26f1e-191">In hello **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="26f1e-192">按一下 hello 連結對應 toohello 映像您想要從 Microsoft 下載中心 hello toodownload。</span><span class="sxs-lookup"><span data-stu-id="26f1e-192">Click hello link corresponding toohello image that you want toodownload from hello Microsoft Download Center.</span></span> <span data-ttu-id="26f1e-193">hello 映像檔案是大約 4.8 GB。</span><span class="sxs-lookup"><span data-stu-id="26f1e-193">hello image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="26f1e-194">VHDX (適用於 Windows Server 2012 及更新版本上的 Hyper-V)</span><span class="sxs-lookup"><span data-stu-id="26f1e-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="26f1e-195">VHD (適用於 Windows Server 2008 R2 及更新版本上的 Hyper-V)</span><span class="sxs-lookup"><span data-stu-id="26f1e-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="26f1e-196">VMDK (適用於 VMWare ESXi 5.5 及更新版本)</span><span class="sxs-lookup"><span data-stu-id="26f1e-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="26f1e-197">下載並解壓縮 hello 檔案 tooa 本機磁碟機，記下 hello 解壓縮的檔案所在的位置。</span><span class="sxs-lookup"><span data-stu-id="26f1e-197">Download and unzip hello file tooa local drive, making a note of where hello unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="26f1e-198">選擇性步驟： 設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="26f1e-198">Optional step: Configure a new storage account for hello service</span></span>

<span data-ttu-id="26f1e-199">此步驟為選擇性，而且您並未啟用 hello 自動建立儲存體帳戶與您的服務時，才應執行。</span><span class="sxs-lookup"><span data-stu-id="26f1e-199">This step is optional and should be performed only if you did not enable hello automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="26f1e-200">如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="26f1e-200">If you need toocreate an Azure storage account in a different region, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="26f1e-201">執行下列步驟在 hello hello [Azure 入口網站](https://ms.portal.azure.com/)hello StorSimple 裝置管理員服務頁面 tooadd 現有的 Microsoft Azure 儲存體帳戶上。</span><span class="sxs-lookup"><span data-stu-id="26f1e-201">Perform hello following steps in hello [Azure portal](https://ms.portal.azure.com/) on hello StorSimple Device Manager service page tooadd an existing Microsoft Azure storage account.</span></span>

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a><span data-ttu-id="26f1e-202">儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="26f1e-202">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>

1. <span data-ttu-id="26f1e-203">瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="26f1e-203">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="26f1e-204">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="26f1e-204">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="26f1e-205">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="26f1e-205">Select **Storage account credentials** within hello **Configuration** section.</span></span>
3. <span data-ttu-id="26f1e-206">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="26f1e-206">Click **Add**.</span></span>
4. <span data-ttu-id="26f1e-207">在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="26f1e-207">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="26f1e-208">在 [訂用帳戶] 中，選取 [目前]。</span><span class="sxs-lookup"><span data-stu-id="26f1e-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="26f1e-209">提供 hello Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="26f1e-209">Provide hello name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="26f1e-210">選取**啟用**toocreate StorSimple 裝置與 hello 雲端之間的網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="26f1e-210">Select **Enable** toocreate a secure channel for network communication between your StorSimple device and hello cloud.</span></span> <span data-ttu-id="26f1e-211">只有當您在私人雲端內操作時，才選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="26f1e-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="26f1e-212">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="26f1e-212">Click **Add**.</span></span> <span data-ttu-id="26f1e-213">已成功建立 hello 儲存體帳戶之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="26f1e-213">You are notified after hello storage account is successfully created.</span></span><br></br>
   
     ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="26f1e-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26f1e-215">Next step</span></span>

<span data-ttu-id="26f1e-216">hello 下一個步驟是 tooprovision 是您的 StorSimple Virtual Array 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26f1e-216">hello next step is tooprovision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="26f1e-217">根據您主機的作業系統，請參閱 hello 詳細中的指示：</span><span class="sxs-lookup"><span data-stu-id="26f1e-217">Depending on your host operating system, see hello detailed instructions in:</span></span>

* [<span data-ttu-id="26f1e-218">在 Hyper-V 中佈建 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="26f1e-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="26f1e-219">在 VMware 中佈建 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="26f1e-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

