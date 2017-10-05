---
title: "在 Government 入口網站中部署 StorSimple 裝置 | Microsoft Docs"
description: "描述在 Azure Government 入口網站中部署 StorSimple Update 1 裝置和服務的步驟與最佳做法。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 3fe3648d-e0b6-4928-a2cb-8d3ccc50d62a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/17/2016
ms.author: v-sharos
ms.openlocfilehash: f120caf4ea21299e52782db33994b9bd8f63780d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal"></a><span data-ttu-id="cbbf8-103">在 Government 入口網站中部署您的內部部署 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-103">Deploy your on-premises StorSimple device in the Government Portal</span></span>
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a><span data-ttu-id="cbbf8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cbbf8-104">Overview</span></span>
<span data-ttu-id="cbbf8-105">歡迎使用 Microsoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-105">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="cbbf8-106">這些部署教學課程適用於 Azure Government 入口網站中執行 Update 1 軟體的 StorSimple 8000 系列。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-106">These deployment tutorials apply to the StorSimple 8000 Series running Update 1 software in the Azure Government Portal.</span></span> <span data-ttu-id="cbbf8-107">這一系列的教學課程說明如何設定 StorSimple 裝置，並包含設定檢查清單、設定必要條件以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-107">This series of tutorials describes how to configure your StorSimple device, and includes a configuration checklist, configuration prerequisites, and detailed configuration steps.</span></span>

<span data-ttu-id="cbbf8-108">這些教學課程中的資訊均假設您已經檢閱安全性預防措施，並已打開 StorSimple 裝置包裝、裝上機架並接好纜線。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-108">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="cbbf8-109">如果您仍然需要執行這些工作，請從檢閱 [安全性預防措施](storsimple-safety.md)開始。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-109">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="cbbf8-110">視您的裝置型號而定，您接著可以依照下列指示打開包裝、掛接機架及連接纜線：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-110">Depending on your device model, you can then unpack, rack mount, and cable by following the instructions in:</span></span>

