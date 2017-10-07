---
title: "aaaHow tooconfigure 雲端服務 （入口網站） |Microsoft 文件"
description: "了解 tooconfigure 雲端服務在 Azure 中的方式。 了解 tooupdate hello 雲端服務組態和設定遠端存取 toorole 執行個體。 這些範例使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="22e58-105">如何 tooConfigure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="22e58-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22e58-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="22e58-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="22e58-107">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="22e58-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="22e58-108">您可以在 hello Azure 入口網站中設定雲端服務的 hello 最常使用的設定。</span><span class="sxs-lookup"><span data-stu-id="22e58-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="22e58-109">或者，如果您喜歡 tooupdate 組態檔直接下載服務組態檔 tooupdate 」，然後上傳與 hello 組態變更的 hello 更新檔案和更新 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="22e58-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="22e58-110">無論如何，hello 組態更新推入 tooall 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="22e58-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="22e58-111">您也可以管理您的雲端服務角色或遠端桌面的它們的 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="22e58-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="22e58-112">Azure 才能確保服務 99.95%的可用性期間 hello 組態更新如果您有針對每個角色至少兩個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="22e58-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="22e58-113">可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。</span><span class="sxs-lookup"><span data-stu-id="22e58-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="22e58-114">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="22e58-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="22e58-115">變更雲端服務</span><span class="sxs-lookup"><span data-stu-id="22e58-115">Change a cloud service</span></span>
<span data-ttu-id="22e58-116">之後開啟 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 tooyour 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="22e58-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="22e58-117">您可以從這裡管理許多層面。</span><span class="sxs-lookup"><span data-stu-id="22e58-117">From here, you manage many aspects of it.</span></span>

![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="22e58-119">hello**設定**或**所有設定**連結會開啟 hello**設定**刀鋒視窗，您可以在其中變更 hello**屬性**，變更 hello**組態**，管理 hello**憑證**，安裝程式**警示規則**，及管理 hello**使用者**誰可以存取toothis 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="22e58-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Azure 雲端服務設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="22e58-121">管理客體作業系統版本</span><span class="sxs-lookup"><span data-stu-id="22e58-121">Manage Guest OS version</span></span>

<span data-ttu-id="22e58-122">根據預設，Azure 會定期更新客體作業系統 toohello 最新支援映像，在您的服務組態 (.cscfg) 中所指定的作業系統系列 hello 例如 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="22e58-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="22e58-123">如果您需要 tootarget 特定的作業系統版本，可以設定在 hello**組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="22e58-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![設定作業系統版本](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="22e58-125">選擇特定的作業系統版本會停用作業系統自動更新，並使修補變成您的責任。</span><span class="sxs-lookup"><span data-stu-id="22e58-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="22e58-126">您必須確定您的角色執行個體可接收更新，或您可能會公開您的應用程式 toosecurity 弱點。</span><span class="sxs-lookup"><span data-stu-id="22e58-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="22e58-127">監視</span><span class="sxs-lookup"><span data-stu-id="22e58-127">Monitoring</span></span>
<span data-ttu-id="22e58-128">您可以加入警示 tooyour 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="22e58-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="22e58-129">按一下 [設定] > [警示規則] > [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="22e58-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="22e58-130">您可以從這裡設定警示。</span><span class="sxs-lookup"><span data-stu-id="22e58-130">From here, you can setup an alert.</span></span> <span data-ttu-id="22e58-131">以 hello**度量**下拉式清單方塊中，您可以設定警示來 hello 下列類型的資料。</span><span class="sxs-lookup"><span data-stu-id="22e58-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="22e58-132">磁碟讀取</span><span class="sxs-lookup"><span data-stu-id="22e58-132">Disk read</span></span>
* <span data-ttu-id="22e58-133">磁碟寫入</span><span class="sxs-lookup"><span data-stu-id="22e58-133">Disk write</span></span>
* <span data-ttu-id="22e58-134">網路輸入</span><span class="sxs-lookup"><span data-stu-id="22e58-134">Network in</span></span>
* <span data-ttu-id="22e58-135">網路輸出</span><span class="sxs-lookup"><span data-stu-id="22e58-135">Network out</span></span>
* <span data-ttu-id="22e58-136">CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="22e58-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="22e58-137">從計量圖格設定監視</span><span class="sxs-lookup"><span data-stu-id="22e58-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="22e58-138">而不是使用**設定** > **警示規則**，您可以按一下其中一個 hello 度量磚中 hello**監視**區段 hello**雲端服務**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="22e58-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![雲端服務監視](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="22e58-140">從這裡您可以自訂 hello 圖表搭配 hello 磚，或加入警示規則。</span><span class="sxs-lookup"><span data-stu-id="22e58-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="22e58-141">重新啟動、重新安裝映像或遠端桌面</span><span class="sxs-lookup"><span data-stu-id="22e58-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="22e58-142">在這個階段中，您無法設定遠端桌面使用 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="22e58-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="22e58-143">不過，您可以設定它透過 hello [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)， [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)，或透過[Visual Studio](../vs-azure-tools-remote-desktop-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="22e58-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="22e58-144">首先，請按一下 hello 雲端服務執行個體上。</span><span class="sxs-lookup"><span data-stu-id="22e58-144">First, click on hello cloud service instance.</span></span>

![雲端服務執行個體](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="22e58-146">從 hello 刀鋒視窗，開啟時，您可以起始遠端桌面連線中，從遠端重新啟動 hello 執行個體，或從遠端重新安裝映像 （開始使用新的映像） hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="22e58-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![雲端服務執行個體按鈕](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="22e58-148">重新設定 .cscfg</span><span class="sxs-lookup"><span data-stu-id="22e58-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="22e58-149">您可能需要 tooreconfigure 您的雲端服務，透過 hello[服務組態 (cscfg)](cloud-services-model-and-package.md#cscfg)檔案。</span><span class="sxs-lookup"><span data-stu-id="22e58-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="22e58-150">首先，您必須 toodownload 您.cscfg 檔案，請修改它，然後將它上傳。</span><span class="sxs-lookup"><span data-stu-id="22e58-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="22e58-151">按一下 hello**設定**圖示或 hello**所有設定**連結向上 hello tooopen**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="22e58-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="22e58-153">按一下 hello**組態**項目。</span><span class="sxs-lookup"><span data-stu-id="22e58-153">Click on hello **Configuration** item.</span></span>

    ![設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="22e58-155">按一下 hello**下載** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e58-155">Click on hello **Download** button.</span></span>

    ![下載](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="22e58-157">更新 hello 服務組態檔之後，請上傳，並套用 hello 組態更新：</span><span class="sxs-lookup"><span data-stu-id="22e58-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![上傳](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="22e58-159">選取 hello.cscfg 檔案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22e58-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22e58-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22e58-160">Next steps</span></span>
* <span data-ttu-id="22e58-161">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22e58-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="22e58-162">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22e58-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="22e58-163">[管理您的雲端服務](cloud-services-how-to-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22e58-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="22e58-164">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22e58-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
