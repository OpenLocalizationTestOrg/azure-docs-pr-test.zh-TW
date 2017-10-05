---
title: "如何設定雲端服務 (傳統入口網站) | Microsoft Docs"
description: "了解如何在 Azure 中設定雲端服務。 了解更新雲端服務組態和設定角色執行個體的遠端存取。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 39bb294c96ce0c12d91cf8b3488ac3e1a7b2f7b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="31959-104">如何設定雲端服務</span><span class="sxs-lookup"><span data-stu-id="31959-104">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31959-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31959-105">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="31959-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="31959-106">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
> 
> 

<span data-ttu-id="31959-107">您可以在 Azure 傳統入口網站中設定雲端服務的最常用設定。</span><span class="sxs-lookup"><span data-stu-id="31959-107">You can configure the most commonly used settings for a cloud service in the Azure classic portal.</span></span> <span data-ttu-id="31959-108">或者，如果您想要直接更新組態檔，可以下載要更新的服務組態檔、上傳更新過的檔案，然後將雲端服務更新為使用這些組態變更。</span><span class="sxs-lookup"><span data-stu-id="31959-108">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="31959-109">使用上述任一種方式，都會將組態更新推送到所有角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="31959-109">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="31959-110">Azure 傳統入口網站也可讓您 [啟用 Azure 雲端服務中角色的遠端桌面連線](cloud-services-role-enable-remote-desktop.md)</span><span class="sxs-lookup"><span data-stu-id="31959-110">The Azure classic portal also allows you to [enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span></span>

<span data-ttu-id="31959-111">每個角色至少必須有兩個角色執行個體，Azure 才能確保服務在組態更新期間有 99.95% 的可用性。</span><span class="sxs-lookup"><span data-stu-id="31959-111">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="31959-112">如此才能讓一個虛擬機器在受到更新時，還有另一個虛擬機器可以處理用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="31959-112">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="31959-113">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="31959-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="31959-114">變更雲端服務</span><span class="sxs-lookup"><span data-stu-id="31959-114">Change a cloud service</span></span>
1. <span data-ttu-id="31959-115">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，依序按一下 [雲端服務]、雲端服務的名稱及 [設定]。</span><span class="sxs-lookup"><span data-stu-id="31959-115">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
   
    ![Configuration Page](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    <span data-ttu-id="31959-117">在 [設定]  頁面上，您可以設定監視、更新角色設定，以及選擇角色執行個體的客體作業系統和系列。</span><span class="sxs-lookup"><span data-stu-id="31959-117">On the **Configure** page, you can configure monitoring, update role settings, and choose the guest operating system and family for role instances.</span></span> 
2. <span data-ttu-id="31959-118">在 [監視] 中，將監視層級設定為 [詳細資訊] 或 [最小]，並設定進行詳細資訊監視時所需的診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="31959-118">In **monitoring**, set the monitoring level to Verbose or Minimal, and configure the diagnostics connection strings that are required for verbose monitoring.</span></span>
3. <span data-ttu-id="31959-119">針對服務角色 (依角色分組)，您可以更新下列設定：</span><span class="sxs-lookup"><span data-stu-id="31959-119">For service roles (grouped by role), you can update the following settings:</span></span>
   
    * <span data-ttu-id="31959-120">**設定** 修改服務組態檔 (.cscfg) 之 *ConfigurationSettings* 元素中所指定的其他組態設定值。</span><span class="sxs-lookup"><span data-stu-id="31959-120">**Settings** Modify the values of miscellaneous configuration settings that are specified in the *ConfigurationSettings* elements of the service configuration (.cscfg) file.</span></span>

    * <span data-ttu-id="31959-121">**憑證**</span><span class="sxs-lookup"><span data-stu-id="31959-121">**Certificates**</span></span>  
        <span data-ttu-id="31959-122">變更要在角色之 SSL 加密中使用的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="31959-122">Change the certificate thumbprint that's being used in SSL encryption for a role.</span></span> <span data-ttu-id="31959-123">若要變更憑證，您必須先上傳新的憑證 (在 [憑證]  頁面上)。</span><span class="sxs-lookup"><span data-stu-id="31959-123">To change a certificate, you must first upload the new certificate (on the **Certificates** page).</span></span> <span data-ttu-id="31959-124">然後，更新角色設定中所顯示憑證字串中的指紋。</span><span class="sxs-lookup"><span data-stu-id="31959-124">Then update the thumbprint in the certificate string displayed in the role settings.</span></span>
4. <span data-ttu-id="31959-125">在 [作業系統] 中，您可以變更角色執行個體的作業系統系列或版本，或選擇 [自動] 以啟用自動更新目前的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="31959-125">In **operating system**, you can change the operating system family or version for role instances, or choose **Automatic** to enable automatic updates of the current operating system version.</span></span> <span data-ttu-id="31959-126">作業系統設定會套用於 Web 角色和背景工作角色，但不影響虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="31959-126">The operating system settings apply to web roles and worker roles, but do not affect Virtual Machines.</span></span>
   
    <span data-ttu-id="31959-127">部署期間會在所有角色執行個體上安裝最新作業系統版本，而且預設會自動更新作業系統。</span><span class="sxs-lookup"><span data-stu-id="31959-127">During deployment, the most recent operating system version is installed on all role instances, and the operating systems are updated automatically by default.</span></span> 
   
    <span data-ttu-id="31959-128">如果您因為程式碼中的相容性需求而需要在不同的作業系統版本上執行雲端服務，則可以選擇作業系統系列和版本。</span><span class="sxs-lookup"><span data-stu-id="31959-128">If you need for your cloud service to run on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span></span> <span data-ttu-id="31959-129">當您選擇特定作業系統版本時，雲端服務的自動作業系統更新會暫停。</span><span class="sxs-lookup"><span data-stu-id="31959-129">When you choose a specific operating system version, automatic operating system updates for the cloud service are suspended.</span></span> <span data-ttu-id="31959-130">您需要確保作業系統收到更新。</span><span class="sxs-lookup"><span data-stu-id="31959-130">You will need to ensure the operating systems receive updates.</span></span>
   
    <span data-ttu-id="31959-131">如果您解決了應用程式對最新作業系統版本的所有相容性問題，則可以將作業系統版本設定為 [自動] ，以啟用自動更新作業系統。</span><span class="sxs-lookup"><span data-stu-id="31959-131">If you resolve all compatibility issues that your apps have with the most recent operating system version, you can enable automatic operating system updates by setting the operating system version to **Automatic**.</span></span> 
   
    ![OS Settings](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. <span data-ttu-id="31959-133">若要儲存組態設定，並將之推送到角色執行個體中，請按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="31959-133">To save your configuration settings, and push them to the role instances, click **Save**.</span></span> <span data-ttu-id="31959-134">(按一下 [捨棄] 可取消變更。)在您變更設定之後，命令列中即會新增 [儲存] 和 [捨棄]。</span><span class="sxs-lookup"><span data-stu-id="31959-134">(Click **Discard** to cancel the changes.) **Save** and **Discard** are added to the command bar after you change a setting.</span></span>

## <a name="update-a-cloud-service-configuration-file"></a><span data-ttu-id="31959-135">更新雲端服務組態檔</span><span class="sxs-lookup"><span data-stu-id="31959-135">Update a cloud service configuration file</span></span>
1. <span data-ttu-id="31959-136">下載含有最新組態的雲端服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="31959-136">Download a cloud service configuration file (.cscfg) with the current configuration.</span></span> <span data-ttu-id="31959-137">在雲端服務的 [設定] 頁面上，按 [下載]。</span><span class="sxs-lookup"><span data-stu-id="31959-137">On the **Configure** page for the cloud service, click **Download**.</span></span> <span data-ttu-id="31959-138">然後按一下 [儲存]，或按一下 [另存新檔] 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="31959-138">Then click **Save**, or click **Save As** to save the file.</span></span>
2. <span data-ttu-id="31959-139">在您更新服務組態檔之後，請上傳和套用組態更新：</span><span class="sxs-lookup"><span data-stu-id="31959-139">After you update the service configuration file, upload and apply the configuration updates:</span></span>
   
   1. <span data-ttu-id="31959-140">在 [設定] 頁面上，按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="31959-140">On the **Configure** page, click **Upload**.</span></span>
      
       ![Upload Configuration](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. <span data-ttu-id="31959-142">在 [組態檔] 中，使用 [瀏覽] 來選取已更新的.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="31959-142">In **Configuration file**, use **Browse** to select the updated .cscfg file.</span></span>
   3. <span data-ttu-id="31959-143">如果您的雲端服務包含任何只有一個執行個體的角色，請選取 [ **套用組態，即使有一或多個角色包含單一執行個體** ] 核取方塊，讓角色的組態更新能夠繼續。</span><span class="sxs-lookup"><span data-stu-id="31959-143">If your cloud service contains any roles that have only one instance, select the **Apply configuration even if one or more roles contain a single instance** check box to enable the configuration updates for the roles to proceed.</span></span>
      
       <span data-ttu-id="31959-144">除非每個角色都定義至少兩個執行個體，否則 Azure 無法保證雲端服務在服務組態更新期間至少有 99.95% 的可用性。</span><span class="sxs-lookup"><span data-stu-id="31959-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span></span> <span data-ttu-id="31959-145">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="31959-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
   4. <span data-ttu-id="31959-146">按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="31959-146">Click **OK** (checkmark).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31959-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31959-147">Next steps</span></span>
* <span data-ttu-id="31959-148">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="31959-148">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="31959-149">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="31959-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="31959-150">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="31959-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* [<span data-ttu-id="31959-151">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="31959-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>](cloud-services-role-enable-remote-desktop.md)
* <span data-ttu-id="31959-152">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="31959-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

