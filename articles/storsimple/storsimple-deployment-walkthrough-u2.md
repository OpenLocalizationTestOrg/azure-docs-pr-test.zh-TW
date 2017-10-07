---
title: "aaaDeploy StorSimple 裝置 (Update 2) |Microsoft 文件"
description: "描述 hello 步驟和部署 hello StorSimple Update 2 的裝置和服務的最佳作法。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: 5906cc3c41f03c426905ef91be37852608ae9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a><span data-ttu-id="867c7-103">部署您的內部部署 StorSimple 裝置 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="867c7-103">Deploy your on-premises StorSimple device (Update 2)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="867c7-104">Update 2 和更新版本</span><span class="sxs-lookup"><span data-stu-id="867c7-104">Update 2 & later </span></span>](storsimple-deployment-walkthrough-u2.md)
> * [<span data-ttu-id="867c7-105">Update 1</span><span class="sxs-lookup"><span data-stu-id="867c7-105">Update 1</span></span>](storsimple-deployment-walkthrough-u1.md)
> * [<span data-ttu-id="867c7-106">GA 版本</span><span class="sxs-lookup"><span data-stu-id="867c7-106">GA Release</span></span>](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="867c7-107">概觀</span><span class="sxs-lookup"><span data-stu-id="867c7-107">Overview</span></span>
<span data-ttu-id="867c7-108">歡迎使用 tooMicrosoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="867c7-108">Welcome tooMicrosoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="867c7-109">這些部署教學課程適用於 tooStorSimple 8000 系列 Update 2。</span><span class="sxs-lookup"><span data-stu-id="867c7-109">These deployment tutorials apply tooStorSimple 8000 Series Update 2.</span></span> <span data-ttu-id="867c7-110">這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件，以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="867c7-110">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="867c7-111">這些教學課程中的 hello 資訊假設您已檢閱 hello 安全措施，並解壓縮、 racked，和妥您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-111">hello information in these tutorials assumes that you have reviewed hello safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="867c7-112">如果您仍然需要的 tooperform 這些工作，以檢閱 hello 開頭[安全措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="867c7-112">If you still need tooperform those tasks, start with reviewing hello [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="867c7-113">請遵循 hello 裝置的特定指示 toounpack，機架掛接，並以纜線連接您的裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-113">Follow hello device specific instructions toounpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="867c7-114">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="867c7-114">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="867c7-115">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="867c7-115">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="867c7-116">您需要系統管理員權限 toocomplete hello 安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="867c7-116">You will need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="867c7-117">我們建議您先檢閱 hello 組態檢查清單。</span><span class="sxs-lookup"><span data-stu-id="867c7-117">We recommend that you review hello configuration checklist before you begin.</span></span> <span data-ttu-id="867c7-118">hello 部署和設定程序可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="867c7-118">hello deployment and configuration process can take some time toocomplete.</span></span>

> [!NOTE]
> <span data-ttu-id="867c7-119">hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-119">hello StorSimple deployment information published on hello Microsoft Azure website applies tooStorSimple 8000 series devices only.</span></span> <span data-ttu-id="867c7-120">如需 hello 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="867c7-120">For complete information about hello 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="867c7-121">如需 7000 系列部署資訊，請參閱 hello [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="867c7-121">For 7000 series deployment information, see hello [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="867c7-122">部署步驟</span><span class="sxs-lookup"><span data-stu-id="867c7-122">Deployment steps</span></span>
<span data-ttu-id="867c7-123">執行下列必要的步驟 tooconfigure StorSimple 裝置，並將它連接 tooyour StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="867c7-123">Perform these required steps tooconfigure your StorSimple device and connect it tooyour StorSimple Manager service.</span></span> <span data-ttu-id="867c7-124">此外 toohello 所需的步驟，選擇性的步驟和程序，您可能需要在 hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="867c7-124">In addition toohello required steps, there are optional steps and procedures you may need during hello deployment.</span></span> <span data-ttu-id="867c7-125">您應該執行每一個選擇性的步驟時，就會指出 hello 逐步部署指示。</span><span class="sxs-lookup"><span data-stu-id="867c7-125">hello step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="867c7-126">步驟</span><span class="sxs-lookup"><span data-stu-id="867c7-126">Step</span></span> | <span data-ttu-id="867c7-127">說明</span><span class="sxs-lookup"><span data-stu-id="867c7-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="867c7-128">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="867c7-128">**PREREQUISITES**</span></span> |<span data-ttu-id="867c7-129">這些需要 toobe 完成在 hello 即將部署的準備。</span><span class="sxs-lookup"><span data-stu-id="867c7-129">These need toobe completed in preparation for hello upcoming deployment.</span></span> |
| [<span data-ttu-id="867c7-130">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="867c7-130">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="867c7-131">使用此檢查清單 toogather 和記錄資訊先前 tooand hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="867c7-131">Use this checklist toogather and record information prior tooand during hello deployment.</span></span> |
| [<span data-ttu-id="867c7-132">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="867c7-132">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="867c7-133">這些驗證 hello 環境是否準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="867c7-133">These  validate hello environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="867c7-134">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="867c7-134">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="867c7-135">這些步驟是必要的 toodeploy StorSimple 裝置在生產環境中的。</span><span class="sxs-lookup"><span data-stu-id="867c7-135">These steps are required toodeploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="867c7-136">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="867c7-136">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="867c7-137">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="867c7-137">Set up cloud management and storage for your   StorSimple device.</span></span> <span data-ttu-id="867c7-138">*如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。</span><span class="sxs-lookup"><span data-stu-id="867c7-138">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="867c7-139">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="867c7-139">Step 2: Get hello service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="867c7-140">使用此索引鍵 tooregister （& s) 連線您的 StorSimple 裝置 hello 管理服務。</span><span class="sxs-lookup"><span data-stu-id="867c7-140">Use this key tooregister & connect your StorSimple device with hello management service.</span></span> |
| [<span data-ttu-id="867c7-141">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="867c7-141">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="867c7-142">Hello 裝置 tooyour 網路連線，並向使用 hello 管理服務的 Azure toocomplete hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="867c7-142">Connect hello device tooyour network and register it with Azure toocomplete hello setup using hello management service.</span></span> |
| [<span data-ttu-id="867c7-143">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="867c7-143">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="867c7-144">選用：更新您的 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="867c7-144">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="867c7-145">使用 hello management 服務 toocomplete hello 裝置安裝程式並啟用它 tooprovide 儲存體。</span><span class="sxs-lookup"><span data-stu-id="867c7-145">Use hello management service toocomplete hello device setup and enable it tooprovide storage.</span></span> |
| [<span data-ttu-id="867c7-146">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="867c7-146">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="867c7-147">建立容器 tooprovision 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-147">Create a container tooprovision volumes.</span></span> <span data-ttu-id="867c7-148">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-148">A volume container has storage   account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> |
| [<span data-ttu-id="867c7-149">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="867c7-149">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="867c7-150">佈建伺服器 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-150">Provision storage volume(s) on hello StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="867c7-151">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="867c7-151">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="867c7-152">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="867c7-152">Optional: Configure MPIO</span></span>](storsimple-configure-mpio-windows-server.md) |<span data-ttu-id="867c7-153">連接伺服器 toohello iSCSI 存放裝置 hello 裝置所提供。</span><span class="sxs-lookup"><span data-stu-id="867c7-153">Connect your servers toohello iSCSI storage provided by hello device.</span></span> <span data-ttu-id="867c7-154">選擇性地設定 MPIO tooensure 伺服器可容許連結、 網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="867c7-154">Optionally configure MPIO tooensure that your servers can tolerate link, network and interface failure.</span></span> |
| [<span data-ttu-id="867c7-155">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="867c7-155">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="867c7-156">設定備份原則 tooprotect 您的資料</span><span class="sxs-lookup"><span data-stu-id="867c7-156">Set up your backup policy tooprotect your data</span></span> |
|  | |
| <span data-ttu-id="867c7-157">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="867c7-157">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="867c7-158">當您部署方案，您可能需要 toorefer toothese 程序。</span><span class="sxs-lookup"><span data-stu-id="867c7-158">You may need toorefer toothese procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="867c7-159">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="867c7-159">Configure a new storage account for hello service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="867c7-160">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="867c7-160">Use PuTTY tooconnect toohello device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="867c7-161">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="867c7-161">Get hello IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="867c7-162">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="867c7-162">Create a manual backup</span></span>](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="867c7-163">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="867c7-163">Deployment configuration checklist</span></span>
<span data-ttu-id="867c7-164">部署您的裝置之前，您必須 toocollect 資訊 tooconfigure hello 軟體在您的 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="867c7-164">Before you deploy your device, you will need toocollect information tooconfigure hello software on your StorSimple device.</span></span> <span data-ttu-id="867c7-165">準備某些事先這項資訊可協助簡化的部署環境中的 hello StorSimple 裝置 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="867c7-165">Preparing some of this information ahead of time will help streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="867c7-166">下載並使用此檢查清單 toonote，向下 hello 設定詳細資料，與部署您的裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-166">Download and use this checklist toonote down hello configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="867c7-167">下載 StorSimple 部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="867c7-167">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="867c7-168">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="867c7-168">Deployment prerequisites</span></span>
<span data-ttu-id="867c7-169">hello 下列各節說明 hello StorSimple Manager 服務和您的 StorSimple 裝置的組態先決條件。</span><span class="sxs-lookup"><span data-stu-id="867c7-169">hello following sections explain hello configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-hello-storsimple-manager-service"></a><span data-ttu-id="867c7-170">Hello StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="867c7-170">For hello StorSimple Manager service</span></span>
<span data-ttu-id="867c7-171">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="867c7-171">Before you begin, make sure that:</span></span>

* <span data-ttu-id="867c7-172">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="867c7-172">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="867c7-173">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="867c7-173">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="867c7-174">Hello StorSimple Manager 服務已啟用 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="867c7-174">Your Microsoft Azure subscription is enabled for hello StorSimple Manager service.</span></span> <span data-ttu-id="867c7-175">您的訂用帳戶應採購 hello [Enterprise 合約](https://azure.microsoft.com/pricing/enterprise-agreement/)。</span><span class="sxs-lookup"><span data-stu-id="867c7-175">Your subscription should be purchased through hello [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="867c7-176">您必須存取 tooterminal 模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="867c7-176">You have access tooterminal emulation software such as PuTTY.</span></span>

### <a name="for-hello-device-in-hello-datacenter"></a><span data-ttu-id="867c7-177">Hello hello 資料中心內的裝置</span><span class="sxs-lookup"><span data-stu-id="867c7-177">For hello device in hello datacenter</span></span>
<span data-ttu-id="867c7-178">設定之前 hello 裝置，請確定您的裝置已完全解除封裝、 掛接在機架上且完整配線的電源、 網路和序列存取如中所述：</span><span class="sxs-lookup"><span data-stu-id="867c7-178">Before configuring hello device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="867c7-179">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="867c7-179">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="867c7-180">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="867c7-180">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="867c7-181">Hello 資料中心中的 hello 網路</span><span class="sxs-lookup"><span data-stu-id="867c7-181">For hello network in hello datacenter</span></span>
<span data-ttu-id="867c7-182">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="867c7-182">Before you begin, make sure that:</span></span>

* <span data-ttu-id="867c7-183">hello 中您資料中心的防火牆連接埠是開啟的 tooallow iSCSI 和雲端流量中所述[StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。</span><span class="sxs-lookup"><span data-stu-id="867c7-183">hello ports in your datacenter firewall are opened tooallow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="867c7-184">逐步部署</span><span class="sxs-lookup"><span data-stu-id="867c7-184">Step-by-step deployment</span></span>
<span data-ttu-id="867c7-185">使用您的 StorSimple 裝置 hello 遵循逐步指示 toodeploy hello 資料中心內。</span><span class="sxs-lookup"><span data-stu-id="867c7-185">Use hello following step-by-step instructions toodeploy your StorSimple device in hello datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="867c7-186">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="867c7-186">Step 1: Create a new service</span></span>
<span data-ttu-id="867c7-187">StorSimple Manager 服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-187">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="867c7-188">執行下列步驟 toocreate hello StorSimple Manager 服務的新執行個體的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-188">Perform hello following steps toocreate a new instance of hello StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="867c7-189">如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。</span><span class="sxs-lookup"><span data-stu-id="867c7-189">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="867c7-190">當您建立磁碟區容器時，將會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="867c7-190">This storage account will be used when you create a volume container.</span></span> 
> 
> * <span data-ttu-id="867c7-191">如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="867c7-191">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span> 
> * <span data-ttu-id="867c7-192">如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="867c7-192">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="867c7-193">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="867c7-193">Step 2: Get hello service registration key</span></span>
<span data-ttu-id="867c7-194">Hello StorSimple Manager 服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="867c7-194">After hello StorSimple Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="867c7-195">這個金鑰是使用的 tooregister，而且與 hello 服務連接您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-195">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="867c7-196">執行下列步驟在 hello 管理入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-196">Perform hello following steps in hello Management Portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="867c7-197">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="867c7-197">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="867c7-198">Hello 遵循程序中所述，您的 StorSimple 裝置的 StorSimple toocomplete hello 初始設定使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="867c7-198">Use Windows PowerShell for StorSimple toocomplete hello initial setup of your StorSimple device as explained in hello following procedure.</span></span> <span data-ttu-id="867c7-199">您將需要 toouse 終端機模擬軟體 toocomplete 此步驟。</span><span class="sxs-lookup"><span data-stu-id="867c7-199">You will need toouse terminal emulation software toocomplete this step.</span></span> <span data-ttu-id="867c7-200">如需詳細資訊，請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="867c7-200">For more information, see [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="867c7-201">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="867c7-201">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="867c7-202">您的 StorSimple 裝置 hello 最低裝置設定，您都必須：</span><span class="sxs-lookup"><span data-stu-id="867c7-202">For hello minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="867c7-203">設定次要 DNS 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-203">Set up hello secondary DNS server.</span></span>
* <span data-ttu-id="867c7-204">至少在一個網路介面上啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="867c7-204">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="867c7-205">Tooboth hello 控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="867c7-205">Assign fixed IP addresses tooboth hello controllers.</span></span>

<span data-ttu-id="867c7-206">執行下列步驟在 hello 管理入口網站 toocomplete hello 最低裝置設定中的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-206">Perform hello following steps in hello Management Portal toocomplete hello minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="867c7-207">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="867c7-207">Step 5: Create a volume container</span></span>
<span data-ttu-id="867c7-208">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-208">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> <span data-ttu-id="867c7-209">您可以開始佈建您的 StorSimple 裝置上的磁碟區之前，您將需要 toocreate 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="867c7-209">You will need toocreate a volume container before you can start provisioning volumes on your StorSimple device.</span></span> 

<span data-ttu-id="867c7-210">執行下列步驟在 hello 管理入口網站 toocreate 磁碟區容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-210">Perform hello following steps in hello Management Portal toocreate a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="867c7-211">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="867c7-211">Step 6: Create a volume</span></span>
<span data-ttu-id="867c7-212">建立磁碟區容器之後，您可以為您的伺服器來佈建 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-212">After you create a volume container, you can provision a storage volume on hello StorSimple device for your servers.</span></span> <span data-ttu-id="867c7-213">執行下列步驟在 hello 管理入口網站 toocreate 磁碟區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-213">Perform hello following steps in hello Management Portal toocreate a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867c7-214">StorSimple Manager 可建立精簡的磁碟區，也可建立完整佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-214">StorSimple Manager can create both thin and fully provisioned volumes.</span></span> <span data-ttu-id="867c7-215">然而，您無法建立部分佈建的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="867c7-215">You cannot however create partially provisioned volumes.</span></span> 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="867c7-216">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="867c7-216">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="867c7-217">hello 步驟會執行 Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="867c7-217">hello following steps are performed on your Windows Server host.</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="867c7-218">Hello 的 StorSimple 解決方案的高可用性，建議您在您的主機伺服器 （選擇性） 先前 tooconfiguring iSCSI 上設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="867c7-218">For hello high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior tooconfiguring iSCSI.</span></span> <span data-ttu-id="867c7-219">在主機伺服器上的 MPIO 設定可確保 hello 伺服器可容許連結、 網路或介面失效。</span><span class="sxs-lookup"><span data-stu-id="867c7-219">MPIO configuration on host servers will ensure that hello servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="867c7-220">MPIO 與 iSCSI 安裝和設定指示 Windows Server 主機上，移過[設定 MPIO StorSimple 裝置的](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="867c7-220">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go too[Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="867c7-221">這些也會包含 hello 步驟 toomount、 初始化及格式化 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="867c7-221">These will also include hello steps toomount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="867c7-222">MPIO 與 iSCSI 安裝和設定指示在 Linux 主機上，移過[設定 MPIO StorSimple Linux 主機](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="867c7-222">For MPIO and iSCSI installation and configuration instructions on a Linux host, go too[Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>
> 
> 

<span data-ttu-id="867c7-223">如果您決定 tooconfigure MPIO，執行下列步驟 toomount hello、 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="867c7-223">If you decide not tooconfigure MPIO, perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="867c7-224">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="867c7-224">Step 8: Take a backup</span></span>
<span data-ttu-id="867c7-225">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="867c7-225">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="867c7-226">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="867c7-226">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="867c7-227">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="867c7-227">Each of these backup types can be **Scheduled** or **Manual**.</span></span> 

<span data-ttu-id="867c7-228">執行下列步驟在 hello 管理入口網站 toocreate 排定的備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="867c7-228">Perform hello following steps in hello Management Portal toocreate a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="867c7-229">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="867c7-229">You can take a manual backup at any time.</span></span> <span data-ttu-id="867c7-230">程序，跳過[建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="867c7-230">For procedures, go too[Create a manual backup](#create-a-manual-backup).</span></span> 

## <a name="configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="867c7-231">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="867c7-231">Configure a new storage account for hello service</span></span>
<span data-ttu-id="867c7-232">這是選擇性的步驟，您需要 tooperform，只有當您未啟用 hello 自動建立儲存體帳戶與您的服務。</span><span class="sxs-lookup"><span data-stu-id="867c7-232">This is an optional step that you need tooperform only if you did not enable hello automatic creation of a storage account with your service.</span></span> <span data-ttu-id="867c7-233">Microsoft Azure 儲存體帳戶是必要的 toocreate StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="867c7-233">A Microsoft Azure storage account is required toocreate a StorSimple volume container.</span></span>

<span data-ttu-id="867c7-234">如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="867c7-234">If you need toocreate an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="867c7-235">執行步驟上 hello hello 管理入口網站中的 hello **StorSimple Manager 服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="867c7-235">Perform hello following steps in hello Management Portal, on hello **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a><span data-ttu-id="867c7-236">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="867c7-236">Use PuTTY tooconnect toohello device serial console</span></span>
<span data-ttu-id="867c7-237">tooconnect tooWindows PowerShell for StorSimple 中，您需要 toouse 終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="867c7-237">tooconnect tooWindows PowerShell for StorSimple, you need toouse terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="867c7-238">當您存取 hello 裝置直接透過 hello 序列主控台或從遠端電腦開啟 telnet 工作階段時，您可以使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="867c7-238">You can use PuTTY when you access hello device directly through hello serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="867c7-239">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="867c7-239">Scan for and apply updates</span></span>
<span data-ttu-id="867c7-240">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="867c7-240">Updating your device can take several hours.</span></span> <span data-ttu-id="867c7-241">執行下列步驟 tooscan 的 hello 和您的裝置上套用更新。</span><span class="sxs-lookup"><span data-stu-id="867c7-241">Perform hello following steps tooscan for and apply updates on your device.</span></span>
<!--can take 1-4 hours--> 

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a><span data-ttu-id="867c7-242">tooupdate 您的裝置</span><span class="sxs-lookup"><span data-stu-id="867c7-242">tooupdate your device</span></span>
1. <span data-ttu-id="867c7-243">Hello 裝置上**快速入門**頁面上，按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="867c7-243">On hello device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="867c7-244">選取 hello 實體裝置，請按一下**維護**，然後按一下**掃描更新**。</span><span class="sxs-lookup"><span data-stu-id="867c7-244">Select hello physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="867c7-245">建立工作 tooscan 可用的更新。</span><span class="sxs-lookup"><span data-stu-id="867c7-245">A job tooscan for available updates is created.</span></span> <span data-ttu-id="867c7-246">如果有可用的更新，hello**掃描更新**變更太**安裝更新**。</span><span class="sxs-lookup"><span data-stu-id="867c7-246">If updates are available, hello **Scan Updates** changes too**Install Updates**.</span></span> <span data-ttu-id="867c7-247">按一下 [安裝更新] 。</span><span class="sxs-lookup"><span data-stu-id="867c7-247">Click **Install Updates**.</span></span> 
3. <span data-ttu-id="867c7-248">更新工作將會建立。</span><span class="sxs-lookup"><span data-stu-id="867c7-248">An update job will be created.</span></span> <span data-ttu-id="867c7-249">監視的瀏覽過您的更新 hello 狀態**作業**。</span><span class="sxs-lookup"><span data-stu-id="867c7-249">Monitor hello status of your update by navigating too**Jobs**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="867c7-250">Hello 更新工作啟動時，它立即顯示 hello 狀態為 50%。</span><span class="sxs-lookup"><span data-stu-id="867c7-250">When hello update job starts, it immediately displays hello status as 50 percent.</span></span> <span data-ttu-id="867c7-251">只有在 hello 更新工作完成後，hello 狀態會變更 too100 百分比。</span><span class="sxs-lookup"><span data-stu-id="867c7-251">hello status changes too100 percent only after hello update job is complete.</span></span> <span data-ttu-id="867c7-252">沒有 hello 更新程序的即時狀態。</span><span class="sxs-lookup"><span data-stu-id="867c7-252">There is no real-time status for hello update process.</span></span>
   > 
   > 
4. <span data-ttu-id="867c7-253">Hello 裝置已成功更新之後，啟用這些已停用資料 2 和 Data 3 網路介面。</span><span class="sxs-lookup"><span data-stu-id="867c7-253">After hello device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="867c7-254">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="867c7-254">Get hello IQN of a Windows Server host</span></span>
<span data-ttu-id="867c7-255">執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server® 2012年的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="867c7-255">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="867c7-256">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="867c7-256">Create a manual backup</span></span>
<span data-ttu-id="867c7-257">執行 hello 遵循您的 StorSimple 裝置上 hello 管理入口網站 toocreate 隨需手動備份單一磁碟區中的步驟。</span><span class="sxs-lookup"><span data-stu-id="867c7-257">Perform hello following steps in hello Management Portal toocreate an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="867c7-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="867c7-258">Next steps</span></span>
* <span data-ttu-id="867c7-259">設定 [虛擬裝置](storsimple-virtual-device-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="867c7-259">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="867c7-260">使用 hello [StorSimple Manager 服務](storsimple-manager-service-administration.md)toomanage StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="867c7-260">Use hello [StorSimple Manager service](storsimple-manager-service-administration.md) toomanage your StorSimple device.</span></span>

