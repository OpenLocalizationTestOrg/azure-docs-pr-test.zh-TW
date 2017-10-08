---
title: "aaaHow tooconfigure 雲端服務 （傳統入口網站） |Microsoft 文件"
description: "了解 tooconfigure 雲端服務在 Azure 中的方式。 了解 tooupdate hello 雲端服務組態和設定遠端存取 toorole 執行個體。"
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
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="abd4a-104">如何 tooConfigure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="abd4a-104">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abd4a-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="abd4a-105">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="abd4a-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="abd4a-106">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
> 
> 

<span data-ttu-id="abd4a-107">您可以在 hello Azure 傳統入口網站中設定雲端服務的 hello 最常使用的設定。</span><span class="sxs-lookup"><span data-stu-id="abd4a-107">You can configure hello most commonly used settings for a cloud service in hello Azure classic portal.</span></span> <span data-ttu-id="abd4a-108">或者，如果您喜歡 tooupdate 組態檔直接下載服務組態檔 tooupdate 」，然後上傳與 hello 組態變更的 hello 更新檔案和更新 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="abd4a-108">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="abd4a-109">無論如何，hello 組態更新推入 tooall 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="abd4a-109">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="abd4a-110">hello Azure 傳統入口網站也可讓您太[Azure 雲端服務中的角色啟用遠端桌面連線](cloud-services-role-enable-remote-desktop.md)</span><span class="sxs-lookup"><span data-stu-id="abd4a-110">hello Azure classic portal also allows you too[enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span></span>

<span data-ttu-id="abd4a-111">Azure 才能確保服務 99.95%的可用性期間 hello 組態更新如果您有針對每個角色至少兩個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="abd4a-111">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="abd4a-112">可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。</span><span class="sxs-lookup"><span data-stu-id="abd4a-112">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="abd4a-113">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="abd4a-114">變更雲端服務</span><span class="sxs-lookup"><span data-stu-id="abd4a-114">Change a cloud service</span></span>
1. <span data-ttu-id="abd4a-115">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="abd4a-115">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
   
    ![Configuration Page](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    <span data-ttu-id="abd4a-117">在 [hello**設定**] 頁面上，您可以設定監視之後，更新角色設定，並選擇 hello 客體作業系統和角色執行個體的系列。</span><span class="sxs-lookup"><span data-stu-id="abd4a-117">On hello **Configure** page, you can configure monitoring, update role settings, and choose hello guest operating system and family for role instances.</span></span> 
2. <span data-ttu-id="abd4a-118">在**監視**，監視層級 tooVerbose 組 hello 或最小，並設定所需的詳細資訊監視 hello 診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="abd4a-118">In **monitoring**, set hello monitoring level tooVerbose or Minimal, and configure hello diagnostics connection strings that are required for verbose monitoring.</span></span>
3. <span data-ttu-id="abd4a-119">對於服務角色 （根據角色分組），您可以更新 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="abd4a-119">For service roles (grouped by role), you can update hello following settings:</span></span>
   
    * <span data-ttu-id="abd4a-120">**設定**修改 hello 中所指定的其他組態設定的 hello 值*ConfigurationSettings* hello 服務組態 (.cscfg) 檔的項目。</span><span class="sxs-lookup"><span data-stu-id="abd4a-120">**Settings** Modify hello values of miscellaneous configuration settings that are specified in hello *ConfigurationSettings* elements of hello service configuration (.cscfg) file.</span></span>

    * <span data-ttu-id="abd4a-121">**憑證**</span><span class="sxs-lookup"><span data-stu-id="abd4a-121">**Certificates**</span></span>  
        <span data-ttu-id="abd4a-122">變更用於 SSL 加密為角色的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="abd4a-122">Change hello certificate thumbprint that's being used in SSL encryption for a role.</span></span> <span data-ttu-id="abd4a-123">toochange 憑證，您必須先上傳 hello 新憑證 (在 hello**憑證**頁面)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-123">toochange a certificate, you must first upload hello new certificate (on hello **Certificates** page).</span></span> <span data-ttu-id="abd4a-124">接著，更新顯示 hello 角色設定中的 hello 憑證字串中的 hello 指紋。</span><span class="sxs-lookup"><span data-stu-id="abd4a-124">Then update hello thumbprint in hello certificate string displayed in hello role settings.</span></span>
4. <span data-ttu-id="abd4a-125">在**作業系統**，您可以變更 hello 作業系統系列或版本，角色執行個體，或選擇**自動**tooenable 的 hello 目前作業系統版本的自動更新。</span><span class="sxs-lookup"><span data-stu-id="abd4a-125">In **operating system**, you can change hello operating system family or version for role instances, or choose **Automatic** tooenable automatic updates of hello current operating system version.</span></span> <span data-ttu-id="abd4a-126">hello 作業系統設定套用 tooweb 角色和背景工作角色，但不是會影響虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="abd4a-126">hello operating system settings apply tooweb roles and worker roles, but do not affect Virtual Machines.</span></span>
   
    <span data-ttu-id="abd4a-127">在部署期間，hello 最新的作業系統版本安裝在所有角色執行個體，而且 hello 作業系統預設會自動更新。</span><span class="sxs-lookup"><span data-stu-id="abd4a-127">During deployment, hello most recent operating system version is installed on all role instances, and hello operating systems are updated automatically by default.</span></span> 
   
    <span data-ttu-id="abd4a-128">如果您需要針對您在不同的作業系統版本上的雲端服務 toorun 因為相容性需求，所以您的程式碼中，您可以選擇的作業系統系列和版本。</span><span class="sxs-lookup"><span data-stu-id="abd4a-128">If you need for your cloud service toorun on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span></span> <span data-ttu-id="abd4a-129">當您選擇使用特定作業系統版本時，就會暫停作業系統自動更新為 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="abd4a-129">When you choose a specific operating system version, automatic operating system updates for hello cloud service are suspended.</span></span> <span data-ttu-id="abd4a-130">您將需要 tooensure hello 作業系統接收更新。</span><span class="sxs-lookup"><span data-stu-id="abd4a-130">You will need tooensure hello operating systems receive updates.</span></span>
   
    <span data-ttu-id="abd4a-131">如果您解決所有應用程式具有 hello 最新的作業系統版本的相容性問題，您可以啟用作業系統自動更新設定 hello 作業系統版本太**自動**。</span><span class="sxs-lookup"><span data-stu-id="abd4a-131">If you resolve all compatibility issues that your apps have with hello most recent operating system version, you can enable automatic operating system updates by setting hello operating system version too**Automatic**.</span></span> 
   
    ![OS Settings](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. <span data-ttu-id="abd4a-133">toosave 您的組態設定，並將其推送 toohello 角色執行個體，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="abd4a-133">toosave your configuration settings, and push them toohello role instances, click **Save**.</span></span> <span data-ttu-id="abd4a-134">(按一下**捨棄**toocancel hello 變更。)**儲存**和**捨棄**變更設定之後才加入 toohello 命令列。</span><span class="sxs-lookup"><span data-stu-id="abd4a-134">(Click **Discard** toocancel hello changes.) **Save** and **Discard** are added toohello command bar after you change a setting.</span></span>

## <a name="update-a-cloud-service-configuration-file"></a><span data-ttu-id="abd4a-135">更新雲端服務組態檔</span><span class="sxs-lookup"><span data-stu-id="abd4a-135">Update a cloud service configuration file</span></span>
1. <span data-ttu-id="abd4a-136">下載雲端服務組態檔 (.cscfg) hello 目前的組態。</span><span class="sxs-lookup"><span data-stu-id="abd4a-136">Download a cloud service configuration file (.cscfg) with hello current configuration.</span></span> <span data-ttu-id="abd4a-137">在 hello**設定**hello 雲端服務頁面上，按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="abd4a-137">On hello **Configure** page for hello cloud service, click **Download**.</span></span> <span data-ttu-id="abd4a-138">然後按一下 **儲存**，或按一下**存**toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="abd4a-138">Then click **Save**, or click **Save As** toosave hello file.</span></span>
2. <span data-ttu-id="abd4a-139">更新 hello 服務組態檔之後，請上傳，並套用 hello 組態更新：</span><span class="sxs-lookup"><span data-stu-id="abd4a-139">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>
   
   1. <span data-ttu-id="abd4a-140">在 hello**設定**頁面上，按一下**上傳**。</span><span class="sxs-lookup"><span data-stu-id="abd4a-140">On hello **Configure** page, click **Upload**.</span></span>
      
       ![Upload Configuration](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. <span data-ttu-id="abd4a-142">在**組態檔**，使用**瀏覽**tooselect hello 更新.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="abd4a-142">In **Configuration file**, use **Browse** tooselect hello updated .cscfg file.</span></span>
   3. <span data-ttu-id="abd4a-143">如果您的雲端服務包含只有一個執行個體的任何角色，選取 hello**套用設定，即使一個或多個角色包含單一執行個體**核取方塊的 hello 角色 tooproceed tooenable hello 組態更新。</span><span class="sxs-lookup"><span data-stu-id="abd4a-143">If your cloud service contains any roles that have only one instance, select hello **Apply configuration even if one or more roles contain a single instance** check box tooenable hello configuration updates for hello roles tooproceed.</span></span>
      
       <span data-ttu-id="abd4a-144">除非每個角色都定義至少兩個執行個體，否則 Azure 無法保證雲端服務在服務組態更新期間至少有 99.95% 的可用性。</span><span class="sxs-lookup"><span data-stu-id="abd4a-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span></span> <span data-ttu-id="abd4a-145">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
   4. <span data-ttu-id="abd4a-146">按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-146">Click **OK** (checkmark).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="abd4a-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abd4a-147">Next steps</span></span>
* <span data-ttu-id="abd4a-148">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-148">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="abd4a-149">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="abd4a-150">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* [<span data-ttu-id="abd4a-151">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="abd4a-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>](cloud-services-role-enable-remote-desktop.md)
* <span data-ttu-id="abd4a-152">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="abd4a-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

