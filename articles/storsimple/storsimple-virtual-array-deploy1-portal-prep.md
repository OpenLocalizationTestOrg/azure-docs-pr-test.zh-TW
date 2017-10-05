---
title: "為 StorSimple Virtual Array 準備入口網站 | Microsoft Docs"
description: "部署 StorSimple Virtual Array 的第一個教學課程，內容為如何準備 Azure 入口網站"
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
ms.openlocfilehash: 3d0801053721f98ce7a2b0fcbe3c65da8dbdd8d3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-the-azure-portal"></a><span data-ttu-id="db8ef-103">部署 StorSimple Virtual Array - 準備 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="db8ef-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="db8ef-104">概觀</span><span class="sxs-lookup"><span data-stu-id="db8ef-104">Overview</span></span>

<span data-ttu-id="db8ef-105">我們提供一系列如何將虛擬陣列完全部署為檔案伺服器或 iSCSI 伺服器 (使用 Resource Manager 模型) 的佈署教學課程，而這是該系列的第一篇文章。</span><span class="sxs-lookup"><span data-stu-id="db8ef-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span></span> <span data-ttu-id="db8ef-106">本文章說明在佈建虛擬陣列之前，要建立並設定 StorSimple 裝置管理員服務所需的準備工作。</span><span class="sxs-lookup"><span data-stu-id="db8ef-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span></span> <span data-ttu-id="db8ef-107">本文章也連結到部署設定檢查清單及設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="db8ef-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="db8ef-108">您需要有系統管理員權限，才能完成安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="db8ef-108">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="db8ef-109">我們建議您在開始之前，先檢閱部署設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="db8ef-109">We recommend that you review the deployment configuration checklist before you begin.</span></span> <span data-ttu-id="db8ef-110">入口網站準備工作不到 10 分鐘就能完成。</span><span class="sxs-lookup"><span data-stu-id="db8ef-110">The portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="db8ef-111">本文中發佈的資訊適用於在 Azure 入口網站及 Microsoft Azure 政府服務雲端部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="db8ef-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="db8ef-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="db8ef-112">Get started</span></span>
<span data-ttu-id="db8ef-113">部署的工作流程包括準備入口網站、在您的虛擬環境中佈建虛擬陣列，以及完成安裝程序。</span><span class="sxs-lookup"><span data-stu-id="db8ef-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span></span> <span data-ttu-id="db8ef-114">若要開始將 StorSimple Virtual Array 部署為檔案伺服器和 iSCSI 伺服器，您必須參閱下表中的資源。</span><span class="sxs-lookup"><span data-stu-id="db8ef-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="db8ef-115">部署相關文章</span><span class="sxs-lookup"><span data-stu-id="db8ef-115">Deployment articles</span></span>

<span data-ttu-id="db8ef-116">若要部署 StorSimple Virtual Array，請依指定的順序參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="db8ef-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span></span>

