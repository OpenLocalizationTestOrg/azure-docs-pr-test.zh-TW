---
title: "政府入口網站中的 aaaDeploy StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述 hello 步驟和最佳做法部署 hello StorSimple 8000 系列裝置執行 Update 3 及更新版本中，與 hello 服務在 hello Azure 政府入口網站。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: ea643cd59dcdf17482268d14c1348a3b5fb098b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a><span data-ttu-id="bf7ca-103">部署在內部部署 StorSimple 裝置在 hello 政府入口網站</span><span class="sxs-lookup"><span data-stu-id="bf7ca-103">Deploy your on-premises StorSimple device in hello Government portal</span></span>

## <a name="overview"></a><span data-ttu-id="bf7ca-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bf7ca-104">Overview</span></span>
<span data-ttu-id="bf7ca-105">歡迎使用 tooMicrosoft Azure StorSimple 裝置部署。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-105">Welcome tooMicrosoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="bf7ca-106">Toohello StorSimple 8000 系列執行 Update 3 軟體或更新版本在 hello Azure 政府入口網站，就會套用這些部署教學課程。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-106">These deployment tutorials apply toohello StorSimple 8000 Series running Update 3 software or later in hello Azure Government portal.</span></span> <span data-ttu-id="bf7ca-107">這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件的清單，以及詳細的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-107">This series of tutorials includes a configuration checklist, a list of configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="bf7ca-108">這些教學課程中的 hello 資訊假設您已檢閱 hello 安全措施，並解壓縮、 racked，和妥您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-108">hello information in these tutorials assumes that you have reviewed hello safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="bf7ca-109">如果您仍然需要的 tooperform 這些工作，以檢閱 hello 開頭[安全措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-109">If you still need tooperform those tasks, start with reviewing hello [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="bf7ca-110">請遵循 toounpack，機架掛接，並以纜線連接您的裝置 hello 裝置的特定指示。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-110">Follow hello device-specific instructions toounpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="bf7ca-111">打開封裝、掛接機架，並將纜線接上 8100</span><span class="sxs-lookup"><span data-stu-id="bf7ca-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="bf7ca-112">打開封裝、掛接機架，並將纜線接上 8600</span><span class="sxs-lookup"><span data-stu-id="bf7ca-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="bf7ca-113">您需要系統管理員權限 toocomplete hello 安裝和設定程序。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-113">You will need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="bf7ca-114">我們建議您先檢閱 hello 組態檢查清單。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-114">We recommend that you review hello configuration checklist before you begin.</span></span> <span data-ttu-id="bf7ca-115">hello 部署和設定程序可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-115">hello deployment and configuration process can take some time toocomplete.</span></span>

> [!NOTE]
> <span data-ttu-id="bf7ca-116">hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-116">hello StorSimple deployment information published on hello Microsoft Azure website applies tooStorSimple 8000 series devices only.</span></span> <span data-ttu-id="bf7ca-117">如需 hello 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-117">For complete information about hello 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="bf7ca-118">如需 7000 系列部署資訊，請參閱 hello [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-118">For 7000 series deployment information, see hello [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>


## <a name="deployment-steps"></a><span data-ttu-id="bf7ca-119">部署步驟</span><span class="sxs-lookup"><span data-stu-id="bf7ca-119">Deployment steps</span></span>
<span data-ttu-id="bf7ca-120">執行下列必要的步驟 tooconfigure StorSimple 裝置，並將它連接 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-120">Perform these required steps tooconfigure your StorSimple device and connect it tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="bf7ca-121">此外 toohello 所需的步驟，選擇性的步驟和程序，您可能需要 toocomplete hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-121">In addition toohello required steps, there are optional steps and procedures that you may need toocomplete during hello deployment.</span></span> <span data-ttu-id="bf7ca-122">您應該執行每一個選擇性的步驟時，就會指出 hello 逐步部署指示。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-122">hello step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="bf7ca-123">步驟</span><span class="sxs-lookup"><span data-stu-id="bf7ca-123">Step</span></span> | <span data-ttu-id="bf7ca-124">說明</span><span class="sxs-lookup"><span data-stu-id="bf7ca-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf7ca-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="bf7ca-125">**PREREQUISITES**</span></span> |<span data-ttu-id="bf7ca-126">這些需要 toobe 完成在 hello 即將部署的準備。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-126">These need toobe completed in preparation for hello upcoming deployment.</span></span> |
| [<span data-ttu-id="bf7ca-127">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="bf7ca-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="bf7ca-128">使用此檢查清單 toogather 和記錄資訊先前 tooand hello 部署期間。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-128">Use this checklist toogather and record information prior tooand during hello deployment.</span></span> |
| [<span data-ttu-id="bf7ca-129">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="bf7ca-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="bf7ca-130">這些驗證該 hello 環境是否準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-130">These  validate that hello environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="bf7ca-131">**逐步部署**</span><span class="sxs-lookup"><span data-stu-id="bf7ca-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="bf7ca-132">這些步驟是必要的 toodeploy StorSimple 裝置在生產環境中的。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-132">These steps are required toodeploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="bf7ca-133">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="bf7ca-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="bf7ca-134">設定雲端管理和 StorSimple 裝置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="bf7ca-135">*如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="bf7ca-136">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="bf7ca-136">Step 2: Get hello service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="bf7ca-137">使用此索引鍵 tooregister 和連線您的 StorSimple 裝置 hello 管理服務。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-137">Use this key tooregister and connect your StorSimple device with hello management service.</span></span> |
| [<span data-ttu-id="bf7ca-138">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="bf7ca-138">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="bf7ca-139">Hello 裝置 tooyour 網路連線，並向使用 hello 管理服務的 Azure toocomplete hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-139">Connect hello device tooyour network and register it with Azure toocomplete hello setup using hello management service.</span></span> |
| [<span data-ttu-id="bf7ca-140">步驟 4: Hello 完成最低裝置設定</span><span class="sxs-lookup"><span data-stu-id="bf7ca-140">Step 4: Complete hello minimum device setup</span></span>](#step-4-complete-minimum-device-setup) </br><span data-ttu-id="bf7ca-141">選用：更新您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-141">Optional: Update your StorSimple device.</span></span> |<span data-ttu-id="bf7ca-142">使用 hello management 服務 toocomplete hello 裝置安裝程式並啟用它 tooprovide 儲存體。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-142">Use hello management service toocomplete hello device setup and enable it tooprovide storage.</span></span> |
| [<span data-ttu-id="bf7ca-143">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="bf7ca-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="bf7ca-144">建立容器 tooprovision 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-144">Create a container tooprovision volumes.</span></span> <span data-ttu-id="bf7ca-145">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-145">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> |
| [<span data-ttu-id="bf7ca-146">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="bf7ca-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="bf7ca-147">佈建伺服器 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-147">Provision storage volume(s) on hello StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="bf7ca-148">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="bf7ca-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume) </br><span data-ttu-id="bf7ca-149">選用：設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-149">Optional: Configure MPIO.</span></span> |<span data-ttu-id="bf7ca-150">連接伺服器 toohello iSCSI 存放裝置 hello 裝置所提供。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-150">Connect your servers toohello iSCSI storage provided by hello device.</span></span> <span data-ttu-id="bf7ca-151">（選擇性） 設定 MPIO tooensure 伺服器可容許連結、 網路和介面失敗。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-151">Optionally, configure MPIO tooensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="bf7ca-152">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="bf7ca-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="bf7ca-153">設定備份原則 tooprotect 您的資料</span><span class="sxs-lookup"><span data-stu-id="bf7ca-153">Set up your backup policy tooprotect your data</span></span> |
|  | |
| <span data-ttu-id="bf7ca-154">**其他程序**</span><span class="sxs-lookup"><span data-stu-id="bf7ca-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="bf7ca-155">當您部署方案，您可能需要 toorefer toothese 程序。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-155">You may need toorefer toothese procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="bf7ca-156">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="bf7ca-156">Configure a new storage account for hello service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="bf7ca-157">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="bf7ca-157">Use PuTTY tooconnect toohello device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="bf7ca-158">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="bf7ca-158">Scan for and apply updates</span></span>](#scan-for-and-apply-updates) | |
| [<span data-ttu-id="bf7ca-159">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="bf7ca-159">Get hello IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="bf7ca-160">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="bf7ca-160">Create a manual backup</span></span>](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a><span data-ttu-id="bf7ca-161">部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="bf7ca-161">Deployment configuration checklist</span></span>
<span data-ttu-id="bf7ca-162">部署您的 StorSimple 裝置之前，您將需要 toocollect 資訊 tooconfigure hello 軟體在裝置上。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-162">Before you deploy your StorSimple device, you will need toocollect information tooconfigure hello software on your device.</span></span> <span data-ttu-id="bf7ca-163">準備某些事先這項資訊可協助簡化的部署環境中的 hello StorSimple 裝置 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-163">Preparing some of this information ahead of time will help streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="bf7ca-164">下載並使用此檢查清單 toonote hello 設定詳細資料，與部署您的裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-164">Download and use this checklist toonote hello configuration details as you deploy your device.</span></span>

[<span data-ttu-id="bf7ca-165">下載 StorSimple 部署設定檢查清單</span><span class="sxs-lookup"><span data-stu-id="bf7ca-165">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="bf7ca-166">部署必要條件</span><span class="sxs-lookup"><span data-stu-id="bf7ca-166">Deployment prerequisites</span></span>
<span data-ttu-id="bf7ca-167">hello 下列各節說明 hello StorSimple 裝置 Manager 服務和您的 StorSimple 裝置的組態先決條件。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-167">hello following sections explain hello configuration prerequisites for your StorSimple Device Manager service and your StorSimple device.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="bf7ca-168">Hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="bf7ca-168">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="bf7ca-169">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="bf7ca-169">Before you begin, make sure that:</span></span>

* <span data-ttu-id="bf7ca-170">您擁有的 Microsoft 帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-170">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="bf7ca-171">您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-171">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="bf7ca-172">Hello StorSimple 裝置管理員服務已啟用 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-172">Your Microsoft Azure subscription is enabled for hello StorSimple Device Manager service.</span></span> <span data-ttu-id="bf7ca-173">您的訂用帳戶應採購 hello [Enterprise 合約](https://azure.microsoft.com/pricing/enterprise-agreement/)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-173">Your subscription should be purchased through hello [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="bf7ca-174">您必須存取 tooterminal 模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-174">You have access tooterminal emulation software such as PuTTY.</span></span>

### <a name="for-hello-device-in-hello-datacenter"></a><span data-ttu-id="bf7ca-175">Hello hello 資料中心內的裝置</span><span class="sxs-lookup"><span data-stu-id="bf7ca-175">For hello device in hello datacenter</span></span>
<span data-ttu-id="bf7ca-176">在設定之前 hello 裝置，請確認：</span><span class="sxs-lookup"><span data-stu-id="bf7ca-176">Before configuring hello device, make sure that:</span></span>

* <span data-ttu-id="bf7ca-177">您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：</span><span class="sxs-lookup"><span data-stu-id="bf7ca-177">Your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>
  
  * [<span data-ttu-id="bf7ca-178">打開封裝、掛接機架，並將纜線接上 8100 裝置</span><span class="sxs-lookup"><span data-stu-id="bf7ca-178">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
  * [<span data-ttu-id="bf7ca-179">打開封裝、掛接機架，並將纜線接上 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="bf7ca-179">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="bf7ca-180">Hello 資料中心中的 hello 網路</span><span class="sxs-lookup"><span data-stu-id="bf7ca-180">For hello network in hello datacenter</span></span>
<span data-ttu-id="bf7ca-181">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="bf7ca-181">Before you begin, make sure that:</span></span>

* <span data-ttu-id="bf7ca-182">hello 中您資料中心的防火牆連接埠是開啟的 tooallow iSCSI 和雲端流量中所述[StorSimple 裝置的網路需求](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-182">hello ports in your datacenter firewall are opened tooallow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="bf7ca-183">逐步部署</span><span class="sxs-lookup"><span data-stu-id="bf7ca-183">Step-by-step deployment</span></span>
<span data-ttu-id="bf7ca-184">使用您的 StorSimple 裝置 hello 遵循逐步指示 toodeploy hello 資料中心內。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-184">Use hello following step-by-step instructions toodeploy your StorSimple device in hello datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="bf7ca-185">步驟 1：建立新的服務</span><span class="sxs-lookup"><span data-stu-id="bf7ca-185">Step 1: Create a new service</span></span>
<span data-ttu-id="bf7ca-186">StorSimple 裝置管理員服務可以管理多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-186">A StorSimple Device Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="bf7ca-187">執行下列步驟 toocreate hello StorSimple 裝置管理員服務的新執行個體的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-187">Perform hello following steps toocreate a new instance of hello StorSimple Device Manager service.</span></span>

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> <span data-ttu-id="bf7ca-188">如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-188">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="bf7ca-189">當您建立磁碟區容器時，將會使用此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-189">This storage account will be used when you create a volume container.</span></span>
> 
> * <span data-ttu-id="bf7ca-190">如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-190">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="bf7ca-191">如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-191">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>


## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="bf7ca-192">步驟 2： 取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="bf7ca-192">Step 2: Get hello service registration key</span></span>
<span data-ttu-id="bf7ca-193">Hello StorSimple 裝置管理員服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-193">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="bf7ca-194">這個金鑰是使用的 tooregister，而且連接您的 StorSimple 裝置 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-194">This key is used tooregister and connect your StorSimple device toohello service.</span></span>

<span data-ttu-id="bf7ca-195">執行下列步驟在 hello 政府入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-195">Perform hello following steps in hello Government portal.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="bf7ca-196">步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊</span><span class="sxs-lookup"><span data-stu-id="bf7ca-196">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="bf7ca-197">Hello 遵循程序中所述，您的 StorSimple 裝置的 StorSimple toocomplete hello 初始設定使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-197">Use Windows PowerShell for StorSimple toocomplete hello initial setup of your StorSimple device as explained in hello following procedure.</span></span> <span data-ttu-id="bf7ca-198">您將需要 toouse 終端機模擬軟體 toocomplete 此步驟。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-198">You will need toouse terminal emulation software toocomplete this step.</span></span> <span data-ttu-id="bf7ca-199">如需詳細資訊，請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-199">For more information, see [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="bf7ca-200">步驟 4：完成最小量裝置設定</span><span class="sxs-lookup"><span data-stu-id="bf7ca-200">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="bf7ca-201">您的 StorSimple 裝置 hello 最低裝置設定，您都必須：</span><span class="sxs-lookup"><span data-stu-id="bf7ca-201">For hello minimum device configuration of your StorSimple device, you are required to:</span></span>

* <span data-ttu-id="bf7ca-202">為裝置提供 [易記名稱]。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-202">Provide a friendly name for your device.</span></span>
* <span data-ttu-id="bf7ca-203">設定裝置時區 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-203">Set hello device time zone.</span></span>
* <span data-ttu-id="bf7ca-204">Tooboth hello 控制器指派固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-204">Assign fixed IP addresses tooboth hello controllers.</span></span>

<span data-ttu-id="bf7ca-205">執行下列步驟在 hello Azure 政府入口 toocomplete hello 最低裝置設定中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-205">Perform hello following steps in hello Azure Government portal toocomplete hello minimum device setup.</span></span>

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="bf7ca-206">步驟 5：建立磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="bf7ca-206">Step 5: Create a volume container</span></span>
<span data-ttu-id="bf7ca-207">磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-207">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> <span data-ttu-id="bf7ca-208">您可以開始佈建您的 StorSimple 裝置上的磁碟區之前，您將需要 toocreate 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-208">You will need toocreate a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="bf7ca-209">執行下列步驟在 hello 政府入口 toocreate 磁碟區容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-209">Perform hello following steps in hello Government portal toocreate a volume container.</span></span>

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="bf7ca-210">步驟 6：建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="bf7ca-210">Step 6: Create a volume</span></span>
<span data-ttu-id="bf7ca-211">建立磁碟區容器之後，您可以為您的伺服器來佈建 hello StorSimple 裝置上的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-211">After you create a volume container, you can provision a storage volume on hello StorSimple device for your servers.</span></span> <span data-ttu-id="bf7ca-212">執行下列步驟在 hello 政府入口 toocreate 磁碟區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-212">Perform hello following steps in hello Government portal toocreate a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf7ca-213">StorSimple 裝置管理員只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-213">StorSimple Device Manager can create only thinly provisioned volumes.</span></span>  <span data-ttu-id="bf7ca-214">然而，您無法建立部分佈建的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-214">You cannot however create partially provisioned volumes.</span></span>

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="bf7ca-215">步驟 7：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="bf7ca-215">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="bf7ca-216">請在 Windows Server 主機上執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-216">Perform these steps on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="bf7ca-217">Hello 的 StorSimple 解決方案的高可用性，建議您在您的主機伺服器 （選擇性） 先前 tooconfiguring iSCSI 上設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-217">For hello high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior tooconfiguring iSCSI.</span></span> <span data-ttu-id="bf7ca-218">在主機伺服器上的 MPIO 設定可確保 hello 伺服器可容許連結、 網路或介面失效。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-218">MPIO configuration on host servers will ensure that hello servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="bf7ca-219">MPIO 與 iSCSI 安裝和設定指示 Windows Server 主機上，移過[設定 MPIO StorSimple 裝置的](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-219">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go too[Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="bf7ca-220">這些也會包含 hello 步驟 toomount、 初始化及格式化 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-220">These will also include hello steps toomount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="bf7ca-221">MPIO 與 iSCSI 安裝和設定指示在 Linux 主機上，移過[設定 MPIO StorSimple Linux 主機](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="bf7ca-221">For MPIO and iSCSI installation and configuration instructions on a Linux host, go too[Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>

<span data-ttu-id="bf7ca-222">如果您決定 tooconfigure MPIO，執行下列步驟 toomount hello、 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-222">If you decide not tooconfigure MPIO, perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="bf7ca-223">步驟 8：進行備份</span><span class="sxs-lookup"><span data-stu-id="bf7ca-223">Step 8: Take a backup</span></span>
<span data-ttu-id="bf7ca-224">備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-224">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="bf7ca-225">您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-225">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="bf7ca-226">每一種備份類型都可以是 [排程] 或 [手動]。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-226">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="bf7ca-227">執行下列步驟在 hello 政府入口 toocreate 排定的備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-227">Perform hello following steps in hello Government portal toocreate a scheduled backup.</span></span>

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

<span data-ttu-id="bf7ca-228">您可以隨時進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-228">You can take a manual backup at any time.</span></span> <span data-ttu-id="bf7ca-229">程序，跳過[建立手動備份](#create-a-manual-backup)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-229">For procedures, go too[Create a manual backup](#create-a-manual-backup).</span></span>

## <a name="configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="bf7ca-230">設定新的儲存體帳戶 hello 服務</span><span class="sxs-lookup"><span data-stu-id="bf7ca-230">Configure a new storage account for hello service</span></span>
<span data-ttu-id="bf7ca-231">這是選擇性的步驟，您需要 tooperform，只有當您未啟用 hello 自動建立儲存體帳戶與您的服務。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-231">This is an optional step that you need tooperform only if you did not enable hello automatic creation of a storage account with your service.</span></span> <span data-ttu-id="bf7ca-232">Microsoft Azure 儲存體帳戶是必要的 toocreate StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-232">A Microsoft Azure storage account is required toocreate a StorSimple volume container.</span></span>

<span data-ttu-id="bf7ca-233">如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-233">If you need toocreate an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="bf7ca-234">執行下列步驟在 hello 政府入口網站上 hello hello **StorSimple 裝置管理員服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-234">Perform hello following steps in hello Government portal, on hello **StorSimple Device Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a><span data-ttu-id="bf7ca-235">使用 PuTTY tooconnect toohello 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="bf7ca-235">Use PuTTY tooconnect toohello device serial console</span></span>
<span data-ttu-id="bf7ca-236">tooconnect tooWindows PowerShell for StorSimple 中，您需要 toouse 終端機模擬軟體，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-236">tooconnect tooWindows PowerShell for StorSimple, you need toouse terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="bf7ca-237">當您存取 hello 裝置直接透過 hello 序列主控台或從遠端電腦開啟 telnet 工作階段時，您可以使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-237">You can use PuTTY when you access hello device directly through hello serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="bf7ca-238">掃描並套用更新</span><span class="sxs-lookup"><span data-stu-id="bf7ca-238">Scan for and apply updates</span></span>
<span data-ttu-id="bf7ca-239">更新裝置可能需要數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-239">Updating your device can take several hours.</span></span> <span data-ttu-id="bf7ca-240">如需有關如何 tooinstall hello 最新的更新詳細的步驟，請移過[安裝更新的 4](storsimple-8000-install-update-4.md)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-240">For detailed steps on how tooinstall hello latest update, go too[Install Update 4](storsimple-8000-install-update-4.md).</span></span>

## <a name="get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="bf7ca-241">取得 Windows Server 主機的 IQN hello</span><span class="sxs-lookup"><span data-stu-id="bf7ca-241">Get hello IQN of a Windows Server host</span></span>
<span data-ttu-id="bf7ca-242">執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server® 2012年的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-242">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="bf7ca-243">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="bf7ca-243">Create a manual backup</span></span>
<span data-ttu-id="bf7ca-244">執行 hello 遵循您的 StorSimple 裝置上 hello 政府入口 toocreate 隨需手動備份單一磁碟區中的步驟。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-244">Perform hello following steps in hello Government portal toocreate an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="bf7ca-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf7ca-245">Next steps</span></span>
* <span data-ttu-id="bf7ca-246">設定 [虛擬裝置](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-246">Configure a [virtual device](storsimple-8000-cloud-appliance-u2.md).</span></span>
* <span data-ttu-id="bf7ca-247">使用 hello [StorSimple 裝置管理員服務](storsimple-8000-manager-service-administration.md)toomanage StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="bf7ca-247">Use hello [StorSimple Device Manager service](storsimple-8000-manager-service-administration.md) toomanage your StorSimple device.</span></span>

