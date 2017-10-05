---
title: "在 Azure 雲端服務中啟用遠端桌面 | Microsoft Docs"
description: "如何設定的 Azure 雲端服務應用程式以允許遠端桌面連線"
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
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="3dc26-103">啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="3dc26-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3dc26-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3dc26-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="3dc26-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="3dc26-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="3dc26-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dc26-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="3dc26-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3dc26-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="3dc26-108">您可以在開發期間藉由在服務定義中包含遠端桌面模組啟用遠端桌面連線，也可以選擇透過遠端桌面延伸模組啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="3dc26-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="3dc26-109">慣用的方法是使用遠端桌面延伸模組，因為即使在部署應用程式之後，您仍然可以啟用遠端桌面，無需重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dc26-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="3dc26-110">從 Azure 傳統入口網站設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="3dc26-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="3dc26-111">Azure 傳統入口網站會使用遠端桌面延伸模組方法，因此即使在應用程式部署之後，您也可以啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="3dc26-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="3dc26-112">雲端服務的 [設定]  頁面可讓您啟用遠端桌面，變更用來與虛擬機器連線的本機系統管理員帳戶、驗證中使用的憑證，並設定到期日。</span><span class="sxs-lookup"><span data-stu-id="3dc26-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="3dc26-113">依序按一下 [雲端服務]、雲端服務的名稱及 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3dc26-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="3dc26-114">按一下底部的 [遠端] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dc26-114">Click the **Remote** button at the bottom.</span></span>

    ![Cloud services remote](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="3dc26-116">當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3dc26-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="3dc26-117">若要防止重新啟動，角色上必須安裝用來將密碼加密的憑證。</span><span class="sxs-lookup"><span data-stu-id="3dc26-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="3dc26-118">若要防止重新啟動，請[上傳雲端服務的憑證](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後再回到這個對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3dc26-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="3dc26-119">在 [角色] 中，選取想要更新的角色，或選取 [全部] 以更新所有角色。</span><span class="sxs-lookup"><span data-stu-id="3dc26-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="3dc26-120">進行下列任一變更：</span><span class="sxs-lookup"><span data-stu-id="3dc26-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="3dc26-121">若要啟用遠端桌面，請選取 [啟用遠端桌面]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3dc26-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="3dc26-122">若要停用遠端桌面，請清除此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3dc26-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="3dc26-123">建立用來對角色執行個體進行遠端桌面連線的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3dc26-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="3dc26-124">更新現有帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="3dc26-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="3dc26-125">選取要用於驗證的已上傳憑證 (使用 [憑證] 頁面上的 [上傳] 來上傳憑證)，或建立新的憑證。</span><span class="sxs-lookup"><span data-stu-id="3dc26-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="3dc26-126">變更遠端桌面組態的到期日。</span><span class="sxs-lookup"><span data-stu-id="3dc26-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="3dc26-127">完成組態更新時，按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="3dc26-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="3dc26-128">角色執行個體的遠端存取</span><span class="sxs-lookup"><span data-stu-id="3dc26-128">Remote into role instances</span></span>
<span data-ttu-id="3dc26-129">一旦在角色上啟用遠端桌面，您可以透過各種工具遠端存取角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3dc26-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="3dc26-130">若要從 Azure 傳統入口網站連線到角色執行個體：</span><span class="sxs-lookup"><span data-stu-id="3dc26-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="3dc26-131">按一下 [執行個體] 以開啟 [執行個體] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3dc26-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="3dc26-132">選取已設定「遠端桌面」的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3dc26-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="3dc26-133">按一下 [ **連接**]，然後依照指示開啟桌面。</span><span class="sxs-lookup"><span data-stu-id="3dc26-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="3dc26-134">按一下 [開啟]，然後按一下 [連接] 以啟動遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="3dc26-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="3dc26-135">使用 Visual Studio 遠端存取角色執行個體</span><span class="sxs-lookup"><span data-stu-id="3dc26-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="3dc26-136">在 Visual Studio 中，伺服器總管：</span><span class="sxs-lookup"><span data-stu-id="3dc26-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="3dc26-137">展開 **Azure** > 雲端服務] > 「雲端服務名稱」節點。</span><span class="sxs-lookup"><span data-stu-id="3dc26-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="3dc26-138">展開 [預備]或 [生產]。</span><span class="sxs-lookup"><span data-stu-id="3dc26-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="3dc26-139">展開個別角色。</span><span class="sxs-lookup"><span data-stu-id="3dc26-139">Expand the individual role.</span></span>
4. <span data-ttu-id="3dc26-140">以滑鼠右鍵按一下其中一個角色執行個體，按一下 [使用遠端桌面連線...] ，然後輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="3dc26-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![伺服器總管遠端桌面](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="3dc26-142">使用 PowerShell 取得 RDP 檔案</span><span class="sxs-lookup"><span data-stu-id="3dc26-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="3dc26-143">您可以使用 [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet 擷取 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="3dc26-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="3dc26-144">然後，您可以使用 RDP 檔案及遠端桌面連線存取雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3dc26-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="3dc26-145">以程式設計的方式透過服務管理 REST API 下載 RDP 檔案</span><span class="sxs-lookup"><span data-stu-id="3dc26-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="3dc26-146">您可以使用 [下載 RDP 檔案](https://msdn.microsoft.com/library/jj157183.aspx) REST 作業下載 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="3dc26-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="3dc26-147">在服務定義檔中設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="3dc26-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="3dc26-148">這個方法可讓您在開發期間啟用應用程式的遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="3dc26-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="3dc26-149">此方法需要加密的密碼儲存在您的服務組態檔中，且遠端桌面組態的任何更新都需要重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dc26-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="3dc26-150">如果您想要避免這些缺點，您應該使用以上所述之以遠端桌面延伸模組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="3dc26-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="3dc26-151">您可以使用 Visual Studio [啟用遠端桌面連線](../vs-azure-tools-remote-desktop-roles.md) 以使用服務定義檔方法。</span><span class="sxs-lookup"><span data-stu-id="3dc26-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="3dc26-152">下列步驟說明服務模型檔案啟用遠端桌面所需的變更。</span><span class="sxs-lookup"><span data-stu-id="3dc26-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="3dc26-153">Visual Studio 將會在發佈時自動產生這些變更。</span><span class="sxs-lookup"><span data-stu-id="3dc26-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="3dc26-154">設定服務模型中的連線</span><span class="sxs-lookup"><span data-stu-id="3dc26-154">Set up the connection in the service model</span></span>
<span data-ttu-id="3dc26-155">使用 **Imports** 元素將 **RemoteAccess** 模組和 **RemoteForwarder** 模組匯入至 [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) 檔案。</span><span class="sxs-lookup"><span data-stu-id="3dc26-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="3dc26-156">服務定義檔應類似下列已加入 `<Imports>` 元素的範例。</span><span class="sxs-lookup"><span data-stu-id="3dc26-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

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
<span data-ttu-id="3dc26-157">[ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) 檔案應類似下列範例，請注意 `<ConfigurationSettings>` 和 `<Certificates>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3dc26-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="3dc26-158">指定的憑證必須已[上傳至雲端服務](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="3dc26-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="3dc26-159">其他資源</span><span class="sxs-lookup"><span data-stu-id="3dc26-159">Additional Resources</span></span>
<span data-ttu-id="3dc26-160">[如何設定雲端服務](cloud-services-how-to-configure.md)
[雲端服務常見問題集 - 遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3dc26-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