| **#** | <span data-ttu-id="db8ef-117">**在此步驟中**</span><span class="sxs-lookup"><span data-stu-id="db8ef-117">**In this step**</span></span> | <span data-ttu-id="db8ef-118">**執行此動作...**</span><span class="sxs-lookup"><span data-stu-id="db8ef-118">**You do this …**</span></span> | <span data-ttu-id="db8ef-119">**並使用這些文件。**</span><span class="sxs-lookup"><span data-stu-id="db8ef-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db8ef-120">1.</span><span class="sxs-lookup"><span data-stu-id="db8ef-120">1.</span></span> |<span data-ttu-id="db8ef-121">**設定 Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="db8ef-121">**Set up the Azure portal**</span></span> |<span data-ttu-id="db8ef-122">在佈建 StorSimple Virtual Array 之前，建立並設定 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="db8ef-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="db8ef-123">準備入口網站</span><span class="sxs-lookup"><span data-stu-id="db8ef-123">Prepare the portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="db8ef-124">2.</span><span class="sxs-lookup"><span data-stu-id="db8ef-124">2.</span></span> |<span data-ttu-id="db8ef-125">**佈建 Virtual Array**</span><span class="sxs-lookup"><span data-stu-id="db8ef-125">**Provision the Virtual Array**</span></span> |<span data-ttu-id="db8ef-126">對於 Hyper-V，在執行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 之 Hyper-V 的主機系統上，佈建並連接至 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="db8ef-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="db8ef-127">對於 VMware，在執行 VMware ESXi 5.5 及更新版本的主機系統上，佈建並連接至 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="db8ef-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="db8ef-128">在 Hyper-V 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="db8ef-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="db8ef-129">在 VMware 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="db8ef-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="db8ef-130">3.</span><span class="sxs-lookup"><span data-stu-id="db8ef-130">3.</span></span> |<span data-ttu-id="db8ef-131">**設定 Virtual Array**</span><span class="sxs-lookup"><span data-stu-id="db8ef-131">**Set up the Virtual Array**</span></span> |<span data-ttu-id="db8ef-132">對於檔案伺服器，請執行初始安裝程序、註冊 StorSimple 檔案伺服器，以及完成裝置安裝程序。</span><span class="sxs-lookup"><span data-stu-id="db8ef-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span></span> <span data-ttu-id="db8ef-133">接下來，您可以佈建 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="db8ef-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="db8ef-134">對於 iSCSI 伺服器，請執行初始安裝、註冊 StorSimple iSCSI 伺服器，並完成裝置安裝程序。</span><span class="sxs-lookup"><span data-stu-id="db8ef-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span></span> <span data-ttu-id="db8ef-135">接下來，您可以佈建 iSCSI 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="db8ef-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="db8ef-136">將虛擬陣列設定為檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="db8ef-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="db8ef-137">將虛擬陣列設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="db8ef-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="db8ef-138">現在您可以開始設定 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="db8ef-138">You can now begin to set up the Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="db8ef-139">設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="db8ef-139">Configuration checklist</span></span>

<span data-ttu-id="db8ef-140">設定檢查清單說明您在設定 StorSimple Virtual Array 上的軟體之前需要收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="db8ef-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="db8ef-141">事先備妥此資訊可協助簡化在環境中部署 StorSimple 裝置的程序。</span><span class="sxs-lookup"><span data-stu-id="db8ef-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="db8ef-142">視 StorSimple Virtual Array 部署為檔案伺服器或 iSCSI 伺服器而定，您需要下列其中一個檢查清單。</span><span class="sxs-lookup"><span data-stu-id="db8ef-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span></span>

