---
title: "部署 StorSimple 裝置 (Update 1) | Microsoft Docs"
description: "描述部署 StorSimple Update 1 裝置和服務的步驟與最佳做法。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ac631d3c-3c53-4c9e-9e4a-5c61c0cd8167
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 4d568fb2eca418ca939f7a76ac24197a0457fe47
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-1"></a><span data-ttu-id="181bd-103">部署您的內部部署 StorSimple 裝置 (Update 1)</span><span class="sxs-lookup"><span data-stu-id="181bd-103">Deploy your on-premises StorSimple device (Update 1)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="181bd-104">Update 2</span><span class="sxs-lookup"><span data-stu-id="181bd-104">Update 2</span></span>](storsimple-deployment-walkthrough-u2.md)
> * [<span data-ttu-id="181bd-105">Update 1</span><span class="sxs-lookup"><span data-stu-id="181bd-105">Update 1</span></span>](storsimple-deployment-walkthrough-u1.md)
> * [<span data-ttu-id="181bd-106">GA 版本</span><span class="sxs-lookup"><span data-stu-id="181bd-106">GA Release</span></span>](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="181bd-107">Overview</span><span class="sxs-lookup"><span data-stu-id="181bd-107">Overview</span></span>
<span data-ttu-id="181bd-108">歡迎使用 Microsoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="181bd-108">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="181bd-109">這些部署教學課程適用於 StorSimple 8000 Series Update 1.0。</span><span class="sxs-lookup"><span data-stu-id="181bd-109">These deployment tutorials apply to StorSimple 8000 Series Update 1.0.</span></span> <span data-ttu-id="181bd-110">這一系列的教學課程說明如何設定 StorSimple 裝置，並包含設定檢查清單、設定必要條件以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-110">This series of tutorials describes how to configure your StorSimple device, and includes a configuration checklist, configuration prerequisites, and detailed configuration steps.</span></span>

<span data-ttu-id="181bd-111">這些教學課程中的資訊均假設您已經檢閱安全性預防措施，並已打開 StorSimple 裝置包裝、裝上機架並接好纜線。</span><span class="sxs-lookup"><span data-stu-id="181bd-111">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="181bd-112">如果您仍然需要執行這些工作，請從檢閱 [安全性預防措施](storsimple-safety.md)開始。</span><span class="sxs-lookup"><span data-stu-id="181bd-112">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="181bd-113">視您的裝置型號而定，您接著可以依照下列指示打開包裝、掛接機架及連接纜線：</span><span class="sxs-lookup"><span data-stu-id="181bd-113">Depending on your device model, you can then unpack, rack mount, and cable by following the instructions in:</span></span>

* [<span data-ttu-id="181bd-114">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="181bd-114">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="181bd-115">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="181bd-115">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="181bd-116">您必須需要有系統管理員權限，才能完成安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="181bd-116">You will need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="181bd-117">建議您在開始之前，檢閱設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="181bd-117">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="181bd-118">部署與設定程序可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="181bd-118">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="181bd-119">發佈於 Microsoft Azure 網站上的 StorSimple 部署資訊僅適用於 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-119">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="181bd-120">如需 5000 和 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="181bd-120">For complete information about the 5000 and 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="181bd-121">如需 5000 和 7000 系列部署資訊，請參閱 [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="181bd-121">For 5000 and 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="181bd-122">部署步驟</span><span class="sxs-lookup"><span data-stu-id="181bd-122">Deployment steps</span></span>
<span data-ttu-id="181bd-123">請執行這些必要步驟來設定 StorSimple 裝置，並將它連接到 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="181bd-123">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Manager service.</span></span> <span data-ttu-id="181bd-124">除了這些必要步驟外，部署期間也會有一些您可能需要的選擇性步驟和程序。</span><span class="sxs-lookup"><span data-stu-id="181bd-124">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span></span> <span data-ttu-id="181bd-125">逐步部署指出您應該執行各選擇性步驟的時機。</span><span class="sxs-lookup"><span data-stu-id="181bd-125">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="181bd-126">步驟</span><span class="sxs-lookup"><span data-stu-id="181bd-126">Step</span></span> | <span data-ttu-id="181bd-127">說明</span><span class="sxs-lookup"><span data-stu-id="181bd-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="181bd-128">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="181bd-128">**PREREQUISITES**</span></span> |<span data-ttu-id="181bd-129">這些是針對將要進行的部署而需要完成的準備工作。</span><span class="sxs-lookup"><span data-stu-id="181bd-129">These need to be completed in preparation for the upcoming deployment.</span></span> |
| <span data-ttu-id="181bd-130">部署設定檢查清單。</span><span class="sxs-lookup"><span data-stu-id="181bd-130">Deployment configuration checklist.</span></span> |<span data-ttu-id="181bd-131">使用此檢查清單來收集並記錄部署之前和部署期間的資訊。</span><span class="sxs-lookup"><span data-stu-id="181bd-131">Use this checklist to gather and record information prior to and during the deployment.</span></span> |
| <span data-ttu-id="181bd-132">部署必要條件。</span><span class="sxs-lookup"><span data-stu-id="181bd-132">Deployment prerequisites.</span></span> |<span data-ttu-id="181bd-133">這些會驗證環境是否準備就緒以供部署。</span><span class="sxs-lookup"><span data-stu-id="181bd-133">These  validate the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="181bd-134">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="181bd-134">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="181bd-135">需要執行這些步驟，才能在生產環境中部署您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-135">These steps are required to deploy your StorSimple device in production.</span></span> |
| <span data-ttu-id="181bd-136">步驟 1：建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="181bd-136">Step 1: Create a new service.</span></span> |<span data-ttu-id="181bd-137">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="181bd-137">Set up cloud management and storage for your   StorSimple device.</span></span> <span data-ttu-id="181bd-138">如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-138">Skip this step if you have an existing service for other StorSimple devices.</span></span> |
| <span data-ttu-id="181bd-139">步驟 2：取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="181bd-139">Step 2: Get the service registration key.</span></span> |<span data-ttu-id="181bd-140">使用此金鑰註冊並將 StorSimple 裝置與管理服務連接。</span><span class="sxs-lookup"><span data-stu-id="181bd-140">Use this key to register & connect your StorSimple device with the management service.</span></span> |
| <span data-ttu-id="181bd-141">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-141">Step 3: Configure and register the device through Windows PowerShell for StorSimple.</span></span> |<span data-ttu-id="181bd-142">使用管理服務將裝置連線到您的網路並使用 Azure 註冊以完成設定。</span><span class="sxs-lookup"><span data-stu-id="181bd-142">Connect the device to your network and register it with Azure to complete   the setup using the management service.</span></span> |
| <span data-ttu-id="181bd-143">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="181bd-143">Step 4: Complete minimum device setup</span></span></br><span data-ttu-id="181bd-144">選用：更新您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-144">Optional: Update your StorSimple device.</span></span> |<span data-ttu-id="181bd-145">使用管理服務來完成裝置設定並啟用裝置以提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="181bd-145">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| <span data-ttu-id="181bd-146">步驟 5：建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="181bd-146">Step 5: Create a volume container.</span></span> |<span data-ttu-id="181bd-147">建立容器以佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-147">Create a container to provision volumes.</span></span> <span data-ttu-id="181bd-148">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="181bd-148">A volume container has storage   account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| <span data-ttu-id="181bd-149">步驟 6：建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-149">Step 6: Create a volume.</span></span> |<span data-ttu-id="181bd-150">在您伺服器的 StorSimple 裝置上佈建儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-150">Provision storage volume(s) on the StorSimple device for your servers.</span></span> |
| <span data-ttu-id="181bd-151">步驟 7：掛接、初始化及格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-151">Step 7: Mount, initialize, and format a volume.</span></span></br><span data-ttu-id="181bd-152">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="181bd-152">Optional: Configure MPIO.</span></span> |<span data-ttu-id="181bd-153">將您的伺服器連接至裝置提供的 iSCSI 儲存體。</span><span class="sxs-lookup"><span data-stu-id="181bd-153">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="181bd-154">選擇性地設定 MPIO 確保您的伺服器可以容許連結、網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="181bd-154">Optionally configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| <span data-ttu-id="181bd-155">步驟 8：進行備份。</span><span class="sxs-lookup"><span data-stu-id="181bd-155">Step 8: Take a backup.</span></span> |<span data-ttu-id="181bd-156">設定備份原則以保護您的資料</span><span class="sxs-lookup"><span data-stu-id="181bd-156">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="181bd-157">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="181bd-157">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="181bd-158">在您部署解決方案時可能需要參考這些程序。</span><span class="sxs-lookup"><span data-stu-id="181bd-158">You may need to refer to these procedures as you deploy your solution.</span></span> |
| <span data-ttu-id="181bd-159">針對服務設定新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="181bd-159">Configure a new storage account for the service.</span></span> | |
| <span data-ttu-id="181bd-160">使用 PuTTY 連接到裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="181bd-160">Use PuTTY to connect to the device serial console.</span></span> | |
| <span data-ttu-id="181bd-161">取得 Windows Server 主機的 IQN。</span><span class="sxs-lookup"><span data-stu-id="181bd-161">Get the IQN of a Windows Server host.</span></span> | |
| <span data-ttu-id="181bd-162">建立手動備份。</span><span class="sxs-lookup"><span data-stu-id="181bd-162">Create a manual backup.</span></span> | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="181bd-163">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="181bd-163">Deployment configuration checklist</span></span>
<span data-ttu-id="181bd-164">下列部署設定檢查清單描述當您在設定 StorSimple 裝置上的軟體之前需要收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="181bd-164">The following deployment configuration checklist describes the information that you need to collect before and as you configure the software on your StorSimple device.</span></span> <span data-ttu-id="181bd-165">事先備妥部分的這些資訊可協助簡化在環境中部署 StorSimple 裝置的程序。</span><span class="sxs-lookup"><span data-stu-id="181bd-165">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="181bd-166">也請您使用此檢查清單記下您部署裝置時的設定詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="181bd-166">Use this checklist to also note down the configuration details as you deploy your device.</span></span>

| <span data-ttu-id="181bd-167">階段</span><span class="sxs-lookup"><span data-stu-id="181bd-167">Stage</span></span> | <span data-ttu-id="181bd-168">參數</span><span class="sxs-lookup"><span data-stu-id="181bd-168">Parameter</span></span> | <span data-ttu-id="181bd-169">詳細資料</span><span class="sxs-lookup"><span data-stu-id="181bd-169">Details</span></span> | <span data-ttu-id="181bd-170">值</span><span class="sxs-lookup"><span data-stu-id="181bd-170">Values</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="181bd-171">**將裝置接上纜線**</span><span class="sxs-lookup"><span data-stu-id="181bd-171">**Cable your device**</span></span> |<span data-ttu-id="181bd-172">序列存取</span><span class="sxs-lookup"><span data-stu-id="181bd-172">Serial access</span></span> |<span data-ttu-id="181bd-173">初始裝置組態</span><span class="sxs-lookup"><span data-stu-id="181bd-173">Initial device configuration</span></span> |<span data-ttu-id="181bd-174">是/否</span><span class="sxs-lookup"><span data-stu-id="181bd-174">Yes/No</span></span> |
|  | | | |
| <span data-ttu-id="181bd-175">**設定和註冊裝置**</span><span class="sxs-lookup"><span data-stu-id="181bd-175">**Configure and register device**</span></span> |<span data-ttu-id="181bd-176">Data 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="181bd-176">Data 0 network settings</span></span> |<span data-ttu-id="181bd-177">Data 0 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-177">Data 0 IP Address:</span></span></br><span data-ttu-id="181bd-178">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-178">Subnet mask:</span></span></br><span data-ttu-id="181bd-179">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-179">Gateway:</span></span></br><span data-ttu-id="181bd-180">主要 DNS 伺服器：</span><span class="sxs-lookup"><span data-stu-id="181bd-180">Primary DNS server:</span></span></br><span data-ttu-id="181bd-181">主要 NTP 伺服器：</span><span class="sxs-lookup"><span data-stu-id="181bd-181">Primary NTP server:</span></span></br><span data-ttu-id="181bd-182">Web Proxy 伺服器 IP/FQDN (選擇性)︰</span><span class="sxs-lookup"><span data-stu-id="181bd-182">Web proxy server IP/FQDN (optional):</span></span></br><span data-ttu-id="181bd-183">Web proxy 連接埠：</span><span class="sxs-lookup"><span data-stu-id="181bd-183">Web proxy port:</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-184">裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="181bd-184">Device administrator password</span></span> |<span data-ttu-id="181bd-185">密碼必須介於 8 到 15 個字元之間，包含小寫字母、大寫字母、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="181bd-185">Password must be between 8 and 15 characters containing lowercase, uppercase, numeric and special characters.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-186">StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="181bd-186">StorSimple Snapshot Manager password</span></span> |<span data-ttu-id="181bd-187">密碼必須是 14 或 15 個字元，包含小寫字母、大寫字母、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="181bd-187">Password must be 14 or 15 characters containing lowercase, uppercase, numeric and special characters.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-188">服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="181bd-188">Service Registration Key</span></span> |<span data-ttu-id="181bd-189">此金鑰是從 Azure 傳統入口網站產生。</span><span class="sxs-lookup"><span data-stu-id="181bd-189">This key is generated from the Azure classic portal.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-190">服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="181bd-190">Service Data Encryption Key</span></span> |<span data-ttu-id="181bd-191">當裝置透過 Windows PowerShell for StorSimple 註冊管理服務時會建立此金鑰。</span><span class="sxs-lookup"><span data-stu-id="181bd-191">This key is created when the device is registered with the management service via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="181bd-192">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="181bd-192">Copy this key and save it in a safe location.</span></span> | |
|  | | | |
| <span data-ttu-id="181bd-193">**完成最小裝置設定**</span><span class="sxs-lookup"><span data-stu-id="181bd-193">**Complete minimum device setup**</span></span> |<span data-ttu-id="181bd-194">裝置的易記名稱</span><span class="sxs-lookup"><span data-stu-id="181bd-194">Friendly name for your device</span></span> |<span data-ttu-id="181bd-195">這是裝置的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="181bd-195">This is a descriptive name for the device.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-196">時區</span><span class="sxs-lookup"><span data-stu-id="181bd-196">Timezone</span></span> |<span data-ttu-id="181bd-197">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="181bd-197">Your device will use this time zone for all scheduled operations.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-198">次要 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="181bd-198">Secondary DNS server</span></span> |<span data-ttu-id="181bd-199">這是必要設定。</span><span class="sxs-lookup"><span data-stu-id="181bd-199">This is a required configuration.</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-200">網路介面：Data 0 控制器固定 IP</span><span class="sxs-lookup"><span data-stu-id="181bd-200">Network interface: Data 0 controller fixed IPs</span></span> |<span data-ttu-id="181bd-201">這些 IP 必須可路由傳送到網際網路。</span><span class="sxs-lookup"><span data-stu-id="181bd-201">These IP’s should be routable to the Internet.</span></span></br><span data-ttu-id="181bd-202">控制器 0 固定 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="181bd-202">Controller 0 fixed IP address:</span></span></br><span data-ttu-id="181bd-203">控制器 1 固定 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="181bd-203">Controller 1 fixed IP address:</span></span> | |
|  | | | |
| <span data-ttu-id="181bd-204">**其他的網路介面設定**</span><span class="sxs-lookup"><span data-stu-id="181bd-204">**Additional network interface settings**</span></span> |<span data-ttu-id="181bd-205">網路介面：Data 1</span><span class="sxs-lookup"><span data-stu-id="181bd-205">Network interface: Data 1</span></span></br><span data-ttu-id="181bd-206">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="181bd-206">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="181bd-207">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="181bd-207">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="181bd-208">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-208">IP address:</span></span></br><span data-ttu-id="181bd-209">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-209">Subnet mask:</span></span></br><span data-ttu-id="181bd-210">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-210">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-211">網路介面：Data 2</span><span class="sxs-lookup"><span data-stu-id="181bd-211">Network interface: Data 2</span></span></br><span data-ttu-id="181bd-212">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="181bd-212">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="181bd-213">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="181bd-213">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="181bd-214">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-214">IP address:</span></span></br><span data-ttu-id="181bd-215">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-215">Subnet mask:</span></span></br><span data-ttu-id="181bd-216">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-216">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-217">網路介面：Data 3</span><span class="sxs-lookup"><span data-stu-id="181bd-217">Network interface: Data 3</span></span></br><span data-ttu-id="181bd-218">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="181bd-218">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="181bd-219">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="181bd-219">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="181bd-220">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-220">IP address:</span></span></br><span data-ttu-id="181bd-221">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-221">Subnet mask:</span></span></br><span data-ttu-id="181bd-222">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-222">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-223">網路介面：Data 4</span><span class="sxs-lookup"><span data-stu-id="181bd-223">Network interface: Data 4</span></span></br><span data-ttu-id="181bd-224">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="181bd-224">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="181bd-225">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="181bd-225">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="181bd-226">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-226">IP address:</span></span></br><span data-ttu-id="181bd-227">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-227">Subnet mask:</span></span></br><span data-ttu-id="181bd-228">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-228">Gateway:</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-229">網路介面：Data 5</span><span class="sxs-lookup"><span data-stu-id="181bd-229">Network interface: Data 5</span></span></br><span data-ttu-id="181bd-230">如果 iSCSI 已啟用，請勿設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="181bd-230">If iSCSI enabled, do not configure the Gateway.</span></span> |<span data-ttu-id="181bd-231">用途：雲端/iSCSI/未使用</span><span class="sxs-lookup"><span data-stu-id="181bd-231">Purpose: Cloud/iSCSI/Not used</span></span></br><span data-ttu-id="181bd-232">IP 位址：</span><span class="sxs-lookup"><span data-stu-id="181bd-232">IP address:</span></span></br><span data-ttu-id="181bd-233">子網路遮罩：</span><span class="sxs-lookup"><span data-stu-id="181bd-233">Subnet mask:</span></span></br><span data-ttu-id="181bd-234">閘道器：</span><span class="sxs-lookup"><span data-stu-id="181bd-234">Gateway:</span></span> | |
|  | | | |
| <span data-ttu-id="181bd-235">**建立磁碟區容器**</span><span class="sxs-lookup"><span data-stu-id="181bd-235">**Create a volume container**</span></span> |<span data-ttu-id="181bd-236">磁碟區容器名稱：</span><span class="sxs-lookup"><span data-stu-id="181bd-236">Volume container name:</span></span> |<span data-ttu-id="181bd-237">容器名稱</span><span class="sxs-lookup"><span data-stu-id="181bd-237">Name for the container</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-238">Azure 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="181bd-238">Azure storage account:</span></span> |<span data-ttu-id="181bd-239">與此磁碟區容器相關的儲存體帳戶名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="181bd-239">Storage account name & access key to associate with this volume container</span></span> | |
| &nbsp; |<span data-ttu-id="181bd-240">雲端儲存體加密金鑰：</span><span class="sxs-lookup"><span data-stu-id="181bd-240">Cloud storage encryption key:</span></span> |<span data-ttu-id="181bd-241">每個容器中儲存體的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="181bd-241">Encryption key for storage in each container</span></span> | |
|  | | | |
| <span data-ttu-id="181bd-242">**建立磁碟區**</span><span class="sxs-lookup"><span data-stu-id="181bd-242">**Create a volume**</span></span> |<span data-ttu-id="181bd-243">每個磁碟區的詳細資料</span><span class="sxs-lookup"><span data-stu-id="181bd-243">Details for each volume</span></span> |<span data-ttu-id="181bd-244">磁碟區名稱：</span><span class="sxs-lookup"><span data-stu-id="181bd-244">Volume name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-245">大小：</span><span class="sxs-lookup"><span data-stu-id="181bd-245">Size:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-246">使用類型：</span><span class="sxs-lookup"><span data-stu-id="181bd-246">Usage type:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-247">ACR 名稱：</span><span class="sxs-lookup"><span data-stu-id="181bd-247">ACR name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-248">預設備份原則：</span><span class="sxs-lookup"><span data-stu-id="181bd-248">Default backup policy:</span></span> | |
|  | | | |
| <span data-ttu-id="181bd-249">**掛接、初始化及格式化磁碟區**</span><span class="sxs-lookup"><span data-stu-id="181bd-249">**Mount, initialize, and format a volume**</span></span> |<span data-ttu-id="181bd-250">連接至儲存體的每個主機伺服器詳細資料</span><span class="sxs-lookup"><span data-stu-id="181bd-250">Details for each host server connecting to the storage</span></span> |<span data-ttu-id="181bd-251">Windows Server 名稱：</span><span class="sxs-lookup"><span data-stu-id="181bd-251">Windows Server name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-252">Windows Server IQN：</span><span class="sxs-lookup"><span data-stu-id="181bd-252">Windows Server IQN:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-253">Windows Server 磁碟區名稱：</span><span class="sxs-lookup"><span data-stu-id="181bd-253">Windows Server volume name:</span></span> | |
| &nbsp; |&nbsp; |<span data-ttu-id="181bd-254">NTFS 掛接點/磁碟機代號：</span><span class="sxs-lookup"><span data-stu-id="181bd-254">NTFS mount point/Drive letter:</span></span> | |

## <a name="deployment-prerequisites"></a><span data-ttu-id="181bd-255">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="181bd-255">Deployment prerequisites</span></span>
<span data-ttu-id="181bd-256">下列各節說明 StorSimple Manager 服務與 StorSimple 裝置的設定必要條件。</span><span class="sxs-lookup"><span data-stu-id="181bd-256">The following sections explain the configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="181bd-257">對於 StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="181bd-257">For the StorSimple Manager service</span></span>
<span data-ttu-id="181bd-258">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="181bd-258">Before you begin, make sure that:</span></span>

* <span data-ttu-id="181bd-259">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="181bd-259">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="181bd-260">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="181bd-260">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="181bd-261">StorSimple Manager 服務已啟用您的 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="181bd-261">Your Microsoft Azure subscription is enabled for the StorSimple Manager service.</span></span> <span data-ttu-id="181bd-262">您應該透過 [企業合約](https://azure.microsoft.com/pricing/enterprise-agreement/)購買訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="181bd-262">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="181bd-263">您有權限可存取終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="181bd-263">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="181bd-264">對於資料中心的裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-264">For the device in the datacenter</span></span>
<span data-ttu-id="181bd-265">在設定裝置前，請確認：</span><span class="sxs-lookup"><span data-stu-id="181bd-265">Before configuring the device, make sure that:</span></span>

* <span data-ttu-id="181bd-266">您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：</span><span class="sxs-lookup"><span data-stu-id="181bd-266">Your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>
  
  * [<span data-ttu-id="181bd-267">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-267">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
  * [<span data-ttu-id="181bd-268">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-268">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="181bd-269">針對資料中心內的網路</span><span class="sxs-lookup"><span data-stu-id="181bd-269">For the network in the datacenter</span></span>
<span data-ttu-id="181bd-270">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="181bd-270">Before you begin, make sure that:</span></span>

* <span data-ttu-id="181bd-271">資料中心防火牆中的連接埠已開放，以允許 iSCSI 和雲端流量，如 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)中所述。</span><span class="sxs-lookup"><span data-stu-id="181bd-271">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="181bd-272">逐步部署</span><span class="sxs-lookup"><span data-stu-id="181bd-272">Step-by-step deployment</span></span>
<span data-ttu-id="181bd-273">請在資料中心使用下列逐步指示來部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-273">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="181bd-274">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="181bd-274">Step 1: Create a new service</span></span>
<span data-ttu-id="181bd-275">StorSimple Manager 服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-275">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="181bd-276">請執行下列步驟以建立 StorSimple Manager 服務的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="181bd-276">Perform the following steps to create a new instance of the StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="181bd-277">如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="181bd-277">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="181bd-278">當您建立磁碟區容器時，將會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="181bd-278">This storage account will be used when you create a volume container.</span></span>
> 
> * <span data-ttu-id="181bd-279">如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) 以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="181bd-279">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="181bd-280">如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="181bd-280">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="181bd-281">步驟 2：取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="181bd-281">Step 2: Get the service registration key</span></span>
<span data-ttu-id="181bd-282">當 StorSimple Manager 服務啟動後處於執行中時，您就必須取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="181bd-282">After the StorSimple Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="181bd-283">這個金鑰是用來註冊和將 StorSimple 裝置與服務連接。</span><span class="sxs-lookup"><span data-stu-id="181bd-283">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="181bd-284">請在 Azure 傳統入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-284">Perform the following steps in the Azure classic portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="181bd-285">步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-285">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="181bd-286">您可以使用 Windows PowerShell for StorSimple 來完成 StorSimple 裝置的初始安裝，如下列程序所述。</span><span class="sxs-lookup"><span data-stu-id="181bd-286">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="181bd-287">您必須使用終端機模擬軟體來完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-287">You will need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="181bd-288">如需詳細資訊，請參閱 [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="181bd-288">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="181bd-289">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="181bd-289">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="181bd-290">為完成 StorSimple 裝置的最小量裝置設定，您必須：</span><span class="sxs-lookup"><span data-stu-id="181bd-290">For the minimum device configuration of your StorSimple device, you are required to:</span></span>

* <span data-ttu-id="181bd-291">設定次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="181bd-291">Set up the secondary DNS server.</span></span>
* <span data-ttu-id="181bd-292">至少在一個網路介面上啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="181bd-292">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="181bd-293">針對兩個控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="181bd-293">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="181bd-294">請在 Azure 傳統入口網站中執行下列步驟以完成最小量裝置設定。</span><span class="sxs-lookup"><span data-stu-id="181bd-294">Perform the following steps in the Azure classic portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="181bd-295">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="181bd-295">Step 5: Create a volume container</span></span>
<span data-ttu-id="181bd-296">磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。</span><span class="sxs-lookup"><span data-stu-id="181bd-296">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="181bd-297">您必須建立磁碟區容器，才能開始在 StorSimple 裝置上佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-297">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="181bd-298">請在 Azure 傳統入口網站中執行下列步驟以建立磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="181bd-298">Perform the following steps in the Azure classic portal to create a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="181bd-299">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="181bd-299">Step 6: Create a volume</span></span>
<span data-ttu-id="181bd-300">建立磁碟區容器之後，您就可以為伺服器在 StorSimple 裝置上佈建存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-300">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="181bd-301">請在 Azure 傳統入口網站中執行下列步驟以建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-301">Perform the following steps in the Azure  classic portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="181bd-302">StorSimple Manager 只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-302">StorSimple Manager can create only thinly provisioned volumes.</span></span> <span data-ttu-id="181bd-303">您無法建立完整佈建或部分佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-303">You cannot create fully provisioned or partially provisioned volumes.</span></span>
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="181bd-304">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="181bd-304">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="181bd-305">在 Windows Server 主機上執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-305">The following steps are performed on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="181bd-306">為獲得 StorSimple 解決方案的高可用性，建議您先在主機伺服器 (選用) 上設定 MPIO，再設定 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="181bd-306">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="181bd-307">主機伺服器上的 MPIO 設定會確保伺服器可以容許連結、網路，或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="181bd-307">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="181bd-308">如需在 Windows Server 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="181bd-308">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="181bd-309">其中也會包括掛接、初始化和格式化 StorSimple 磁碟區的步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-309">These will also include the steps to mount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="181bd-310">如需在 Linux 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="181bd-310">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>
> 
> 

<span data-ttu-id="181bd-311">如果您決定不設定 MPIO，請執行下列步驟在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="181bd-311">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="181bd-312">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="181bd-312">Step 8: Take a backup</span></span>
<span data-ttu-id="181bd-313">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="181bd-313">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="181bd-314">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="181bd-314">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="181bd-315">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="181bd-315">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="181bd-316">請在 Azure 傳統入口網站中執行下列步驟，以建立排程備份。</span><span class="sxs-lookup"><span data-stu-id="181bd-316">Perform the following steps in the Azure classic portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="181bd-317">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="181bd-317">You can take a manual backup at any time.</span></span> <span data-ttu-id="181bd-318">如需相關程序，請移至 [建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="181bd-318">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="181bd-319">針對服務設定新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="181bd-319">Configure a new storage account for the service</span></span>
<span data-ttu-id="181bd-320">這是選擇性步驟，只有當您並未啟用服務自動建立儲存體帳戶時才需要執行。</span><span class="sxs-lookup"><span data-stu-id="181bd-320">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="181bd-321">必須要有 Microsoft Azure 儲存體帳戶，才能建立 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="181bd-321">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="181bd-322">如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) 以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="181bd-322">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="181bd-323">請在 Azure 傳統入口網站上的 [StorSimple Manager 服務]  頁面，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="181bd-323">Perform the following steps in the Azure classic portal, on the **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="181bd-324">使用 PuTTY 連接到裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="181bd-324">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="181bd-325">若要連接到 Windows PowerShell for StorSimple，您需要使用終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="181bd-325">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="181bd-326">您可以在存取裝置時，直接透過序列主控台或從遠端電腦開啟 Telnet 工作階段來使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="181bd-326">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="181bd-327">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="181bd-327">Scan for and apply updates</span></span>
<span data-ttu-id="181bd-328">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="181bd-328">Updating your device can take several hours.</span></span> <span data-ttu-id="181bd-329">在裝置上執行下列步驟來掃描並套用更新。</span><span class="sxs-lookup"><span data-stu-id="181bd-329">Perform the following steps to scan for and apply updates on your device.</span></span>
<!--can take 1-4 hours-->

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a><span data-ttu-id="181bd-330">若要更新裝置</span><span class="sxs-lookup"><span data-stu-id="181bd-330">To update your device</span></span>
1. <span data-ttu-id="181bd-331">在裝置的 [快速入門] 頁面上，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="181bd-331">On the device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="181bd-332">選取實體裝置，按一下 [維護]，然後按一下 [掃描更新]。</span><span class="sxs-lookup"><span data-stu-id="181bd-332">Select the physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="181bd-333">系統會建立掃描可用更新的工作。</span><span class="sxs-lookup"><span data-stu-id="181bd-333">A job to scan for available updates is created.</span></span> <span data-ttu-id="181bd-334">如果有可用的更新，[掃描更新] 會變更為 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="181bd-334">If updates are available, the **Scan Updates** changes to **Install Updates**.</span></span> <span data-ttu-id="181bd-335">按一下 [安裝更新] 。</span><span class="sxs-lookup"><span data-stu-id="181bd-335">Click **Install Updates**.</span></span>
3. <span data-ttu-id="181bd-336">更新工作將會建立。</span><span class="sxs-lookup"><span data-stu-id="181bd-336">An update job will be created.</span></span> <span data-ttu-id="181bd-337">巡覽至 [工作] 以監視更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="181bd-337">Monitor the status of your update by navigating to **Jobs**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="181bd-338">當更新工作啟動時，狀態會立即顯示為 50 %。</span><span class="sxs-lookup"><span data-stu-id="181bd-338">When the update job starts, it immediately displays the status as 50 percent.</span></span> <span data-ttu-id="181bd-339">只有在更新工作完成之後，狀態才會變更為 100%。</span><span class="sxs-lookup"><span data-stu-id="181bd-339">The status changes to 100 percent only after the update job is complete.</span></span> <span data-ttu-id="181bd-340">更新程序沒有即時狀態。</span><span class="sxs-lookup"><span data-stu-id="181bd-340">There is no real-time status for the update process.</span></span>
   > 
   > 
4. <span data-ttu-id="181bd-341">裝置成功更新之後，請啟用 Data 2 和 Data 3 網路介面 (如果已停用)。</span><span class="sxs-lookup"><span data-stu-id="181bd-341">After the device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

<!-- In step 2, you may be requested to disable Data 2 and Data 3 prior to installing the updates. You must disable these network interfaces or the updates may fail.-->

## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="181bd-342">取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="181bd-342">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="181bd-343">請執行下列步驟，以取得正在執行 Windows Server® 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="181bd-343">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="181bd-344">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="181bd-344">Create a manual backup</span></span>
<span data-ttu-id="181bd-345">請在 Azure 傳統入口網站中執行下列步驟，以針對 StorSimple 裝置上的單一磁碟區建立隨選手動備份。</span><span class="sxs-lookup"><span data-stu-id="181bd-345">Perform the following steps in the Azure classic portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="configure-mpio"></a><span data-ttu-id="181bd-346">設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="181bd-346">Configure MPIO</span></span>
<span data-ttu-id="181bd-347">多重路徑 I/O (MPIO) 是 Windows Server 預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="181bd-347">Multipath I/O (MPIO) is an optional feature and is not installed on Windows Server by default.</span></span> <span data-ttu-id="181bd-348">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="181bd-348">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="181bd-349">如需 MPIO 安裝指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="181bd-349">For MPIO installation instructions, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span>

<span data-ttu-id="181bd-350">如需為連接到 Linux 主機之 StorSimple 裝置安裝 MPIO 的指示，請移至 [為 Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="181bd-350">For MPIO installation instructions for a StorSimple device connected to a Linux host, go to [Configure MPIO for your Linux host](storsimple-configure-mpio-on-linux.md).</span></span>

> [!NOTE]
> <span data-ttu-id="181bd-351">StorSimple 虛擬裝置不支援 MPIO。</span><span class="sxs-lookup"><span data-stu-id="181bd-351">MPIO is not supported on a StorSimple virtual device.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="181bd-352">後續步驟</span><span class="sxs-lookup"><span data-stu-id="181bd-352">Next steps</span></span>
* <span data-ttu-id="181bd-353">設定 [虛擬裝置](storsimple-virtual-device-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="181bd-353">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="181bd-354">使用 [StorSimple Manager 服務](storsimple-manager-service-administration.md) 以管理 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="181bd-354">Use the [StorSimple Manager service](storsimple-manager-service-administration.md) to manage your StorSimple device.</span></span>

