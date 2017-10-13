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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>啟用 Azure 雲端服務中角色的遠端桌面連線

> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

您可以在開發期間藉由在服務定義中包含遠端桌面模組啟用遠端桌面連線，也可以選擇透過遠端桌面延伸模組啟用遠端桌面。 慣用的方法是使用遠端桌面延伸模組，因為即使在部署應用程式之後，您仍然可以啟用遠端桌面，無需重新部署您的應用程式。

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a>從 Azure 傳統入口網站設定遠端桌面
Azure 傳統入口網站會使用遠端桌面延伸模組方法，因此即使在應用程式部署之後，您也可以啟用遠端桌面。 雲端服務的 [設定]  頁面可讓您啟用遠端桌面，變更用來與虛擬機器連線的本機系統管理員帳戶、驗證中使用的憑證，並設定到期日。

1. 依序按一下 [雲端服務]、雲端服務的名稱及 [設定]。
2. 按一下底部的 [遠端] 按鈕。

    ![Cloud services remote](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > 當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。 若要防止重新啟動，角色上必須安裝用來將密碼加密的憑證。 若要防止重新啟動，請[上傳雲端服務的憑證](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後再回到這個對話方塊。

3. 在 [角色] 中，選取想要更新的角色，或選取 [全部] 以更新所有角色。
4. 進行下列任一變更：

   * 若要啟用遠端桌面，請選取 [啟用遠端桌面]  核取方塊。 若要停用遠端桌面，請清除此核取方塊。
   * 建立用來對角色執行個體進行遠端桌面連線的帳戶。
   * 更新現有帳戶的密碼。
   * 選取要用於驗證的已上傳憑證 (使用 [憑證] 頁面上的 [上傳] 來上傳憑證)，或建立新的憑證。
   * 變更遠端桌面組態的到期日。

5. 完成組態更新時，按一下 [確定]  \(勾選記號)。

## <a name="remote-into-role-instances"></a>角色執行個體的遠端存取
一旦在角色上啟用遠端桌面，您可以透過各種工具遠端存取角色執行個體。

若要從 Azure 傳統入口網站連線到角色執行個體：

1. 按一下 [執行個體] 以開啟 [執行個體] 頁面。
2. 選取已設定「遠端桌面」的角色執行個體。
3. 按一下 [ **連接**]，然後依照指示開啟桌面。
4. 按一下 [開啟]，然後按一下 [連接] 以啟動遠端桌面連線。

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a>使用 Visual Studio 遠端存取角色執行個體
在 Visual Studio 中，伺服器總管：

1. 展開 **Azure** > 雲端服務] > 「雲端服務名稱」節點。
2. 展開 [預備]或 [生產]。
3. 展開個別角色。
4. 以滑鼠右鍵按一下其中一個角色執行個體，按一下 [使用遠端桌面連線...] ，然後輸入使用者名稱和密碼。

![伺服器總管遠端桌面](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a>使用 PowerShell 取得 RDP 檔案
您可以使用 [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet 擷取 RDP 檔案。 然後，您可以使用 RDP 檔案及遠端桌面連線存取雲端服務。

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a>以程式設計的方式透過服務管理 REST API 下載 RDP 檔案
您可以使用 [下載 RDP 檔案](https://msdn.microsoft.com/library/jj157183.aspx) REST 作業下載 RDP 檔案。

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a>在服務定義檔中設定遠端桌面
這個方法可讓您在開發期間啟用應用程式的遠端桌面。 此方法需要加密的密碼儲存在您的服務組態檔中，且遠端桌面組態的任何更新都需要重新部署應用程式。 如果您想要避免這些缺點，您應該使用以上所述之以遠端桌面延伸模組為基礎的方法。  

您可以使用 Visual Studio [啟用遠端桌面連線](../vs-azure-tools-remote-desktop-roles.md) 以使用服務定義檔方法。  
下列步驟說明服務模型檔案啟用遠端桌面所需的變更。 Visual Studio 將會在發佈時自動產生這些變更。

### <a name="set-up-the-connection-in-the-service-model"></a>設定服務模型中的連線
使用 **Imports** 元素將 **RemoteAccess** 模組和 **RemoteForwarder** 模組匯入至 [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) 檔案。

服務定義檔應類似下列已加入 `<Imports>` 元素的範例。

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
[ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) 檔案應類似下列範例，請注意 `<ConfigurationSettings>` 和 `<Certificates>` 元素。 指定的憑證必須已[上傳至雲端服務](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)。

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


## <a name="additional-resources"></a>其他資源
[如何設定雲端服務](cloud-services-how-to-configure.md)
[雲端服務常見問題集 - 遠端桌面](cloud-services-faq.md)
