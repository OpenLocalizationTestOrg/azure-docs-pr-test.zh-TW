---
title: "如何設定雲端服務 (入口網站) | Microsoft Docs"
description: "了解如何在 Azure 中設定雲端服務。 了解更新雲端服務組態和設定角色執行個體的遠端存取。 這些範例使用 Azure 入口網站。"
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
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="45953-105">如何設定雲端服務</span><span class="sxs-lookup"><span data-stu-id="45953-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45953-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="45953-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="45953-107">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="45953-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="45953-108">您可以在 Azure 入口網站中設定雲端服務的最常用設定。</span><span class="sxs-lookup"><span data-stu-id="45953-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="45953-109">或者，如果您想要直接更新組態檔，可以下載要更新的服務組態檔、上傳更新過的檔案，然後將雲端服務更新為使用這些組態變更。</span><span class="sxs-lookup"><span data-stu-id="45953-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="45953-110">使用上述任一種方式，都會將組態更新推送到所有角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="45953-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="45953-111">您也可以管理雲端服務角色的執行個體，或從遠端桌面存取它們。</span><span class="sxs-lookup"><span data-stu-id="45953-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="45953-112">每個角色至少必須有兩個角色執行個體，Azure 才能確保服務在組態更新期間有 99.95% 的可用性。</span><span class="sxs-lookup"><span data-stu-id="45953-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="45953-113">如此才能讓一個虛擬機器在受到更新時，還有另一個虛擬機器可以處理用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="45953-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="45953-114">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="45953-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="45953-115">變更雲端服務</span><span class="sxs-lookup"><span data-stu-id="45953-115">Change a cloud service</span></span>
<span data-ttu-id="45953-116">開啟 [Azure 入口網站](https://portal.azure.com/)之後，瀏覽至您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="45953-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="45953-117">您可以從這裡管理許多層面。</span><span class="sxs-lookup"><span data-stu-id="45953-117">From here, you manage many aspects of it.</span></span>

![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="45953-119">[設定] 或 [所有設定] 連結可開啟 [設定] 刀鋒視窗，讓您變更 [屬性]、變更 [組態]、管理 [憑證]、設定 [警示規則]，以及管理可存取此雲端服務的 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="45953-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Azure 雲端服務設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="45953-121">管理客體作業系統版本</span><span class="sxs-lookup"><span data-stu-id="45953-121">Manage Guest OS version</span></span>

<span data-ttu-id="45953-122">根據預設，Azure 會將客體作業系統定期更新為您在服務組態 (.cscfg) 中指定的作業系統系列內最新支援的映像，例如 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="45953-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="45953-123">如果您需要針對特定的作業系統版本，可以在 [組態] 刀鋒視窗中設定。</span><span class="sxs-lookup"><span data-stu-id="45953-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![設定作業系統版本](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="45953-125">選擇特定的作業系統版本會停用作業系統自動更新，並使修補變成您的責任。</span><span class="sxs-lookup"><span data-stu-id="45953-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="45953-126">您必須確定您的角色執行個體將接收更新，否則您可能會會應用程式暴露在安全性弱點之下。</span><span class="sxs-lookup"><span data-stu-id="45953-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="45953-127">監視</span><span class="sxs-lookup"><span data-stu-id="45953-127">Monitoring</span></span>
<span data-ttu-id="45953-128">您可以將警示新增至雲端服務。</span><span class="sxs-lookup"><span data-stu-id="45953-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="45953-129">按一下 [設定] > [警示規則] > [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="45953-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="45953-130">您可以從這裡設定警示。</span><span class="sxs-lookup"><span data-stu-id="45953-130">From here, you can setup an alert.</span></span> <span data-ttu-id="45953-131">您可以使用 [計量] 下拉式方塊設定下列資料類型的警示。</span><span class="sxs-lookup"><span data-stu-id="45953-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="45953-132">磁碟讀取</span><span class="sxs-lookup"><span data-stu-id="45953-132">Disk read</span></span>
* <span data-ttu-id="45953-133">磁碟寫入</span><span class="sxs-lookup"><span data-stu-id="45953-133">Disk write</span></span>
* <span data-ttu-id="45953-134">網路輸入</span><span class="sxs-lookup"><span data-stu-id="45953-134">Network in</span></span>
* <span data-ttu-id="45953-135">網路輸出</span><span class="sxs-lookup"><span data-stu-id="45953-135">Network out</span></span>
* <span data-ttu-id="45953-136">CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="45953-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="45953-137">從計量圖格設定監視</span><span class="sxs-lookup"><span data-stu-id="45953-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="45953-138">除了使用 [設定] > [警示規則]，您也可以在 [雲端服務] 刀鋒視窗的 [監視] 區段中，按一下其中一個計量圖格。</span><span class="sxs-lookup"><span data-stu-id="45953-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![雲端服務監視](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="45953-140">您可以從這裡自訂與圖格一起使用的圖表，或新增警示規則。</span><span class="sxs-lookup"><span data-stu-id="45953-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="45953-141">重新啟動、重新安裝映像或遠端桌面</span><span class="sxs-lookup"><span data-stu-id="45953-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="45953-142">目前，您無法使用 **Azure 入口網站**來設定遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="45953-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="45953-143">不過，您可以透過 [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)、[PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) 或 [Visual Studio](../vs-azure-tools-remote-desktop-roles.md) 來設定它。</span><span class="sxs-lookup"><span data-stu-id="45953-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="45953-144">首先，請按一下雲端服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="45953-144">First, click on the cloud service instance.</span></span>

![雲端服務執行個體](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="45953-146">從開啟的刀鋒視窗中，您可以起始遠端桌面連線、從遠端重新啟動執行個體，或從遠端重新安裝執行個體的映像 (開始使用全新的映像)。</span><span class="sxs-lookup"><span data-stu-id="45953-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![雲端服務執行個體按鈕](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="45953-148">重新設定 .cscfg</span><span class="sxs-lookup"><span data-stu-id="45953-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="45953-149">您可能需要透過[服務組態 (cscfg)](cloud-services-model-and-package.md#cscfg) 檔案來重新設定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="45953-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="45953-150">首先，您需要下載 .cscfg 檔案，進行修改，然後上傳。</span><span class="sxs-lookup"><span data-stu-id="45953-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="45953-151">按一下 [設定] 圖示或 [所有設定] 連結，以開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="45953-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="45953-153">按一下 [ **組態** ] 項目。</span><span class="sxs-lookup"><span data-stu-id="45953-153">Click on the **Configuration** item.</span></span>

    ![設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="45953-155">按一下 [ **下載** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45953-155">Click on the **Download** button.</span></span>

    ![下載](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="45953-157">在您更新服務組態檔之後，請上傳和套用組態更新：</span><span class="sxs-lookup"><span data-stu-id="45953-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![上傳](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="45953-159">選取 .cscfg 檔案，然後按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="45953-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45953-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45953-160">Next steps</span></span>
* <span data-ttu-id="45953-161">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="45953-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="45953-162">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="45953-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="45953-163">[管理您的雲端服務](cloud-services-how-to-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="45953-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="45953-164">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="45953-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
