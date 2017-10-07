---
title: "aaaDeploy Azure 入口網站中的您 StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述 hello 步驟和部署執行更新 3 及更新版本和 StorSimple 裝置管理員服務的 hello StorSimple 8000 系列裝置的最佳作法。"
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
ms.openlocfilehash: 28d32d6c0d37169902d9db91701deee4fd99dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-3-and-later"></a><span data-ttu-id="248ba-103">部署您的內部部署 StorSimple 裝置 (Update 3 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="248ba-103">Deploy your on-premises StorSimple device (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="248ba-104">概觀</span><span class="sxs-lookup"><span data-stu-id="248ba-104">Overview</span></span>
<span data-ttu-id="248ba-105">歡迎使用 tooMicrosoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="248ba-105">Welcome tooMicrosoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="248ba-106">這些部署教學課程適用於 8000 系列更新的 tooStorSimple 3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="248ba-106">These deployment tutorials apply tooStorSimple 8000 Series Update 3 or later.</span></span> <span data-ttu-id="248ba-107">這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件，以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="248ba-107">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="248ba-108">這些教學課程中的 hello 資訊假設您已檢閱 hello 安全措施，並解壓縮、 racked，和妥您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="248ba-108">hello information in these tutorials assumes that you have reviewed hello safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="248ba-109">如果您仍然需要的 tooperform 這些工作，以檢閱 hello 開頭[安全措施](storsimple-8000-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="248ba-109">If you still need tooperform those tasks, start with reviewing hello [safety precautions](storsimple-8000-safety.md).</span></span> <span data-ttu-id="248ba-110">請遵循 toounpack，機架掛接，並以纜線連接您的裝置 hello 裝置的特定指示。</span><span class="sxs-lookup"><span data-stu-id="248ba-110">Follow hello device-specific instructions toounpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="248ba-111">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="248ba-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="248ba-112">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="248ba-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="248ba-113">您需要系統管理員權限 toocomplete hello 安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="248ba-113">You need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="248ba-114">我們建議您先檢閱 hello 組態檢查清單。</span><span class="sxs-lookup"><span data-stu-id="248ba-114">We recommend that you review hello configuration checklist before you begin.</span></span> <span data-ttu-id="248ba-115">hello 部署和設定程序可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="248ba-115">hello deployment and configuration process can take some time toocomplete.</span></span>

> [!NOTE]
> <span data-ttu-id="248ba-116">hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。</span><span class="sxs-lookup"><span data-stu-id="248ba-116">hello StorSimple deployment information published on hello Microsoft Azure website applies tooStorSimple 8000 series devices only.</span></span> <span data-ttu-id="248ba-117">如需 hello 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="248ba-117">For complete information about hello 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="248ba-118">如需 7000 系列部署資訊，請參閱 hello [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="248ba-118">For 7000 series deployment information, see hello [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span> 


## <a name="deployment-steps"></a><span data-ttu-id="248ba-119">部署步驟</span><span class="sxs-lookup"><span data-stu-id="248ba-119">Deployment steps</span></span>
<span data-ttu-id="248ba-120">執行下列必要的步驟 tooconfigure StorSimple 裝置，並將它連接 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="248ba-120">Perform these required steps tooconfigure your StorSimple device and connect it tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="248ba-121">此外 toohello 所需的步驟，選擇性的步驟和程序，您可能需要在 hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="248ba-121">In addition toohello required steps, there are optional steps and procedures you may need during hello deployment.</span></span> <span data-ttu-id="248ba-122">您應該執行每一個選擇性的步驟時，就會指出 hello 逐步部署指示。</span><span class="sxs-lookup"><span data-stu-id="248ba-122">hello step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="248ba-123">步驟</span><span class="sxs-lookup"><span data-stu-id="248ba-123">Step</span></span> | <span data-ttu-id="248ba-124">說明</span><span class="sxs-lookup"><span data-stu-id="248ba-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="248ba-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="248ba-125">**PREREQUISITES**</span></span> |<span data-ttu-id="248ba-126">這些都必須在 hello 即將部署的準備完成。</span><span class="sxs-lookup"><span data-stu-id="248ba-126">These must be completed in preparation for hello upcoming deployment.</span></span> |
| [<span data-ttu-id="248ba-127">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="248ba-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="248ba-128">使用此檢查清單 toogather 和記錄資訊前和 hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="248ba-128">Use this checklist toogather and record information before and during hello deployment.</span></span> |
| [<span data-ttu-id="248ba-129">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="248ba-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="248ba-130">這些驗證 hello 環境是否準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="248ba-130">These validate hello environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="248ba-131">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="248ba-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="248ba-132">這些步驟是必要的 toodeploy StorSimple 裝置在生產環境中的。</span><span class="sxs-lookup"><span data-stu-id="248ba-132">These steps are required toodeploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="248ba-133">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="248ba-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="248ba-134">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="248ba-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="248ba-135">*如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。</span><span class="sxs-lookup"><span data-stu-id="248ba-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="248ba-136">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="248ba-136">Step 2: Get hello service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="248ba-137">使用此索引鍵 tooregister （& s) 連線您的 StorSimple 裝置 hello 管理服務。</span><span class="sxs-lookup"><span data-stu-id="248ba-137">Use this key tooregister & connect your StorSimple device with hello management service.</span></span> |
| [<span data-ttu-id="248ba-138">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="248ba-138">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="248ba-139">toocomplete hello 使用 hello 管理服務的安裝程式、 hello 裝置 tooyour 網路連線和使用 Azure 進行註冊。</span><span class="sxs-lookup"><span data-stu-id="248ba-139">toocomplete hello setup using hello management service, connect hello device tooyour network and register it with Azure.</span></span> |
| [<span data-ttu-id="248ba-140">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="248ba-140">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="248ba-141">選用：更新您的 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="248ba-141">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="248ba-142">使用 hello management 服務 toocomplete hello 裝置安裝程式並啟用它 tooprovide 儲存體。</span><span class="sxs-lookup"><span data-stu-id="248ba-142">Use hello management service toocomplete hello device setup and enable it tooprovide storage.</span></span> |
| [<span data-ttu-id="248ba-143">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="248ba-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="248ba-144">建立容器 tooprovision 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-144">Create a container tooprovision volumes.</span></span> <span data-ttu-id="248ba-145">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-145">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> |
| [<span data-ttu-id="248ba-146">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="248ba-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="248ba-147">佈建伺服器 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-147">Provision storage volumes on hello StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="248ba-148">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="248ba-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="248ba-149">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="248ba-149">Optional: Configure MPIO</span></span>](storsimple-8000-configure-mpio-windows-server.md) |<span data-ttu-id="248ba-150">連接伺服器 toohello iSCSI 存放裝置 hello 裝置所提供。</span><span class="sxs-lookup"><span data-stu-id="248ba-150">Connect your servers toohello iSCSI storage provided by hello device.</span></span> <span data-ttu-id="248ba-151">選擇性地設定 MPIO tooensure 伺服器可容許連結、 網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="248ba-151">Optionally configure MPIO tooensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="248ba-152">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="248ba-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="248ba-153">設定備份原則 tooprotect 您的資料</span><span class="sxs-lookup"><span data-stu-id="248ba-153">Set up your backup policy tooprotect your data</span></span> |
|  | |
| <span data-ttu-id="248ba-154">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="248ba-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="248ba-155">當您部署方案，您可能需要 toorefer toothese 程序。</span><span class="sxs-lookup"><span data-stu-id="248ba-155">You may need toorefer toothese procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="248ba-156">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="248ba-156">Configure a new storage account for hello service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="248ba-157">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="248ba-157">Use PuTTY tooconnect toohello device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="248ba-158">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="248ba-158">Get hello IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="248ba-159">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="248ba-159">Create a manual backup</span></span>](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a><span data-ttu-id="248ba-160">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="248ba-160">Deployment configuration checklist</span></span>
<span data-ttu-id="248ba-161">部署您的裝置之前，您需要 toocollect 資訊 tooconfigure hello 軟體在您的 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="248ba-161">Before you deploy your device, you need toocollect information tooconfigure hello software on your StorSimple device.</span></span> <span data-ttu-id="248ba-162">正在準備某些時間有助於此資訊的部署環境中的 hello StorSimple 裝置的簡化 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="248ba-162">Preparing some of this information ahead of time helps streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="248ba-163">下載並使用此檢查清單 toonote，向下 hello 設定詳細資料，與部署您的裝置。</span><span class="sxs-lookup"><span data-stu-id="248ba-163">Download and use this checklist toonote down hello configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="248ba-164">下載 StorSimple 部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="248ba-164">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="248ba-165">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="248ba-165">Deployment prerequisites</span></span>
<span data-ttu-id="248ba-166">hello 下列各節說明 hello StorSimple 裝置 Manager 服務和您的 StorSimple 裝置的組態先決條件。</span><span class="sxs-lookup"><span data-stu-id="248ba-166">hello following sections explain hello configuration prerequisites for your StorSimple Device Manager service and your StorSimple device.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="248ba-167">Hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="248ba-167">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="248ba-168">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="248ba-168">Before you begin, make sure that:</span></span>

* <span data-ttu-id="248ba-169">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="248ba-169">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="248ba-170">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="248ba-170">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="248ba-171">Hello StorSimple 裝置管理員服務已啟用 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="248ba-171">Your Microsoft Azure subscription is enabled for hello StorSimple Device Manager service.</span></span> <span data-ttu-id="248ba-172">您的訂用帳戶應採購 hello [Enterprise 合約](https://azure.microsoft.com/pricing/enterprise-agreement/)。</span><span class="sxs-lookup"><span data-stu-id="248ba-172">Your subscription should be purchased through hello [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="248ba-173">您必須存取 tooterminal 模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="248ba-173">You have access tooterminal emulation software such as PuTTY.</span></span>

### <a name="for-hello-device-in-hello-datacenter"></a><span data-ttu-id="248ba-174">Hello hello 資料中心內的裝置</span><span class="sxs-lookup"><span data-stu-id="248ba-174">For hello device in hello datacenter</span></span>
<span data-ttu-id="248ba-175">設定之前 hello 裝置，請確定您的裝置已完全解除封裝、 掛接在機架上且完整配線的電源、 網路和序列存取如中所述：</span><span class="sxs-lookup"><span data-stu-id="248ba-175">Before configuring hello device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="248ba-176">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="248ba-176">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="248ba-177">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="248ba-177">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="248ba-178">Hello 資料中心中的 hello 網路</span><span class="sxs-lookup"><span data-stu-id="248ba-178">For hello network in hello datacenter</span></span>
<span data-ttu-id="248ba-179">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="248ba-179">Before you begin, make sure that:</span></span>

* <span data-ttu-id="248ba-180">hello 中您資料中心的防火牆連接埠是開啟的 tooallow iSCSI 和雲端流量中所述[StorSimple 裝置的網路需求](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)。</span><span class="sxs-lookup"><span data-stu-id="248ba-180">hello ports in your datacenter firewall are opened tooallow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="248ba-181">逐步部署</span><span class="sxs-lookup"><span data-stu-id="248ba-181">Step-by-step deployment</span></span>
<span data-ttu-id="248ba-182">使用您的 StorSimple 裝置 hello 遵循逐步指示 toodeploy hello 資料中心內。</span><span class="sxs-lookup"><span data-stu-id="248ba-182">Use hello following step-by-step instructions toodeploy your StorSimple device in hello datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="248ba-183">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="248ba-183">Step 1: Create a new service</span></span>
<span data-ttu-id="248ba-184">StorSimple 裝置管理員服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="248ba-184">A StorSimple Device Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="248ba-185">執行下列步驟 toocreate hello StorSimple 裝置管理員服務的執行個體的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-185">Perform hello following steps toocreate an instance of hello StorSimple Device Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="248ba-186">如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。</span><span class="sxs-lookup"><span data-stu-id="248ba-186">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="248ba-187">當您建立磁碟區容器時，會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="248ba-187">This storage account is used when you create a volume container.</span></span>
>
> * <span data-ttu-id="248ba-188">如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="248ba-188">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="248ba-189">如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="248ba-189">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>


## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="248ba-190">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="248ba-190">Step 2: Get hello service registration key</span></span>
<span data-ttu-id="248ba-191">Hello StorSimple 裝置管理員服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="248ba-191">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="248ba-192">這個金鑰是使用的 tooregister，而且與 hello 服務連接您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="248ba-192">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="248ba-193">執行下列步驟在 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-193">Perform hello following steps in hello Azure portal.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="248ba-194">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="248ba-194">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="248ba-195">Hello 遵循程序中所述，您的 StorSimple 裝置的 StorSimple toocomplete hello 初始設定使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="248ba-195">Use Windows PowerShell for StorSimple toocomplete hello initial setup of your StorSimple device as explained in hello following procedure.</span></span> <span data-ttu-id="248ba-196">您需要 toouse 終端機模擬軟體 toocomplete 此步驟。</span><span class="sxs-lookup"><span data-stu-id="248ba-196">You need toouse terminal emulation software toocomplete this step.</span></span> <span data-ttu-id="248ba-197">如需詳細資訊，請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="248ba-197">For more information, see [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-8000-configure-and-register-device-u2](../../includes/storsimple-8000-configure-and-register-device-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="248ba-198">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="248ba-198">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="248ba-199">您的 StorSimple 裝置 hello 最低裝置設定，您都必須：</span><span class="sxs-lookup"><span data-stu-id="248ba-199">For hello minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="248ba-200">為裝置提供 [易記名稱]。</span><span class="sxs-lookup"><span data-stu-id="248ba-200">Provide a friendly name for your device.</span></span>
* <span data-ttu-id="248ba-201">設定裝置時區 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-201">Set hello device time zone.</span></span>
* <span data-ttu-id="248ba-202">Tooboth hello 控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="248ba-202">Assign fixed IP addresses tooboth hello controllers.</span></span>

<span data-ttu-id="248ba-203">執行下列步驟在 hello Azure 入口網站 toocomplete hello 最低裝置設定中的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-203">Perform hello following steps in hello Azure portal toocomplete hello minimum device setup.</span></span>

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="248ba-204">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="248ba-204">Step 5: Create a volume container</span></span>
<span data-ttu-id="248ba-205">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-205">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> <span data-ttu-id="248ba-206">您可以開始佈建您的 StorSimple 裝置上的磁碟區之前，您將需要 toocreate 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="248ba-206">You will need toocreate a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="248ba-207">執行下列步驟在 hello Azure 入口網站 toocreate 磁碟區容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-207">Perform hello following steps in hello Azure portal toocreate a volume container.</span></span>

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="248ba-208">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="248ba-208">Step 6: Create a volume</span></span>
<span data-ttu-id="248ba-209">建立磁碟區容器之後，您可以為您的伺服器來佈建 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-209">After you create a volume container, you can provision a storage volume on hello StorSimple device for your servers.</span></span> <span data-ttu-id="248ba-210">執行下列步驟在 hello Azure 入口網站 toocreate 磁碟區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-210">Perform hello following steps in hello Azure portal toocreate a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="248ba-211">StorSimple 裝置管理員可建立精簡的磁碟區，也可建立完整佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-211">StorSimple Device Manager can create both thin and fully provisioned volumes.</span></span> <span data-ttu-id="248ba-212">然而，您無法建立部分佈建的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="248ba-212">You cannot however create partially provisioned volumes.</span></span>


[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="248ba-213">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="248ba-213">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="248ba-214">hello 步驟會執行 Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="248ba-214">hello following steps are performed on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="248ba-215">Hello 的 StorSimple 解決方案的高可用性，建議您在您的主機伺服器 （選擇性） 先前 tooconfiguring iSCSI 上設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="248ba-215">For hello high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior tooconfiguring iSCSI.</span></span> <span data-ttu-id="248ba-216">在主機伺服器上的 MPIO 設定可確保 hello 伺服器可容許連結、 網路或介面失效。</span><span class="sxs-lookup"><span data-stu-id="248ba-216">MPIO configuration on host servers will ensure that hello servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="248ba-217">MPIO 與 iSCSI 安裝和設定指示 Windows Server 主機上，移過[設定 MPIO StorSimple 裝置的](storsimple-8000-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="248ba-217">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go too[Configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="248ba-218">其中也包括 hello 步驟 toomount、 初始化及格式化 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="248ba-218">These also include hello steps toomount, initialize, and format StorSimple volumes.</span></span>
> * <span data-ttu-id="248ba-219">MPIO 與 iSCSI 安裝和設定指示在 Linux 主機上，移過[設定 MPIO StorSimple Linux 主機](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="248ba-219">For MPIO and iSCSI installation and configuration instructions on a Linux host, go too[Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>

<span data-ttu-id="248ba-220">如果您決定 tooconfigure MPIO，執行下列步驟 toomount hello、 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="248ba-220">If you decide not tooconfigure MPIO, perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-8000-mount-initialize-format-volume](../../includes/storsimple-8000-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="248ba-221">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="248ba-221">Step 8: Take a backup</span></span>
<span data-ttu-id="248ba-222">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="248ba-222">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="248ba-223">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="248ba-223">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="248ba-224">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="248ba-224">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="248ba-225">執行下列步驟在 hello Azure 入口網站 toocreate 排定的備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="248ba-225">Perform hello following steps in hello Azure portal toocreate a scheduled backup.</span></span>

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

<span data-ttu-id="248ba-226">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="248ba-226">You can take a manual backup at any time.</span></span> <span data-ttu-id="248ba-227">程序，跳過[建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="248ba-227">For procedures, go too[Create a manual backup](#create-a-manual-backup).</span></span>

<span data-ttu-id="248ba-228">您已完成 hello 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="248ba-228">You have completed hello device configuration.</span></span>

## <a name="configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="248ba-229">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="248ba-229">Configure a new storage account for hello service</span></span>
<span data-ttu-id="248ba-230">這是選擇性的步驟，您需要 tooperform，只有當您未啟用 hello 自動建立儲存體帳戶與您的服務。</span><span class="sxs-lookup"><span data-stu-id="248ba-230">This is an optional step that you need tooperform only if you did not enable hello automatic creation of a storage account with your service.</span></span> <span data-ttu-id="248ba-231">Microsoft Azure 儲存體帳戶是必要的 toocreate StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="248ba-231">A Microsoft Azure storage account is required toocreate a StorSimple volume container.</span></span>

<span data-ttu-id="248ba-232">如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="248ba-232">If you need toocreate an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="248ba-233">執行下列步驟在 hello hello 上的 Azure 入口網站中的 hello **StorSimple 裝置管理員服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="248ba-233">Perform hello following steps in hello Azure portal, on hello **StorSimple Device Manager service** page.</span></span>

[!INCLUDE [storsimple-8000-configure-new-storage-account-u2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a><span data-ttu-id="248ba-234">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="248ba-234">Use PuTTY tooconnect toohello device serial console</span></span>
<span data-ttu-id="248ba-235">tooconnect tooWindows PowerShell for StorSimple 中，您需要 toouse 終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="248ba-235">tooconnect tooWindows PowerShell for StorSimple, you need toouse terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="248ba-236">當您存取 hello 裝置直接透過 hello 序列主控台或從遠端電腦開啟 telnet 工作階段時，您可以使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="248ba-236">You can use PuTTY when you access hello device directly through hello serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="248ba-237">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="248ba-237">Scan for and apply updates</span></span>
<span data-ttu-id="248ba-238">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="248ba-238">Updating your device can take several hours.</span></span> <span data-ttu-id="248ba-239">如需有關如何 tooinstall hello 最新的更新詳細的步驟，請移過[安裝更新的 4](storsimple-8000-install-update-4.md)。</span><span class="sxs-lookup"><span data-stu-id="248ba-239">For detailed steps on how tooinstall hello latest update, go too[Install Update 4](storsimple-8000-install-update-4.md).</span></span>


## <a name="get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="248ba-240">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="248ba-240">Get hello IQN of a Windows Server host</span></span>
<span data-ttu-id="248ba-241">執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server® 2012年的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="248ba-241">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="248ba-242">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="248ba-242">Create a manual backup</span></span>
<span data-ttu-id="248ba-243">執行 hello 遵循您的 StorSimple 裝置上 hello Azure 入口網站 toocreate 隨需手動備份的單一磁碟區中的步驟。</span><span class="sxs-lookup"><span data-stu-id="248ba-243">Perform hello following steps in hello Azure portal toocreate an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="248ba-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="248ba-244">Next steps</span></span>
* <span data-ttu-id="248ba-245">[設定 StorSimple 雲端設備](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="248ba-245">[Configure a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>
* <span data-ttu-id="248ba-246">[使用 hello StorSimple 裝置管理員服務 toomanage StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="248ba-246">[Use hello StorSimple Device Manager service toomanage your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

