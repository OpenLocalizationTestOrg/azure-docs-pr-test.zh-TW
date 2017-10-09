---
title: "在 Azure 雲端服務中的遠端桌面 aaaEnable |Microsoft 文件"
description: "如何 tooconfigure 您的 azure 雲端服務應用程式 tooallow 遠端桌面連線"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="aa3fe-103">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="aa3fe-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa3fe-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aa3fe-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="aa3fe-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="aa3fe-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="aa3fe-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa3fe-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="aa3fe-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa3fe-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="aa3fe-108">您可以啟用遠端桌面連線您的角色在開發期間包含在服務定義中的 hello 遠端桌面模組，或者您可以選擇透過遠端桌面延伸模組 hello tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="aa3fe-109">hello 慣用的方法為 toouse hello 遠端桌面延伸您可以在 hello 應用程式部署而不需要 tooredeploy 您的應用程式時，即使啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="aa3fe-110">從 hello Azure 傳統入口網站中設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="aa3fe-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="aa3fe-111">hello Azure 傳統入口網站會使用 hello 遠端桌面的擴充方法，因此即使在 hello 應用程式部署之後，您可以啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="aa3fe-112">hello**設定**為雲端服務 頁面可讓您 tooenable 遠端桌面變更 hello 本機系統管理員帳戶使用 tooconnect toohello 虛擬機器、 hello 憑證用於驗證和設定 hello到期日。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="aa3fe-113">按一下**雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="aa3fe-114">按一下 hello**遠端**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Cloud services remote](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="aa3fe-116">當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="aa3fe-117">tooprevent hello 憑證使用的 tooencrypt hello 密碼重新開機，必須安裝在 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="aa3fe-118">重新啟動，tooprevent [hello 雲端服務將憑證上傳](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後傳回 toothis 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="aa3fe-119">在**角色**，選取您想要 tooupdate 或選取 hello 角色**所有**所有角色。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="aa3fe-120">進行任何 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="aa3fe-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="aa3fe-121">遠端桌面，選取 hello tooenable**啟用遠端桌面**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="aa3fe-122">toodisable 遠端桌面，清除 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="aa3fe-123">建立帳戶 toouse 中遠端桌面連線 toohello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="aa3fe-124">更新 hello hello 現有帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="aa3fe-125">選取的上傳的憑證 toouse 進行驗證 (使用憑證上傳 hello**上傳**上 hello**憑證**頁面) 或建立新的憑證。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="aa3fe-126">變更 hello hello 遠端桌面設定的到期日。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="aa3fe-127">完成組態更新時，按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="aa3fe-128">角色執行個體的遠端存取</span><span class="sxs-lookup"><span data-stu-id="aa3fe-128">Remote into role instances</span></span>
<span data-ttu-id="aa3fe-129">Hello 角色上啟用遠端桌面之後您可以從遠端存取角色執行個體，透過各種工具。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="aa3fe-130">tooconnect tooa 角色執行個體從 hello Azure 傳統入口網站：</span><span class="sxs-lookup"><span data-stu-id="aa3fe-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="aa3fe-131">按一下**執行個體**tooopen hello**執行個體**頁面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="aa3fe-132">選取已設定「遠端桌面」的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="aa3fe-133">按一下**連接**，並遵循 hello 指示 tooopen hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="aa3fe-134">按一下**開啟**然後**連接**toostart hello 遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="aa3fe-135">使用 Visual Studio tooremote 中將角色執行個體</span><span class="sxs-lookup"><span data-stu-id="aa3fe-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="aa3fe-136">在 Visual Studio 中，伺服器總管：</span><span class="sxs-lookup"><span data-stu-id="aa3fe-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="aa3fe-137">展開 hello **Azure** > **雲端服務** > **[雲端服務名稱]**節點。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="aa3fe-138">展開 [預備]或 [生產]。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="aa3fe-139">展開 hello 個別的角色。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="aa3fe-140">以滑鼠右鍵按一下其中一個 hello 角色執行個體中，按一下**使用遠端桌面連線...**，然後輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![伺服器總管遠端桌面](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="aa3fe-142">使用 PowerShell tooget hello RDP 檔案</span><span class="sxs-lookup"><span data-stu-id="aa3fe-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="aa3fe-143">您可以使用 hello [Get-azureremotedesktopfile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="aa3fe-144">您接著可以使用 hello RDP 檔案與遠端桌面連線 tooaccess hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="aa3fe-145">以程式設計方式下載透過 hello 服務管理 REST API 的 hello RDP 檔案</span><span class="sxs-lookup"><span data-stu-id="aa3fe-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="aa3fe-146">您可以使用 hello[下載 RDP 檔案](https://msdn.microsoft.com/library/jj157183.aspx)REST 作業 toodownload hello RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="aa3fe-147">tooconfigure hello 服務定義檔中的遠端桌面</span><span class="sxs-lookup"><span data-stu-id="aa3fe-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="aa3fe-148">這個方法可讓您在開發期間的 hello 應用程式的 tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="aa3fe-149">這個方法會要求加密的密碼儲存在您的服務組態檔案及任何更新 toohello 遠端桌面設定需要重新部署的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="aa3fe-150">如果您想 tooavoid 這些缺點在於，您應該使用 hello 遠端桌面延伸模組為基礎的上面所述的方法。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="aa3fe-151">您也可以使用 Visual Studio[啟用遠端桌面連線](../vs-azure-tools-remote-desktop-roles.md)使用 hello 服務定義檔的方法。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="aa3fe-152">下列的 hello 步驟說明 hello 變更所需的 toohello 服務模型檔案 tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="aa3fe-153">Visual Studio 將會在發佈時自動產生這些變更。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="aa3fe-154">設定 hello 服務模型中的 hello 連線</span><span class="sxs-lookup"><span data-stu-id="aa3fe-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="aa3fe-155">使用 hello**匯入**元素 tooimport hello **RemoteAccess**模組和 hello **RemoteForwarder**模組 toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef)檔案。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="aa3fe-156">hello 服務定義檔應類似下列範例與 hello 的 toohello`<Imports>`加入項目。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="aa3fe-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg)檔案應該會類似下列範例的 toohello，記下 hello`<ConfigurationSettings>`和`<Certificates>`項目。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="aa3fe-158">必須指定憑證 hello [toohello 雲端服務上傳](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="aa3fe-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="aa3fe-159">其他資源</span><span class="sxs-lookup"><span data-stu-id="aa3fe-159">Additional Resources</span></span>
<span data-ttu-id="aa3fe-160">[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="aa3fe-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