* <span data-ttu-id="db8ef-143">下載 [StorSimple Virtual Array 檔案伺服器的設定檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="db8ef-144">下載 [StorSimple Virtual Array iSCSI 伺服器的設定檢查清單](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db8ef-145">必要條件</span><span class="sxs-lookup"><span data-stu-id="db8ef-145">Prerequisites</span></span>

<span data-ttu-id="db8ef-146">我們在此提供 StorSimple 裝置管理員服務、StorSimple Virtual Array 及資料中心網路的設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="db8ef-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="db8ef-147">StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="db8ef-147">For the StorSimple Device Manager service</span></span>

<span data-ttu-id="db8ef-148">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="db8ef-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="db8ef-149">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="db8ef-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="db8ef-150">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="db8ef-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="db8ef-151">您的 Microsoft Azure 訂用帳戶應該已啟用來使用 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="db8ef-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="db8ef-152">StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="db8ef-152">For the StorSimple Virtual Array</span></span>

<span data-ttu-id="db8ef-153">在您部署虛擬陣列之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="db8ef-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="db8ef-154">您可以存取可用來佈建裝置、在 Windows Server 2008 R2 或更新版本或 VMware (ESXi 5.5 或更新版本) 上執行 Hyper-V 的主機系統。</span><span class="sxs-lookup"><span data-stu-id="db8ef-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="db8ef-155">主機系統能夠把下列資源專門用來佈建虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="db8ef-155">The host system is able to dedicate the following resources to provision your virtual array:</span></span>
  
  * <span data-ttu-id="db8ef-156">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="db8ef-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="db8ef-157">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="db8ef-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="db8ef-158">若計畫將虛擬陣列設定為檔案伺服器，8 GB 支援 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="db8ef-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="db8ef-159">您需要 16 GB RAM 才能支援 2 - 4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="db8ef-159">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="db8ef-160">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="db8ef-160">One network interface.</span></span>
  * <span data-ttu-id="db8ef-161">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="db8ef-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-datacenter-network"></a><span data-ttu-id="db8ef-162">對於資料中心的網路</span><span class="sxs-lookup"><span data-stu-id="db8ef-162">For the datacenter network</span></span>

<span data-ttu-id="db8ef-163">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="db8ef-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="db8ef-164">資料中心的網路是根據 StorSimple 裝置的網路需求所設定的。</span><span class="sxs-lookup"><span data-stu-id="db8ef-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span></span> <span data-ttu-id="db8ef-165">如需詳細資訊，請參閱 [StorSimple Virtual Array 的系統需求](storsimple-ova-system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="db8ef-166">StorSimple Virtual Array 隨時都有專用的 5 Mbps 網際網路頻寬 (或更多) 可用。</span><span class="sxs-lookup"><span data-stu-id="db8ef-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="db8ef-167">此頻寬不應與任何其他應用程式共用。</span><span class="sxs-lookup"><span data-stu-id="db8ef-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="db8ef-168">逐步的準備程序</span><span class="sxs-lookup"><span data-stu-id="db8ef-168">Step-by-step preparation</span></span>

<span data-ttu-id="db8ef-169">請依照下列逐步指示，為您的 StorSimple 裝置管理員服務準備入口網站。</span><span class="sxs-lookup"><span data-stu-id="db8ef-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="db8ef-170">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="db8ef-170">Step 1: Create a new service</span></span>

<span data-ttu-id="db8ef-171">單一 StorSimple 裝置管理員服務執行個體就能管理多個 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="db8ef-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="db8ef-172">執行下列步驟來建立 StorSimple 裝置管理員服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="db8ef-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span> <span data-ttu-id="db8ef-173">如果您已經有 StorSimple 裝置管理員服務來管理虛擬陣列，請略過此步驟，並移至[步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="db8ef-174">如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="db8ef-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="db8ef-175">如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#optional-step-configure-a-new-storage-account-for-the-service) 以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="db8ef-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="db8ef-176">如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="db8ef-177">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="db8ef-177">Step 2: Get the service registration key</span></span>

<span data-ttu-id="db8ef-178">當 StorSimple 裝置管理員服務已啟動並執行之後，您就必須取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="db8ef-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="db8ef-179">這個金鑰是用來註冊和將 StorSimple 裝置與服務連接。</span><span class="sxs-lookup"><span data-stu-id="db8ef-179">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="db8ef-180">請在 [Azure 入口網站](https://portal.azure.com/)中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="db8ef-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="db8ef-181">服務註冊金鑰用來註冊所有必須向 StorSimple 裝置管理員服務註冊的 StorSimple 裝置管理員裝置。</span><span class="sxs-lookup"><span data-stu-id="db8ef-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-the-virtual-array-image"></a><span data-ttu-id="db8ef-182">步驟 3：下載虛擬陣列映像</span><span class="sxs-lookup"><span data-stu-id="db8ef-182">Step 3: Download the virtual array image</span></span>

<span data-ttu-id="db8ef-183">當您取得服務註冊金鑰之後，必須下載適當的虛擬陣列映像，以便在主機系統上佈建虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="db8ef-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span></span> <span data-ttu-id="db8ef-184">虛擬陣列映像依作業系統而定，您可以從 Azure 入口網站的 [快速啟動] 頁面下載。</span><span class="sxs-lookup"><span data-stu-id="db8ef-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db8ef-185">StorSimple Virtual Array 上執行的軟體只能搭配 Storsimple 裝置管理員服務來使用。</span><span class="sxs-lookup"><span data-stu-id="db8ef-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="db8ef-186">請在 [Azure 入口網站](https://portal.azure.com/)中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="db8ef-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-get-the-virtual-array-image"></a><span data-ttu-id="db8ef-187">若要取得虛擬陣列映像</span><span class="sxs-lookup"><span data-stu-id="db8ef-187">To get the virtual array image</span></span>

1. <span data-ttu-id="db8ef-188">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="db8ef-188">Sign into the [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="db8ef-189">在 Azure 入口網站中，按一下 [瀏覽] > [StorSimple 裝置管理員]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="db8ef-190">選取現有的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="db8ef-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="db8ef-191">在 [StorSimple 裝置管理員] 刀鋒視窗中，按一下 [快速啟動]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="db8ef-192">按一下與您想要從「Microsoft 下載中心」下載的映像對應的連結。</span><span class="sxs-lookup"><span data-stu-id="db8ef-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span></span> <span data-ttu-id="db8ef-193">映像檔大約是 4.8 GB。</span><span class="sxs-lookup"><span data-stu-id="db8ef-193">The image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="db8ef-194">VHDX (適用於 Windows Server 2012 及更新版本上的 Hyper-V)</span><span class="sxs-lookup"><span data-stu-id="db8ef-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="db8ef-195">VHD (適用於 Windows Server 2008 R2 及更新版本上的 Hyper-V)</span><span class="sxs-lookup"><span data-stu-id="db8ef-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="db8ef-196">VMDK (適用於 VMWare ESXi 5.5 及更新版本)</span><span class="sxs-lookup"><span data-stu-id="db8ef-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="db8ef-197">下載檔案並將檔案解壓縮至本機磁碟機，記下解壓縮檔案的所在位置。</span><span class="sxs-lookup"><span data-stu-id="db8ef-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="db8ef-198">選用步驟：為服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="db8ef-198">Optional step: Configure a new storage account for the service</span></span>

<span data-ttu-id="db8ef-199">這是選擇性步驟，只有在您未啟用隨著服務自動建立儲存體帳戶時才需要執行。</span><span class="sxs-lookup"><span data-stu-id="db8ef-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="db8ef-200">如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱[如何建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)來取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="db8ef-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="db8ef-201">請在 [Azure 入口網站](https://ms.portal.azure.com/)的 [StorSimple 裝置管理員服務] 頁面上執行下列步驟，以新增現有的 Microsoft Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="db8ef-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="db8ef-202">若要新增儲存體帳戶認證，而且其 Azure 訂用帳戶與裝置管理員服務相同</span><span class="sxs-lookup"><span data-stu-id="db8ef-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="db8ef-203">瀏覽至您的裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="db8ef-203">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="db8ef-204">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="db8ef-204">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="db8ef-205">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-205">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="db8ef-206">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-206">Click **Add**.</span></span>
4. <span data-ttu-id="db8ef-207">在 [加入儲存體帳戶] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="db8ef-207">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="db8ef-208">在 [訂用帳戶] 中，選取 [目前]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="db8ef-209">提供您 Azure 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="db8ef-209">Provide the name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="db8ef-210">選取 [啟用]，為 StorSimple 裝置與雲端之間的網路通訊建立安全通道。</span><span class="sxs-lookup"><span data-stu-id="db8ef-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="db8ef-211">只有當您在私人雲端內操作時，才選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="db8ef-212">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="db8ef-212">Click **Add**.</span></span> <span data-ttu-id="db8ef-213">成功建立儲存體帳戶之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="db8ef-213">You are notified after the storage account is successfully created.</span></span><br></br>
   
     ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="db8ef-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db8ef-215">Next step</span></span>

<span data-ttu-id="db8ef-216">下一個步驟是為 StorSimple Virtual Array 佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="db8ef-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="db8ef-217">請根據您的主機作業系統，來參閱下列其中一個詳細指示：</span><span class="sxs-lookup"><span data-stu-id="db8ef-217">Depending on your host operating system, see the detailed instructions in:</span></span>

* [<span data-ttu-id="db8ef-218">在 Hyper-V 中佈建 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="db8ef-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="db8ef-219">在 VMware 中佈建 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="db8ef-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

