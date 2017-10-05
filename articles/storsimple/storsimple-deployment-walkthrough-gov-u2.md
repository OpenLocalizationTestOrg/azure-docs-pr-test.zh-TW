---
title: "在 Government 入口網站中部署 StorSimple 裝置 | Microsoft Docs"
description: "描述在 Azure Government 入口網站中部署 StorSimple Update 2 裝置和服務的步驟與最佳做法。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 0b22dcdfc0432533b286e70d130bfe2ee2db92b2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal-update-2"></a><span data-ttu-id="4b3a8-103">在 Government 入口網站中部署您的內部部署 StorSimple 裝置 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="4b3a8-103">Deploy your on-premises StorSimple device in the Government Portal (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a><span data-ttu-id="4b3a8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4b3a8-104">Overview</span></span>
<span data-ttu-id="4b3a8-105">歡迎使用 Microsoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-105">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="4b3a8-106">這些部署教學課程適用於 Azure Government 入口網站中執行 Update 2 軟體的 StorSimple 8000 系列。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-106">These deployment tutorials apply to the StorSimple 8000 Series running Update 2 software in the Azure Government Portal.</span></span> <span data-ttu-id="4b3a8-107">這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件的清單，以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-107">This series of tutorials includes a configuration checklist, a list of configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="4b3a8-108">這些教學課程中的資訊均假設您已經檢閱安全性預防措施，並已打開 StorSimple 裝置包裝、裝上機架並接好纜線。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-108">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="4b3a8-109">如果您仍然需要執行這些工作，請從檢閱 [安全性預防措施](storsimple-safety.md)開始。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-109">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="4b3a8-110">請遵循裝置特定的指示打開包裝、掛接機架和佈線您的裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-110">Follow the device-specific instructions to unpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="4b3a8-111">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="4b3a8-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="4b3a8-112">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="4b3a8-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="4b3a8-113">您必須需要有系統管理員權限，才能完成安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-113">You will need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="4b3a8-114">建議您在開始之前，檢閱設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-114">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="4b3a8-115">部署與設定程序可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-115">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="4b3a8-116">發佈於 Microsoft Azure 網站上的 StorSimple 部署資訊僅適用於 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-116">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="4b3a8-117">如需 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-117">For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="4b3a8-118">如需 7000 系列部署資訊，請參閱 [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-118">For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="4b3a8-119">部署步驟</span><span class="sxs-lookup"><span data-stu-id="4b3a8-119">Deployment steps</span></span>
<span data-ttu-id="4b3a8-120">請執行這些必要步驟來設定 StorSimple 裝置，並將它連接到 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-120">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Manager service.</span></span> <span data-ttu-id="4b3a8-121">除了這些必要步驟外，部署期間也會有一些您可能需要完成的選擇性步驟和程序。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-121">In addition to the required steps, there are optional steps and procedures that you may need to complete during the deployment.</span></span> <span data-ttu-id="4b3a8-122">逐步部署指出您應該執行各選擇性步驟的時機。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-122">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="4b3a8-123">步驟</span><span class="sxs-lookup"><span data-stu-id="4b3a8-123">Step</span></span> | <span data-ttu-id="4b3a8-124">說明</span><span class="sxs-lookup"><span data-stu-id="4b3a8-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b3a8-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="4b3a8-125">**PREREQUISITES**</span></span> |<span data-ttu-id="4b3a8-126">這些是針對將要進行的部署而需要完成的準備工作。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-126">These need to be completed in preparation for the upcoming deployment.</span></span> |
| [<span data-ttu-id="4b3a8-127">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4b3a8-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="4b3a8-128">使用此檢查清單來收集並記錄部署之前和部署期間的資訊。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-128">Use this checklist to gather and record information prior to and during the deployment.</span></span> |
| [<span data-ttu-id="4b3a8-129">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="4b3a8-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="4b3a8-130">這些項目會驗證環境是否準備就緒以供部署。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-130">These  validate that the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="4b3a8-131">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="4b3a8-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="4b3a8-132">需要執行這些步驟，才能在生產環境中部署您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-132">These steps are required to deploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="4b3a8-133">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="4b3a8-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="4b3a8-134">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="4b3a8-135">*如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="4b3a8-136">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4b3a8-136">Step 2: Get the service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="4b3a8-137">使用此金鑰註冊並將 StorSimple 裝置與管理服務連接。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-137">Use this key to register and connect your StorSimple device with the management service.</span></span> |
| [<span data-ttu-id="4b3a8-138">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-138">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="4b3a8-139">使用管理服務將裝置連線到您的網路並使用 Azure 註冊以完成設定。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-139">Connect the device to your network and register it with Azure to complete the setup using the management service.</span></span> |
| [<span data-ttu-id="4b3a8-140">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="4b3a8-140">Step 4: Complete the minimum device setup</span></span>](#step-4-complete-minimum-device-setup) </br><span data-ttu-id="4b3a8-141">選用：更新您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-141">Optional: Update your StorSimple device.</span></span> |<span data-ttu-id="4b3a8-142">使用管理服務來完成裝置設定並啟用裝置以提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-142">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| [<span data-ttu-id="4b3a8-143">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="4b3a8-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="4b3a8-144">建立容器以佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-144">Create a container to provision volumes.</span></span> <span data-ttu-id="4b3a8-145">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-145">A volume container has storage   account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| [<span data-ttu-id="4b3a8-146">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="4b3a8-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="4b3a8-147">在您伺服器的 StorSimple 裝置上佈建儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-147">Provision storage volume(s) on the StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="4b3a8-148">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="4b3a8-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume) </br><span data-ttu-id="4b3a8-149">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-149">Optional: Configure MPIO.</span></span> |<span data-ttu-id="4b3a8-150">將您的伺服器連接至裝置提供的 iSCSI 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-150">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="4b3a8-151">選擇性地設定 MPIO，以確保您的伺服器可以容許連結、網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-151">Optionally, configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="4b3a8-152">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="4b3a8-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="4b3a8-153">設定備份原則以保護您的資料</span><span class="sxs-lookup"><span data-stu-id="4b3a8-153">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="4b3a8-154">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="4b3a8-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="4b3a8-155">在您部署解決方案時可能需要參考這些程序。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-155">You may need to refer to these procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="4b3a8-156">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4b3a8-156">Configure a new storage account for the service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="4b3a8-157">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="4b3a8-157">Use PuTTY to connect to the device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="4b3a8-158">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="4b3a8-158">Scan for and apply updates</span></span>](#scan-for-and-apply-updates) | |
| [<span data-ttu-id="4b3a8-159">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="4b3a8-159">Get the IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="4b3a8-160">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="4b3a8-160">Create a manual backup</span></span>](#create-a-manual-backup) | |
| [<span data-ttu-id="4b3a8-161">設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="4b3a8-161">Configure MPIO</span></span>](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="4b3a8-162">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4b3a8-162">Deployment configuration checklist</span></span>
<span data-ttu-id="4b3a8-163">在部署 StorSimple 裝置之前，您必須收集資訊以設定您裝置上的軟體。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-163">Before you deploy your StorSimple device, you will need to collect information to configure the software on your device.</span></span> <span data-ttu-id="4b3a8-164">事先備妥部分的這些資訊可協助簡化在環境中部署 StorSimple 裝置的程序。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-164">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="4b3a8-165">下載並使用此檢查清單，以記下您部署裝置時的設定詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-165">Download and use this checklist to note the configuration details as you deploy your device.</span></span>  

[<span data-ttu-id="4b3a8-166">下載 StorSimple 部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="4b3a8-166">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a><span data-ttu-id="4b3a8-167">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="4b3a8-167">Deployment prerequisites</span></span>
<span data-ttu-id="4b3a8-168">下列各節說明 StorSimple Manager 服務與 StorSimple 裝置的設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-168">The following sections explain the configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="4b3a8-169">對於 StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="4b3a8-169">For the StorSimple Manager service</span></span>
<span data-ttu-id="4b3a8-170">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="4b3a8-170">Before you begin, make sure that:</span></span>

* <span data-ttu-id="4b3a8-171">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-171">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="4b3a8-172">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-172">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="4b3a8-173">StorSimple Manager 服務已啟用您的 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-173">Your Microsoft Azure subscription is enabled for the StorSimple Manager service.</span></span> <span data-ttu-id="4b3a8-174">您應該透過 [企業合約](https://azure.microsoft.com/pricing/enterprise-agreement/)購買訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-174">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="4b3a8-175">您有權限可存取終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-175">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="4b3a8-176">對於資料中心的裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-176">For the device in the datacenter</span></span>
<span data-ttu-id="4b3a8-177">在設定裝置前，請確認：</span><span class="sxs-lookup"><span data-stu-id="4b3a8-177">Before configuring the device, make sure that:</span></span>

* <span data-ttu-id="4b3a8-178">您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：</span><span class="sxs-lookup"><span data-stu-id="4b3a8-178">Your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>
  
  * [<span data-ttu-id="4b3a8-179">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-179">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
  * [<span data-ttu-id="4b3a8-180">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-180">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="4b3a8-181">針對資料中心內的網路</span><span class="sxs-lookup"><span data-stu-id="4b3a8-181">For the network in the datacenter</span></span>
<span data-ttu-id="4b3a8-182">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="4b3a8-182">Before you begin, make sure that:</span></span>

* <span data-ttu-id="4b3a8-183">資料中心防火牆中的連接埠已開放，以允許 iSCSI 和雲端流量，如 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)中所述。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-183">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="4b3a8-184">逐步部署</span><span class="sxs-lookup"><span data-stu-id="4b3a8-184">Step-by-step deployment</span></span>
<span data-ttu-id="4b3a8-185">請在資料中心使用下列逐步指示來部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-185">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="4b3a8-186">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="4b3a8-186">Step 1: Create a new service</span></span>
<span data-ttu-id="4b3a8-187">StorSimple Manager 服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-187">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="4b3a8-188">請執行下列步驟以建立 StorSimple Manager 服務的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-188">Perform the following steps to create a new instance of the StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> <span data-ttu-id="4b3a8-189">如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-189">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="4b3a8-190">當您建立磁碟區容器時，將會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-190">This storage account will be used when you create a volume container.</span></span>
> 
> * <span data-ttu-id="4b3a8-191">如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) 以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-191">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="4b3a8-192">如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-192">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="4b3a8-193">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4b3a8-193">Step 2: Get the service registration key</span></span>
<span data-ttu-id="4b3a8-194">當 StorSimple Manager 服務啟動後處於執行中時，您就必須取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-194">After the StorSimple Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="4b3a8-195">這個金鑰可用以註冊並將 StorSimple 裝置連接至服務。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-195">This key is used to register and connect your StorSimple device to the service.</span></span>

<span data-ttu-id="4b3a8-196">請在 Government 入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-196">Perform the following steps in the Government Portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="4b3a8-197">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-197">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="4b3a8-198">您可以使用 Windows PowerShell for StorSimple 來完成 StorSimple 裝置的初始安裝，如下列程序所述。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-198">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="4b3a8-199">您必須使用終端機模擬軟體來完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-199">You will need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="4b3a8-200">如需詳細資訊，請參閱 [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-200">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="4b3a8-201">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="4b3a8-201">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="4b3a8-202">為完成 StorSimple 裝置的最小量裝置設定，您必須：</span><span class="sxs-lookup"><span data-stu-id="4b3a8-202">For the minimum device configuration of your StorSimple device, you are required to:</span></span>

* <span data-ttu-id="4b3a8-203">設定次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-203">Set up the secondary DNS server.</span></span>
* <span data-ttu-id="4b3a8-204">至少在一個網路介面上啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-204">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="4b3a8-205">針對兩個控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-205">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="4b3a8-206">請在 Government 入口網站中執行下列步驟，以完成最小量裝置設定。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-206">Perform the following steps in the Government Portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="4b3a8-207">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="4b3a8-207">Step 5: Create a volume container</span></span>
<span data-ttu-id="4b3a8-208">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-208">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="4b3a8-209">您必須建立磁碟區容器，才能開始在 StorSimple 裝置上佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-209">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="4b3a8-210">請在 Government 入口網站中執行下列步驟，以建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-210">Perform the following steps in the Government Portal to create a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="4b3a8-211">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="4b3a8-211">Step 6: Create a volume</span></span>
<span data-ttu-id="4b3a8-212">建立磁碟區容器之後，您就可以為伺服器在 StorSimple 裝置上佈建存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-212">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="4b3a8-213">請在 Government 入口網站中執行下列步驟，以建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-213">Perform the following steps in the Government Portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b3a8-214">Azure StorSimple 只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-214">Azure StorSimple can create only thinly provisioned volumes.</span></span>  <span data-ttu-id="4b3a8-215">您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-215">You cannot create fully provisioned or partially provisioned volumes on an Azure StorSimple system.</span></span>
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="4b3a8-216">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="4b3a8-216">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="4b3a8-217">請在 Windows Server 主機上執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-217">Perform these steps on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="4b3a8-218">為獲得 StorSimple 解決方案的高可用性，建議您先在主機伺服器 (選用) 上設定 MPIO，再設定 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-218">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="4b3a8-219">主機伺服器上的 MPIO 設定會確保伺服器可以容許連結、網路，或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-219">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="4b3a8-220">如需在 Windows Server 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-220">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="4b3a8-221">其中也會包括掛接、初始化和格式化 StorSimple 磁碟區的步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-221">These will also include the steps to mount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="4b3a8-222">如需在 Linux 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4b3a8-222">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>
> 
> 

<span data-ttu-id="4b3a8-223">如果您決定不設定 MPIO，請執行下列步驟在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-223">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="4b3a8-224">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="4b3a8-224">Step 8: Take a backup</span></span>
<span data-ttu-id="4b3a8-225">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-225">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="4b3a8-226">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-226">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="4b3a8-227">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-227">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="4b3a8-228">請在 Government 入口網站中執行下列步驟，以建立排程備份。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-228">Perform the following steps in the Government Portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="4b3a8-229">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-229">You can take a manual backup at any time.</span></span> <span data-ttu-id="4b3a8-230">如需相關程序，請移至 [建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-230">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="4b3a8-231">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4b3a8-231">Configure a new storage account for the service</span></span>
<span data-ttu-id="4b3a8-232">這是選擇性步驟，只有當您並未啟用服務自動建立儲存體帳戶時才需要執行。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-232">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="4b3a8-233">必須要有 Microsoft Azure 儲存體帳戶，才能建立 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-233">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="4b3a8-234">如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) 以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-234">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="4b3a8-235">請在 Government 入口網站上的 [StorSimple Manager 服務]  頁面，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-235">Perform the following steps in the Government Portal, on the **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="4b3a8-236">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="4b3a8-236">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="4b3a8-237">若要連接到 Windows PowerShell for StorSimple，您需要使用終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-237">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="4b3a8-238">您可以在存取裝置時，直接透過序列主控台或從遠端電腦開啟 Telnet 工作階段來使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-238">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="4b3a8-239">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="4b3a8-239">Scan for and apply updates</span></span>
<span data-ttu-id="4b3a8-240">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-240">Updating your device can take several hours.</span></span> <span data-ttu-id="4b3a8-241">在裝置上執行下列步驟來掃描並套用更新。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-241">Perform the following steps to scan for and apply updates on your device.</span></span>

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a><span data-ttu-id="4b3a8-242">若要更新裝置</span><span class="sxs-lookup"><span data-stu-id="4b3a8-242">To update your device</span></span>
1. <span data-ttu-id="4b3a8-243">在裝置的 [快速入門] 頁面上，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-243">On the device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="4b3a8-244">選取實體裝置，按一下 [維護]，然後按一下 [掃描更新]。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-244">Select the physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="4b3a8-245">系統會建立掃描可用更新的工作。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-245">A job to scan for available updates is created.</span></span> <span data-ttu-id="4b3a8-246">如果有可用的更新，[掃描更新] 會變更為 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-246">If updates are available, the **Scan Updates** changes to **Install Updates**.</span></span> <span data-ttu-id="4b3a8-247">按一下 [安裝更新] 。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-247">Click **Install Updates**.</span></span>
3. <span data-ttu-id="4b3a8-248">更新工作將會建立。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-248">An update job will be created.</span></span> <span data-ttu-id="4b3a8-249">巡覽至 [工作] 以監視更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-249">Monitor the status of your update by navigating to **Jobs**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4b3a8-250">當更新工作啟動時，狀態會立即顯示為 50 %。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-250">When the update job starts, it immediately displays the status as 50 percent.</span></span> <span data-ttu-id="4b3a8-251">只有在更新工作完成之後，狀態才會變更為 100%。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-251">The status changes to 100 percent only after the update job is complete.</span></span> <span data-ttu-id="4b3a8-252">更新程序沒有即時狀態。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-252">There is no real-time status for the update process.</span></span>
   > 
   > 
4. <span data-ttu-id="4b3a8-253">裝置成功更新之後，請啟用 Data 2 和 Data 3 網路介面 (如果已停用)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-253">After the device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="4b3a8-254">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="4b3a8-254">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="4b3a8-255">請執行下列步驟，以取得正在執行 Windows Server® 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-255">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="4b3a8-256">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="4b3a8-256">Create a manual backup</span></span>
<span data-ttu-id="4b3a8-257">請在 Government 入口網站中執行下列步驟，以針對 StorSimple 裝置上的單一磁碟區建立隨選手動備份。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-257">Perform the following steps in the Government Portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a><span data-ttu-id="4b3a8-258">設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="4b3a8-258">Configure MPIO</span></span>
<span data-ttu-id="4b3a8-259">多重路徑 I/O (MPIO) 是 Windows Server 預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-259">Multipath I/O (MPIO) is an optional feature and is not installed on Windows Server by default.</span></span> <span data-ttu-id="4b3a8-260">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-260">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="4b3a8-261">如需 MPIO 安裝指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-261">For MPIO installation instructions, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span>

<span data-ttu-id="4b3a8-262">如需為連接到 Linux 主機之 StorSimple 裝置安裝 MPIO 的指示，請移至 [為 Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-262">For MPIO installation instructions for a StorSimple device connected to a Linux host, go to [Configure MPIO for your Linux host](storsimple-configure-mpio-on-linux.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4b3a8-263">在 Azure 中 StorSimple 虛擬裝置不支援 MPIO。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-263">MPIO is not supported on a StorSimple virtual device in Azure.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4b3a8-264">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b3a8-264">Next steps</span></span>
* <span data-ttu-id="4b3a8-265">設定 [虛擬裝置](storsimple-virtual-device-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-265">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="4b3a8-266">使用 [StorSimple Manager 服務](storsimple-manager-service-administration.md) 以管理 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4b3a8-266">Use the [StorSimple Manager service](storsimple-manager-service-administration.md) to manage your StorSimple device.</span></span>