* [<span data-ttu-id="cbbf8-111">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="cbbf8-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="cbbf8-112">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="cbbf8-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="cbbf8-113">您必須需要有系統管理員權限，才能完成安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-113">You will need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="cbbf8-114">建議您在開始之前，檢閱設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-114">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="cbbf8-115">部署與設定程序可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-115">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="cbbf8-116">發佈於 Microsoft Azure 網站上的 StorSimple 部署資訊僅適用於 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-116">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="cbbf8-117">如需 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-117">For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="cbbf8-118">如需 7000 系列部署資訊，請參閱 [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-118">For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="cbbf8-119">部署步驟</span><span class="sxs-lookup"><span data-stu-id="cbbf8-119">Deployment steps</span></span>
<span data-ttu-id="cbbf8-120">請執行這些必要步驟來設定 StorSimple 裝置，並將它連接到 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-120">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Manager service.</span></span> <span data-ttu-id="cbbf8-121">除了這些必要步驟外，部署期間也會有一些您可能需要的選擇性步驟和程序。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-121">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span></span> <span data-ttu-id="cbbf8-122">逐步部署指出您應該執行各選擇性步驟的時機。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-122">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="cbbf8-123">步驟</span><span class="sxs-lookup"><span data-stu-id="cbbf8-123">Step</span></span> | <span data-ttu-id="cbbf8-124">說明</span><span class="sxs-lookup"><span data-stu-id="cbbf8-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbbf8-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-125">**PREREQUISITES**</span></span> |<span data-ttu-id="cbbf8-126">這些是針對將要進行的部署而需要完成的準備工作。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-126">These need to be completed in preparation for the upcoming deployment.</span></span> |
| <span data-ttu-id="cbbf8-127">部署設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-127">Deployment configuration checklist.</span></span> |<span data-ttu-id="cbbf8-128">使用此檢查清單來收集並記錄部署之前和部署期間的資訊。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-128">Use this checklist to gather and record information prior to and during the deployment.</span></span> |
| <span data-ttu-id="cbbf8-129">部署必要條件。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-129">Deployment prerequisites.</span></span> |<span data-ttu-id="cbbf8-130">這些會驗證環境是否準備就緒以供部署。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-130">These  validate the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="cbbf8-131">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="cbbf8-132">需要執行這些步驟，才能在生產環境中部署您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-132">These steps are required to deploy your StorSimple device in production.</span></span> |
| <span data-ttu-id="cbbf8-133">步驟 1：建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-133">Step 1: Create a new service.</span></span> |<span data-ttu-id="cbbf8-134">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-134">Set up cloud management and storage for your   StorSimple device.</span></span> <span data-ttu-id="cbbf8-135">如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-135">Skip this step if you have an existing service for other StorSimple devices.</span></span> |
| <span data-ttu-id="cbbf8-136">步驟 2：取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-136">Step 2: Get the service registration key.</span></span> |<span data-ttu-id="cbbf8-137">使用此金鑰註冊並將 StorSimple 裝置與管理服務連接。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-137">Use this key to register & connect your StorSimple device with the management service.</span></span> |
| <span data-ttu-id="cbbf8-138">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-138">Step 3: Configure and register the device through Windows PowerShell for StorSimple.</span></span> |<span data-ttu-id="cbbf8-139">使用管理服務將裝置連線到您的網路並使用 Azure 註冊以完成設定。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-139">Connect the device to your network and register it with Azure to complete   the setup using the management service.</span></span> |
| <span data-ttu-id="cbbf8-140">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="cbbf8-140">Step 4: Complete minimum device setup</span></span></br><span data-ttu-id="cbbf8-141">選用：更新您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-141">Optional: Update your StorSimple device.</span></span> |<span data-ttu-id="cbbf8-142">使用管理服務來完成裝置設定並啟用裝置以提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-142">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| <span data-ttu-id="cbbf8-143">步驟 5：建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-143">Step 5: Create a volume container.</span></span> |<span data-ttu-id="cbbf8-144">建立容器以佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-144">Create a container to provision volumes.</span></span> <span data-ttu-id="cbbf8-145">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-145">A volume container has storage   account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| <span data-ttu-id="cbbf8-146">步驟 6：建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-146">Step 6: Create a volume.</span></span> |<span data-ttu-id="cbbf8-147">在您伺服器的 StorSimple 裝置上佈建儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-147">Provision storage volume(s) on the StorSimple device for your servers.</span></span> |
| <span data-ttu-id="cbbf8-148">步驟 7：掛接、初始化及格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-148">Step 7: Mount, initialize, and format a volume.</span></span></br><span data-ttu-id="cbbf8-149">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-149">Optional: Configure MPIO.</span></span> |<span data-ttu-id="cbbf8-150">將您的伺服器連接至裝置提供的 iSCSI 儲存體。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-150">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="cbbf8-151">選擇性地設定 MPIO 確保您的伺服器可以容許連結、網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-151">Optionally configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| <span data-ttu-id="cbbf8-152">步驟 8：進行備份。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-152">Step 8: Take a backup.</span></span> |<span data-ttu-id="cbbf8-153">設定備份原則以保護您的資料</span><span class="sxs-lookup"><span data-stu-id="cbbf8-153">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="cbbf8-154">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="cbbf8-155">在您部署解決方案時可能需要參考這些程序。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-155">You may need to refer to these procedures as you deploy your solution.</span></span> |
| <span data-ttu-id="cbbf8-156">針對服務設定新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-156">Configure a new storage account for the service.</span></span> | |
| <span data-ttu-id="cbbf8-157">使用 PuTTY 連接到裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-157">Use PuTTY to connect to the device serial console.</span></span> | |
| <span data-ttu-id="cbbf8-158">掃描並套用更新。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-158">Scan for and apply updates.</span></span> | |
| <span data-ttu-id="cbbf8-159">取得 Windows Server 主機的 IQN。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-159">Get the IQN of a Windows Server host.</span></span> | |
| <span data-ttu-id="cbbf8-160">建立手動備份。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-160">Create a manual backup.</span></span> | |
| <span data-ttu-id="cbbf8-161">設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-161">Configure MPIO.</span></span> | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="cbbf8-162">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="cbbf8-162">Deployment configuration checklist</span></span>
<span data-ttu-id="cbbf8-163">下列部署設定檢查清單描述當您在設定 StorSimple 裝置上的軟體之前需要收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-163">The following deployment configuration checklist describes the information that you need to collect before and as you configure the software on your StorSimple device.</span></span> <span data-ttu-id="cbbf8-164">事先備妥部分的這些資訊可協助簡化在環境中部署 StorSimple 裝置的程序。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-164">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="cbbf8-165">也請您使用此檢查清單記下您部署裝置時的設定詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-165">Use this checklist to also note down the configuration details as you deploy your device.</span></span>

| <span data-ttu-id="cbbf8-166">階段</span><span class="sxs-lookup"><span data-stu-id="cbbf8-166">Stage</span></span> | <span data-ttu-id="cbbf8-167">參數</span><span class="sxs-lookup"><span data-stu-id="cbbf8-167">Parameter</span></span> | <span data-ttu-id="cbbf8-168">詳細資料</span><span class="sxs-lookup"><span data-stu-id="cbbf8-168">Details</span></span> | <span data-ttu-id="cbbf8-169">值</span><span class="sxs-lookup"><span data-stu-id="cbbf8-169">Values</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbbf8-170">**將裝置接上纜線**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-170">**Cable your device**</span></span> |<span data-ttu-id="cbbf8-171">序列存取</span><span class="sxs-lookup"><span data-stu-id="cbbf8-171">Serial access</span></span> |<span data-ttu-id="cbbf8-172">初始裝置組態</span><span class="sxs-lookup"><span data-stu-id="cbbf8-172">Initial device configuration</span></span> |<span data-ttu-id="cbbf8-173">是/否</span><span class="sxs-lookup"><span data-stu-id="cbbf8-173">Yes/No</span></span> |
|  | | | |
| <span data-ttu-id="cbbf8-174">**設定和註冊裝置**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-174">**Configure and register device**</span></span> |<span data-ttu-id="cbbf8-175">Data 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="cbbf8-175">Data 0 network settings</span></span> |<span data-ttu-id="cbbf8-176">Data 0 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-176">Data 0 IP Address:</span></span></br><span data-ttu-id="cbbf8-177">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-177">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-178">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-178">Gateway:</span></span></br><span data-ttu-id="cbbf8-179">主要 DNS 伺服器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-179">Primary DNS server:</span></span></br><span data-ttu-id="cbbf8-180">主要 NTP 伺服器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-180">Primary NTP server:</span></span></br><span data-ttu-id="cbbf8-181">Web Proxy 伺服器 IP/FQDN (選擇性)︰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-181">Web proxy server IP/FQDN (optional):</span></span></br><span data-ttu-id="cbbf8-182">Web proxy 連接埠：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-182">Web proxy port:</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-183">裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="cbbf8-183">Device administrator password</span></span> |<span data-ttu-id="cbbf8-184">密碼必須介於 8 到 15 個字元之間，包含小寫字母、大寫字母、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-184">Password must be between 8 and 15 characters containing lowercase, uppercase, numeric and special characters.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-185">StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="cbbf8-185">StorSimple Snapshot Manager password</span></span> |<span data-ttu-id="cbbf8-186">密碼必須是 14 或 15 個字元，包含小寫字母、大寫字母、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-186">Password must be 14 or 15 characters containing lowercase, uppercase, numeric and special characters.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-187">服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-187">Service Registration Key</span></span> |<span data-ttu-id="cbbf8-188">此金鑰是從 Azure 入口網站產生。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-188">This key is generated from the Azure portal.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-189">服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-189">Service Data Encryption Key</span></span> |<span data-ttu-id="cbbf8-190">當裝置透過 Windows PowerShell for StorSimple 註冊管理服務時會建立此金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-190">This key is created when the device is registered with the management service via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="cbbf8-191">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-191">Copy this key and save it in a safe location.</span></span> | |
|  | | | |
| <span data-ttu-id="cbbf8-192">**完成最小裝置設定**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-192">**Complete minimum device setup**</span></span> |<span data-ttu-id="cbbf8-193">裝置的易記名稱</span><span class="sxs-lookup"><span data-stu-id="cbbf8-193">Friendly name for your device</span></span> |<span data-ttu-id="cbbf8-194">這是裝置的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-194">This is a descriptive name for the device.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-195">時區</span><span class="sxs-lookup"><span data-stu-id="cbbf8-195">Timezone</span></span> |<span data-ttu-id="cbbf8-196">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-196">Your device will use this time zone for all scheduled operations.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-197">次要 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="cbbf8-197">Secondary DNS server</span></span> |<span data-ttu-id="cbbf8-198">這是必要設定。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-198">This is a required configuration.</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-199">網路介面：Data 0 控制器固定 IP</span><span class="sxs-lookup"><span data-stu-id="cbbf8-199">Network interface: Data 0 controller fixed IPs</span></span> |<span data-ttu-id="cbbf8-200">這些 IP 必須可路由傳送到網際網路。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-200">These IP’s should be routable to the Internet.</span></span></br><span data-ttu-id="cbbf8-201">控制器 0 固定 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-201">Controller 0 fixed IP address:</span></span></br><span data-ttu-id="cbbf8-202">控制器 1 固定 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-202">Controller 1 fixed IP address:</span></span> | |
|  | | | |
| <span data-ttu-id="cbbf8-203">**其他的網路介面設定**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-203">**Additional network interface settings**</span></span> |<span data-ttu-id="cbbf8-204">網路介面：Data 1</span><span class="sxs-lookup"><span data-stu-id="cbbf8-204">Network interface: Data 1</span></span></br><span data-ttu-id="cbbf8-205">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-205">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="cbbf8-206">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="cbbf8-206">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="cbbf8-207">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-207">IP address:</span></span></br><span data-ttu-id="cbbf8-208">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-208">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-209">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-209">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-210">網路介面：Data 2</span><span class="sxs-lookup"><span data-stu-id="cbbf8-210">Network interface: Data 2</span></span></br><span data-ttu-id="cbbf8-211">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-211">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="cbbf8-212">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="cbbf8-212">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="cbbf8-213">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-213">IP address:</span></span></br><span data-ttu-id="cbbf8-214">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-214">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-215">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-215">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-216">網路介面：Data 3</span><span class="sxs-lookup"><span data-stu-id="cbbf8-216">Network interface: Data 3</span></span></br><span data-ttu-id="cbbf8-217">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-217">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="cbbf8-218">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="cbbf8-218">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="cbbf8-219">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-219">IP address:</span></span></br><span data-ttu-id="cbbf8-220">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-220">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-221">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-221">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-222">網路介面：Data 4</span><span class="sxs-lookup"><span data-stu-id="cbbf8-222">Network interface: Data 4</span></span></br><span data-ttu-id="cbbf8-223">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-223">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="cbbf8-224">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="cbbf8-224">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="cbbf8-225">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-225">IP address:</span></span></br><span data-ttu-id="cbbf8-226">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-226">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-227">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-227">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-228">網路介面：Data 5</span><span class="sxs-lookup"><span data-stu-id="cbbf8-228">Network interface: Data 5</span></span></br><span data-ttu-id="cbbf8-229">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-229">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="cbbf8-230">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="cbbf8-230">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="cbbf8-231">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-231">IP address:</span></span></br><span data-ttu-id="cbbf8-232">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-232">Subnet mask:</span></span></br><span data-ttu-id="cbbf8-233">閘道器：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-233">Gateway:</span></span> | |
|  | | | |
| <span data-ttu-id="cbbf8-234">**建立磁碟區容器**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-234">**Create a volume container**</span></span> |<span data-ttu-id="cbbf8-235">磁碟區容器名稱：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-235">Volume container name:</span></span> |<span data-ttu-id="cbbf8-236">容器名稱</span><span class="sxs-lookup"><span data-stu-id="cbbf8-236">Name for the container</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-237">Azure 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-237">Azure storage account:</span></span> |<span data-ttu-id="cbbf8-238">與此磁碟區容器相關的儲存體帳戶名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-238">Storage account name & access key to associate with this volume container</span></span> | |
| &nbsp; |<span data-ttu-id="cbbf8-239">雲端儲存體加密金鑰：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-239">Cloud storage encryption key:</span></span> |<span data-ttu-id="cbbf8-240">每個容器中儲存體的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-240">Encryption key for storage in each container</span></span> | |
|  | | | |
| <span data-ttu-id="cbbf8-241">**建立磁碟區**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-241">**Create a volume**</span></span> |<span data-ttu-id="cbbf8-242">每個磁碟區的詳細資料</span><span class="sxs-lookup"><span data-stu-id="cbbf8-242">Details for each volume</span></span> |<span data-ttu-id="cbbf8-243">磁碟區名稱：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-243">Volume name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-244">大小：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-244">Size:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-245">使用類型：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-245">Usage type:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-246">ACR 名稱：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-246">ACR name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-247">預設備份原則：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-247">Default backup policy:</span></span> | |
|  | | | |
| <span data-ttu-id="cbbf8-248">**掛接、初始化及格式化磁碟區**</span><span class="sxs-lookup"><span data-stu-id="cbbf8-248">**Mount, initialize, and format a volume**</span></span> |<span data-ttu-id="cbbf8-249">連接至儲存體的每個主機伺服器詳細資料</span><span class="sxs-lookup"><span data-stu-id="cbbf8-249">Details for each host server connecting to the storage</span></span> |<span data-ttu-id="cbbf8-250">Windows Server 名稱：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-250">Windows Server name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-251">Windows Server IQN：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-251">Windows Server IQN:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-252">Windows Server 磁碟區名稱：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-252">Windows Server volume name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="cbbf8-253">NTFS 掛接點/磁碟機代號：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-253">NTFS mount point/Drive letter:</span></span> | |

## <a name="deployment-prerequisites"></a><span data-ttu-id="cbbf8-254">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="cbbf8-254">Deployment prerequisites</span></span>
<span data-ttu-id="cbbf8-255">下列各節說明 StorSimple Manager 服務與 StorSimple 裝置的設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-255">The following sections explain the configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="cbbf8-256">對於 StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="cbbf8-256">For the StorSimple Manager service</span></span>
<span data-ttu-id="cbbf8-257">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-257">Before you begin, make sure that:</span></span>

* <span data-ttu-id="cbbf8-258">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-258">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="cbbf8-259">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-259">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="cbbf8-260">StorSimple Manager 服務已啟用您的 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-260">Your Microsoft Azure subscription is enabled for the StorSimple Manager service.</span></span> <span data-ttu-id="cbbf8-261">您應該透過 [企業合約](https://azure.microsoft.com/pricing/enterprise-agreement/)購買訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-261">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="cbbf8-262">您有權限可存取終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-262">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="cbbf8-263">對於資料中心的裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-263">For the device in the datacenter</span></span>
<span data-ttu-id="cbbf8-264">在設定裝置前，請確認：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-264">Before configuring the device, make sure that:</span></span>

* <span data-ttu-id="cbbf8-265">您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-265">Your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>
  
  * [<span data-ttu-id="cbbf8-266">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-266">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
  * [<span data-ttu-id="cbbf8-267">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-267">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="cbbf8-268">針對資料中心內的網路</span><span class="sxs-lookup"><span data-stu-id="cbbf8-268">For the network in the datacenter</span></span>
<span data-ttu-id="cbbf8-269">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-269">Before you begin, make sure that:</span></span>

* <span data-ttu-id="cbbf8-270">資料中心防火牆中的連接埠已開放，以允許 iSCSI 和雲端流量，如 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)中所述。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-270">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="cbbf8-271">逐步部署</span><span class="sxs-lookup"><span data-stu-id="cbbf8-271">Step-by-step deployment</span></span>
<span data-ttu-id="cbbf8-272">請在資料中心使用下列逐步指示來部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-272">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="cbbf8-273">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="cbbf8-273">Step 1: Create a new service</span></span>
<span data-ttu-id="cbbf8-274">StorSimple Manager 服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-274">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="cbbf8-275">請執行下列步驟以建立 StorSimple Manager 服務的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-275">Perform the following steps to create a new instance of the StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> <span data-ttu-id="cbbf8-276">如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-276">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="cbbf8-277">當您建立磁碟區容器時，將會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-277">This storage account will be used when you create a volume container.</span></span>
> 
> * <span data-ttu-id="cbbf8-278">如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) 以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-278">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="cbbf8-279">如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-279">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="cbbf8-280">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="cbbf8-280">Step 2: Get the service registration key</span></span>
<span data-ttu-id="cbbf8-281">當 StorSimple Manager 服務啟動後處於執行中時，您就必須取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-281">After the StorSimple Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="cbbf8-282">這個金鑰可用以註冊並將 StorSimple 裝置連接至服務。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-282">This key is used to register and connect your StorSimple device to the service.</span></span>

<span data-ttu-id="cbbf8-283">請在 Government 入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-283">Perform the following steps in the Government Portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="cbbf8-284">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-284">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="cbbf8-285">您可以使用 Windows PowerShell for StorSimple 來完成 StorSimple 裝置的初始安裝，如下列程序所述。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-285">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="cbbf8-286">您必須使用終端機模擬軟體來完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-286">You will need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="cbbf8-287">如需詳細資訊，請參閱 [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-287">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="cbbf8-288">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="cbbf8-288">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="cbbf8-289">為完成 StorSimple 裝置的最小量裝置設定，您必須：</span><span class="sxs-lookup"><span data-stu-id="cbbf8-289">For the minimum device configuration of your StorSimple device, you are required to:</span></span>

* <span data-ttu-id="cbbf8-290">設定次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-290">Set up the secondary DNS server.</span></span>
* <span data-ttu-id="cbbf8-291">至少在一個網路介面上啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-291">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="cbbf8-292">針對兩個控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-292">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="cbbf8-293">請在 Government 入口網站中執行下列步驟，以完成最小量裝置設定。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-293">Perform the following steps in the Government Portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="cbbf8-294">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="cbbf8-294">Step 5: Create a volume container</span></span>
<span data-ttu-id="cbbf8-295">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-295">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="cbbf8-296">您必須建立磁碟區容器，才能開始在 StorSimple 裝置上佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-296">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="cbbf8-297">請在 Government 入口網站中執行下列步驟，以建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-297">Perform the following steps in the Government Portal to create a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="cbbf8-298">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="cbbf8-298">Step 6: Create a volume</span></span>
<span data-ttu-id="cbbf8-299">建立磁碟區容器之後，您就可以為伺服器在 StorSimple 裝置上佈建存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-299">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="cbbf8-300">請在 Government 入口網站中執行下列步驟，以建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-300">Perform the following steps in the Government Portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbbf8-301">Azure StorSimple 只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-301">Azure StorSimple can create only thinly provisioned volumes.</span></span>  <span data-ttu-id="cbbf8-302">您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-302">You cannot create fully provisioned or partially provisioned volumes on an Azure StorSimple system.</span></span>
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="cbbf8-303">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="cbbf8-303">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="cbbf8-304">請在 Windows Server 主機上執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-304">Perform these steps on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cbbf8-305">為獲得 StorSimple 解決方案的高可用性，建議您先在主機伺服器 (選用) 上設定 MPIO，再設定 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-305">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="cbbf8-306">主機伺服器上的 MPIO 設定會確保伺服器可以容許連結、網路，或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-306">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="cbbf8-307">如需在 Windows Server 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-307">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="cbbf8-308">其中也會包括掛接、初始化和格式化 StorSimple 磁碟區的步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-308">These will also include the steps to mount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="cbbf8-309">如需在 Linux 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="cbbf8-309">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>
> 
> 

<span data-ttu-id="cbbf8-310">如果您決定不設定 MPIO，請執行下列步驟在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-310">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="cbbf8-311">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="cbbf8-311">Step 8: Take a backup</span></span>
<span data-ttu-id="cbbf8-312">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-312">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="cbbf8-313">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-313">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="cbbf8-314">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-314">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="cbbf8-315">請在 Government 入口網站中執行下列步驟，以建立排程備份。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-315">Perform the following steps in the Government Portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="cbbf8-316">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-316">You can take a manual backup at any time.</span></span> <span data-ttu-id="cbbf8-317">如需相關程序，請移至 [建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-317">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="cbbf8-318">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cbbf8-318">Configure a new storage account for the service</span></span>
<span data-ttu-id="cbbf8-319">這是選擇性步驟，只有當您並未啟用服務自動建立儲存體帳戶時才需要執行。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-319">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="cbbf8-320">必須要有 Microsoft Azure 儲存體帳戶，才能建立 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-320">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="cbbf8-321">如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) 以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-321">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="cbbf8-322">請在 Government 入口網站上的 [StorSimple Manager 服務]  頁面，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-322">Perform the following steps in the Government Portal, on the **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="cbbf8-323">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="cbbf8-323">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="cbbf8-324">若要連接到 Windows PowerShell for StorSimple，您需要使用終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-324">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="cbbf8-325">您可以在存取裝置時，直接透過序列主控台或從遠端電腦開啟 Telnet 工作階段來使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-325">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="cbbf8-326">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="cbbf8-326">Scan for and apply updates</span></span>
<span data-ttu-id="cbbf8-327">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-327">Updating your device can take several hours.</span></span> <span data-ttu-id="cbbf8-328">在裝置上執行下列步驟來掃描並套用更新。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-328">Perform the following steps to scan for and apply updates on your device.</span></span>

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a><span data-ttu-id="cbbf8-329">若要更新裝置</span><span class="sxs-lookup"><span data-stu-id="cbbf8-329">To update your device</span></span>
1. <span data-ttu-id="cbbf8-330">在裝置的 [快速入門] 頁面上，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-330">On the device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="cbbf8-331">選取實體裝置，按一下 [維護]，然後按一下 [掃描更新]。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-331">Select the physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="cbbf8-332">系統會建立掃描可用更新的工作。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-332">A job to scan for available updates is created.</span></span> <span data-ttu-id="cbbf8-333">如果有可用的更新，[掃描更新] 會變更為 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-333">If updates are available, the **Scan Updates** changes to **Install Updates**.</span></span> <span data-ttu-id="cbbf8-334">按一下 [安裝更新] 。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-334">Click **Install Updates**.</span></span>
3. <span data-ttu-id="cbbf8-335">更新工作將會建立。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-335">An update job will be created.</span></span> <span data-ttu-id="cbbf8-336">巡覽至 [工作] 以監視更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-336">Monitor the status of your update by navigating to **Jobs**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cbbf8-337">當更新工作啟動時，狀態會立即顯示為 50 %。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-337">When the update job starts, it immediately displays the status as 50 percent.</span></span> <span data-ttu-id="cbbf8-338">只有在更新工作完成之後，狀態才會變更為 100%。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-338">The status changes to 100 percent only after the update job is complete.</span></span> <span data-ttu-id="cbbf8-339">更新程序沒有即時狀態。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-339">There is no real-time status for the update process.</span></span>
   > 
   > 
4. <span data-ttu-id="cbbf8-340">裝置成功更新之後，請啟用 Data 2 和 Data 3 網路介面 (如果已停用)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-340">After the device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="cbbf8-341">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="cbbf8-341">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="cbbf8-342">請執行下列步驟，以取得正在執行 Windows Server® 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-342">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="cbbf8-343">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="cbbf8-343">Create a manual backup</span></span>
<span data-ttu-id="cbbf8-344">請在 Government 入口網站中執行下列步驟，以針對 StorSimple 裝置上的單一磁碟區建立隨選手動備份。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-344">Perform the following steps in the Government Portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a><span data-ttu-id="cbbf8-345">設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="cbbf8-345">Configure MPIO</span></span>
<span data-ttu-id="cbbf8-346">多重路徑 I/O (MPIO) 是 Windows Server 預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-346">Multipath I/O (MPIO) is an optional feature and is not installed on Windows Server by default.</span></span> <span data-ttu-id="cbbf8-347">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-347">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="cbbf8-348">如需 MPIO 安裝指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-348">For MPIO installation instructions, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span>

<span data-ttu-id="cbbf8-349">如需為連接到 Linux 主機之 StorSimple 裝置安裝 MPIO 的指示，請移至 [為 Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-349">For MPIO installation instructions for a StorSimple device connected to a Linux host, go to [Configure MPIO for your Linux host](storsimple-configure-mpio-on-linux.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cbbf8-350">StorSimple 虛擬裝置不支援 MPIO。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-350">MPIO is not supported on a StorSimple virtual device.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cbbf8-351">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbbf8-351">Next steps</span></span>
* <span data-ttu-id="cbbf8-352">設定 [虛擬裝置](storsimple-virtual-device-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-352">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="cbbf8-353">使用 [StorSimple Manager 服務](https://msdn.microsoft.com/library/azure/dn772396.aspx) 以管理 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cbbf8-353">Use the [StorSimple Manager service](https://msdn.microsoft.com/library/azure/dn772396.aspx) to manage your StorSimple device.</span></span>

