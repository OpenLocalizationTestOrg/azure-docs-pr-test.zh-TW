---
title: "在 Azure 入口網站中部署 StorSimple 8000 系列裝置 | Microsoft Docs"
description: "描述部署執行 Update 3 和更新版本之 StorSimple 8000 系列裝置和 StorSimple 裝置管理員服務的步驟與最佳做法。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3d2023c3e129cfdea27f343a41b3cc373c0c3b8f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-3-and-later"></a><span data-ttu-id="4aea3-103">部署您的內部部署 StorSimple 裝置 (Update 3 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="4aea3-103">Deploy your on-premises StorSimple device (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="4aea3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4aea3-104">Overview</span></span>
<span data-ttu-id="4aea3-105">歡迎使用 Microsoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="4aea3-105">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="4aea3-106">這些部署教學課程適用於 StorSimple 8000 Series Update 3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4aea3-106">These deployment tutorials apply to StorSimple 8000 Series Update 3 or later.</span></span> <span data-ttu-id="4aea3-107">這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件，以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-107">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="4aea3-108">這些教學課程中的資訊均假設您已經檢閱安全性預防措施，並已打開 StorSimple 裝置包裝、裝上機架並接好纜線。</span><span class="sxs-lookup"><span data-stu-id="4aea3-108">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="4aea3-109">如果您仍然需要執行這些工作，請從檢閱 [安全性預防措施](storsimple-8000-safety.md)開始。</span><span class="sxs-lookup"><span data-stu-id="4aea3-109">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-8000-safety.md).</span></span> <span data-ttu-id="4aea3-110">請遵循裝置特定的指示打開包裝、掛接機架和佈線您的裝置。</span><span class="sxs-lookup"><span data-stu-id="4aea3-110">Follow the device-specific instructions to unpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="4aea3-111">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="4aea3-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="4aea3-112">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="4aea3-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="4aea3-113">您需要有系統管理員權限，才能完成安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="4aea3-113">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="4aea3-114">建議您在開始之前，檢閱設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="4aea3-114">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="4aea3-115">部署與設定程序可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="4aea3-115">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="4aea3-116">發佈於 Microsoft Azure 網站上的 StorSimple 部署資訊僅適用於 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="4aea3-116">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="4aea3-117">如需 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-117">For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="4aea3-118">如需 7000 系列部署資訊，請參閱 [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-118">For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span> 


## <a name="deployment-steps"></a><span data-ttu-id="4aea3-119">部署步驟</span><span class="sxs-lookup"><span data-stu-id="4aea3-119">Deployment steps</span></span>
<span data-ttu-id="4aea3-120">請執行這些必要步驟來設定 StorSimple 裝置，並將它連線到 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="4aea3-120">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="4aea3-121">除了這些必要步驟外，部署期間也會有一些您可能需要的選擇性步驟和程序。</span><span class="sxs-lookup"><span data-stu-id="4aea3-121">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span></span> <span data-ttu-id="4aea3-122">逐步部署指出您應該執行各選擇性步驟的時機。</span><span class="sxs-lookup"><span data-stu-id="4aea3-122">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="4aea3-123">步驟</span><span class="sxs-lookup"><span data-stu-id="4aea3-123">Step</span></span> | <span data-ttu-id="4aea3-124">說明</span><span class="sxs-lookup"><span data-stu-id="4aea3-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4aea3-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="4aea3-125">**PREREQUISITES**</span></span> |<span data-ttu-id="4aea3-126">這些是針對將要進行的部署所必須完成的準備工作。</span><span class="sxs-lookup"><span data-stu-id="4aea3-126">These must be completed in preparation for the upcoming deployment.</span></span> |
| [<span data-ttu-id="4aea3-127">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4aea3-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="4aea3-128">使用此檢查清單，將部署之前和部署期間的資訊加以收集並記錄。</span><span class="sxs-lookup"><span data-stu-id="4aea3-128">Use this checklist to gather and record information before and during the deployment.</span></span> |
| [<span data-ttu-id="4aea3-129">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="4aea3-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="4aea3-130">這些會驗證環境是否準備就緒以供部署。</span><span class="sxs-lookup"><span data-stu-id="4aea3-130">These validate the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="4aea3-131">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="4aea3-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="4aea3-132">需要執行這些步驟，才能在生產環境中部署您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4aea3-132">These steps are required to deploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="4aea3-133">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="4aea3-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="4aea3-134">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="4aea3-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="4aea3-135">*如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。</span><span class="sxs-lookup"><span data-stu-id="4aea3-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="4aea3-136">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4aea3-136">Step 2: Get the service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="4aea3-137">使用此金鑰註冊並將 StorSimple 裝置與管理服務連接。</span><span class="sxs-lookup"><span data-stu-id="4aea3-137">Use this key to register & connect your StorSimple device with the management service.</span></span> |
| [<span data-ttu-id="4aea3-138">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-138">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="4aea3-139">使用管理服務將裝置連線到您的網路，並使用 Azure 註冊以完成設定。</span><span class="sxs-lookup"><span data-stu-id="4aea3-139">To complete the setup using the management service, connect the device to your network and register it with Azure.</span></span> |
| [<span data-ttu-id="4aea3-140">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="4aea3-140">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="4aea3-141">選用：更新您的 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-141">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="4aea3-142">使用管理服務來完成裝置設定並啟用裝置以提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="4aea3-142">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| [<span data-ttu-id="4aea3-143">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="4aea3-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="4aea3-144">建立容器以佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-144">Create a container to provision volumes.</span></span> <span data-ttu-id="4aea3-145">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="4aea3-145">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| [<span data-ttu-id="4aea3-146">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="4aea3-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="4aea3-147">在您伺服器的 StorSimple 裝置上，佈建儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-147">Provision storage volumes on the StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="4aea3-148">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="4aea3-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="4aea3-149">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="4aea3-149">Optional: Configure MPIO</span></span>](storsimple-8000-configure-mpio-windows-server.md) |<span data-ttu-id="4aea3-150">將您的伺服器連接至裝置提供的 iSCSI 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4aea3-150">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="4aea3-151">選擇性地設定 MPIO 確保您的伺服器可以容許連結、網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="4aea3-151">Optionally configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="4aea3-152">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="4aea3-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="4aea3-153">設定備份原則以保護您的資料</span><span class="sxs-lookup"><span data-stu-id="4aea3-153">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="4aea3-154">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="4aea3-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="4aea3-155">在您部署解決方案時可能需要參考這些程序。</span><span class="sxs-lookup"><span data-stu-id="4aea3-155">You may need to refer to these procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="4aea3-156">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4aea3-156">Configure a new storage account for the service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="4aea3-157">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="4aea3-157">Use PuTTY to connect to the device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="4aea3-158">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="4aea3-158">Get the IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="4aea3-159">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="4aea3-159">Create a manual backup</span></span>](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a><span data-ttu-id="4aea3-160">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4aea3-160">Deployment configuration checklist</span></span>
<span data-ttu-id="4aea3-161">在部署裝置之前，您必須收集資訊以設定 StorSimple 裝置上的軟體。</span><span class="sxs-lookup"><span data-stu-id="4aea3-161">Before you deploy your device, you need to collect information to configure the software on your StorSimple device.</span></span> <span data-ttu-id="4aea3-162">事先備妥這些資訊，可協助簡化在環境中部署 StorSimple 裝置的程序。</span><span class="sxs-lookup"><span data-stu-id="4aea3-162">Preparing some of this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="4aea3-163">下載並使用此檢查清單，以記下您部署裝置時的設定詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4aea3-163">Download and use this checklist to note down the configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="4aea3-164">下載 StorSimple 部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4aea3-164">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="4aea3-165">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="4aea3-165">Deployment prerequisites</span></span>
<span data-ttu-id="4aea3-166">下列各節說明 StorSimple 裝置管理員服務與 StorSimple 裝置的設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-166">The following sections explain the configuration prerequisites for your StorSimple Device Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="4aea3-167">StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="4aea3-167">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="4aea3-168">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="4aea3-168">Before you begin, make sure that:</span></span>

* <span data-ttu-id="4aea3-169">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="4aea3-169">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="4aea3-170">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="4aea3-170">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="4aea3-171">StorSimple 裝置管理員服務已啟用您的 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4aea3-171">Your Microsoft Azure subscription is enabled for the StorSimple Device Manager service.</span></span> <span data-ttu-id="4aea3-172">您應該透過 [企業合約](https://azure.microsoft.com/pricing/enterprise-agreement/)購買訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4aea3-172">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="4aea3-173">您有權限可存取終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4aea3-173">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="4aea3-174">對於資料中心的裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-174">For the device in the datacenter</span></span>
<span data-ttu-id="4aea3-175">在設定裝置之前，請確定您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：</span><span class="sxs-lookup"><span data-stu-id="4aea3-175">Before configuring the device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="4aea3-176">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-176">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="4aea3-177">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-177">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="4aea3-178">針對資料中心內的網路</span><span class="sxs-lookup"><span data-stu-id="4aea3-178">For the network in the datacenter</span></span>
<span data-ttu-id="4aea3-179">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="4aea3-179">Before you begin, make sure that:</span></span>

* <span data-ttu-id="4aea3-180">資料中心防火牆中的連接埠已開放，以允許 iSCSI 和雲端流量，如 [StorSimple 裝置的網路需求](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)中所述。</span><span class="sxs-lookup"><span data-stu-id="4aea3-180">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="4aea3-181">逐步部署</span><span class="sxs-lookup"><span data-stu-id="4aea3-181">Step-by-step deployment</span></span>
<span data-ttu-id="4aea3-182">請在資料中心使用下列逐步指示來部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4aea3-182">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="4aea3-183">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="4aea3-183">Step 1: Create a new service</span></span>
<span data-ttu-id="4aea3-184">StorSimple 裝置管理員服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4aea3-184">A StorSimple Device Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="4aea3-185">執行下列步驟來建立 StorSimple 裝置管理員服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4aea3-185">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="4aea3-186">如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4aea3-186">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="4aea3-187">當您建立磁碟區容器時，會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4aea3-187">This storage account is used when you create a volume container.</span></span>
>
> * <span data-ttu-id="4aea3-188">如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) 以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="4aea3-188">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="4aea3-189">如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-189">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>


## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="4aea3-190">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4aea3-190">Step 2: Get the service registration key</span></span>
<span data-ttu-id="4aea3-191">當 StorSimple 裝置管理員服務已啟動並執行之後，您就必須取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="4aea3-191">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="4aea3-192">這個金鑰是用來註冊和將 StorSimple 裝置與服務連接。</span><span class="sxs-lookup"><span data-stu-id="4aea3-192">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="4aea3-193">請在 Azure 入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-193">Perform the following steps in the Azure portal.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="4aea3-194">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="4aea3-194">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="4aea3-195">您可以使用 Windows PowerShell for StorSimple 來完成 StorSimple 裝置的初始安裝，如下列程序所述。</span><span class="sxs-lookup"><span data-stu-id="4aea3-195">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="4aea3-196">您必須使用終端機模擬軟體來完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-196">You need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="4aea3-197">如需詳細資訊，請參閱 [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-197">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-8000-configure-and-register-device-u2](../../includes/storsimple-8000-configure-and-register-device-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="4aea3-198">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="4aea3-198">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="4aea3-199">為完成 StorSimple 裝置的最小量裝置設定，您必須：</span><span class="sxs-lookup"><span data-stu-id="4aea3-199">For the minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="4aea3-200">為裝置提供 [易記名稱]。</span><span class="sxs-lookup"><span data-stu-id="4aea3-200">Provide a friendly name for your device.</span></span>
* <span data-ttu-id="4aea3-201">設定裝置的時區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-201">Set the device time zone.</span></span>
* <span data-ttu-id="4aea3-202">針對兩個控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4aea3-202">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="4aea3-203">請在 Azure 入口網站中執行下列步驟，來完成最小量裝置設定。</span><span class="sxs-lookup"><span data-stu-id="4aea3-203">Perform the following steps in the Azure portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="4aea3-204">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="4aea3-204">Step 5: Create a volume container</span></span>
<span data-ttu-id="4aea3-205">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="4aea3-205">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="4aea3-206">您必須建立磁碟區容器，才能開始在 StorSimple 裝置上佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-206">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="4aea3-207">請在 Azure 入口網站中執行下列步驟，來建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="4aea3-207">Perform the following steps in the Azure portal to create a volume container.</span></span>

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="4aea3-208">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="4aea3-208">Step 6: Create a volume</span></span>
<span data-ttu-id="4aea3-209">建立磁碟區容器之後，您就可以為伺服器在 StorSimple 裝置上佈建存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-209">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="4aea3-210">請在 Azure 入口網站中執行下列步驟，來建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-210">Perform the following steps in the Azure portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aea3-211">StorSimple 裝置管理員可建立精簡的磁碟區，也可建立完整佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-211">StorSimple Device Manager can create both thin and fully provisioned volumes.</span></span> <span data-ttu-id="4aea3-212">然而，您無法建立部分佈建的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="4aea3-212">You cannot however create partially provisioned volumes.</span></span>


[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="4aea3-213">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="4aea3-213">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="4aea3-214">在 Windows Server 主機上執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-214">The following steps are performed on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="4aea3-215">為獲得 StorSimple 解決方案的高可用性，建議您先在主機伺服器 (選用) 上設定 MPIO，再設定 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="4aea3-215">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="4aea3-216">主機伺服器上的 MPIO 設定會確保伺服器可以容許連結、網路，或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="4aea3-216">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="4aea3-217">如需在 Windows Server 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-8000-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-217">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="4aea3-218">其中也會包括將 StorSimple 磁碟區掛接、初始化和格式化的步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-218">These also include the steps to mount, initialize, and format StorSimple volumes.</span></span>
> * <span data-ttu-id="4aea3-219">如需在 Linux 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4aea3-219">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>

<span data-ttu-id="4aea3-220">如果您決定不設定 MPIO，請執行下列步驟在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4aea3-220">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-8000-mount-initialize-format-volume](../../includes/storsimple-8000-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="4aea3-221">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="4aea3-221">Step 8: Take a backup</span></span>
<span data-ttu-id="4aea3-222">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="4aea3-222">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="4aea3-223">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="4aea3-223">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="4aea3-224">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="4aea3-224">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="4aea3-225">請在 Azure 入口網站中執行下列步驟，來建立排程備份。</span><span class="sxs-lookup"><span data-stu-id="4aea3-225">Perform the following steps in the Azure portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

<span data-ttu-id="4aea3-226">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="4aea3-226">You can take a manual backup at any time.</span></span> <span data-ttu-id="4aea3-227">如需相關程序，請移至 [建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-227">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

<span data-ttu-id="4aea3-228">您已經完成裝置設定。</span><span class="sxs-lookup"><span data-stu-id="4aea3-228">You have completed the device configuration.</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="4aea3-229">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4aea3-229">Configure a new storage account for the service</span></span>
<span data-ttu-id="4aea3-230">這是選擇性步驟，只有當您並未啟用服務自動建立儲存體帳戶時才需要執行。</span><span class="sxs-lookup"><span data-stu-id="4aea3-230">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="4aea3-231">必須要有 Microsoft Azure 儲存體帳戶，才能建立 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="4aea3-231">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="4aea3-232">如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) 以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="4aea3-232">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="4aea3-233">請在 Azure 入口網站上的 [StorSimple 裝置管理員服務] 頁面，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4aea3-233">Perform the following steps in the Azure portal, on the **StorSimple Device Manager service** page.</span></span>

[!INCLUDE [storsimple-8000-configure-new-storage-account-u2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="4aea3-234">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="4aea3-234">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="4aea3-235">若要連接到 Windows PowerShell for StorSimple，您需要使用終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4aea3-235">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="4aea3-236">您可以在存取裝置時，直接透過序列主控台或從遠端電腦開啟 Telnet 工作階段來使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4aea3-236">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="4aea3-237">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="4aea3-237">Scan for and apply updates</span></span>
<span data-ttu-id="4aea3-238">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="4aea3-238">Updating your device can take several hours.</span></span> <span data-ttu-id="4aea3-239">如需有關如何安裝最新更新的詳細步驟，請移至[安裝 Update 4](storsimple-8000-install-update-4.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-239">For detailed steps on how to install the latest update, go to [Install Update 4](storsimple-8000-install-update-4.md).</span></span>


## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="4aea3-240">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="4aea3-240">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="4aea3-241">請執行下列步驟，以取得正在執行 Windows Server® 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-241">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="4aea3-242">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="4aea3-242">Create a manual backup</span></span>
<span data-ttu-id="4aea3-243">請在 Azure 入口網站中執行下列步驟，針對 StorSimple 裝置上的單一磁碟區建立隨選手動備份。</span><span class="sxs-lookup"><span data-stu-id="4aea3-243">Perform the following steps in the Azure portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="4aea3-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4aea3-244">Next steps</span></span>
* <span data-ttu-id="4aea3-245">[設定 StorSimple 雲端設備](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-245">[Configure a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>
* <span data-ttu-id="4aea3-246">[使用 StorSimple 裝置管理員服務來管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-246">[Use the StorSimple Device Manager service to manage your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

