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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>啟用 Azure 雲端服務中角色的遠端桌面連線

> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

您可以啟用遠端桌面連線您的角色在開發期間包含在服務定義中的 hello 遠端桌面模組，或者您可以選擇透過遠端桌面延伸模組 hello tooenable 遠端桌面。 hello 慣用的方法為 toouse hello 遠端桌面延伸您可以在 hello 應用程式部署而不需要 tooredeploy 您的應用程式時，即使啟用遠端桌面。

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>從 hello Azure 傳統入口網站中設定遠端桌面
hello Azure 傳統入口網站會使用 hello 遠端桌面的擴充方法，因此即使在 hello 應用程式部署之後，您可以啟用遠端桌面。 hello**設定**為雲端服務 頁面可讓您 tooenable 遠端桌面變更 hello 本機系統管理員帳戶使用 tooconnect toohello 虛擬機器、 hello 憑證用於驗證和設定 hello到期日。

1. 按一下**雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**設定**。
2. 按一下 hello**遠端**hello 底部的按鈕。

    ![Cloud services remote](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > 當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。 tooprevent hello 憑證使用的 tooencrypt hello 密碼重新開機，必須安裝在 hello 角色。 重新啟動，tooprevent [hello 雲端服務將憑證上傳](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後傳回 toothis 對話方塊。

3. 在**角色**，選取您想要 tooupdate 或選取 hello 角色**所有**所有角色。
4. 進行任何 hello 下列變更：

   * 遠端桌面，選取 hello tooenable**啟用遠端桌面**核取方塊。 toodisable 遠端桌面，清除 hello 核取方塊。
   * 建立帳戶 toouse 中遠端桌面連線 toohello 角色執行個體。
   * 更新 hello hello 現有帳戶密碼。
   * 選取的上傳的憑證 toouse 進行驗證 (使用憑證上傳 hello**上傳**上 hello**憑證**頁面) 或建立新的憑證。
   * 變更 hello hello 遠端桌面設定的到期日。

5. 完成組態更新時，按一下 [確定]  \(勾選記號)。

## <a name="remote-into-role-instances"></a>角色執行個體的遠端存取
Hello 角色上啟用遠端桌面之後您可以從遠端存取角色執行個體，透過各種工具。

tooconnect tooa 角色執行個體從 hello Azure 傳統入口網站：

1. 按一下**執行個體**tooopen hello**執行個體**頁面。
2. 選取已設定「遠端桌面」的角色執行個體。
3. 按一下**連接**，並遵循 hello 指示 tooopen hello 桌面。
4. 按一下**開啟**然後**連接**toostart hello 遠端桌面連線。

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>使用 Visual Studio tooremote 中將角色執行個體
在 Visual Studio 中，伺服器總管：

1. 展開 hello **Azure** > **雲端服務** > **[雲端服務名稱]**節點。
2. 展開 [預備]或 [生產]。
3. 展開 hello 個別的角色。
4. 以滑鼠右鍵按一下其中一個 hello 角色執行個體中，按一下**使用遠端桌面連線...**，然後輸入 hello 使用者名稱和密碼。

![伺服器總管遠端桌面](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>使用 PowerShell tooget hello RDP 檔案
您可以使用 hello [Get-azureremotedesktopfile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP 檔案。 您接著可以使用 hello RDP 檔案與遠端桌面連線 tooaccess hello 雲端服務。

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>以程式設計方式下載透過 hello 服務管理 REST API 的 hello RDP 檔案
您可以使用 hello[下載 RDP 檔案](https://msdn.microsoft.com/library/jj157183.aspx)REST 作業 toodownload hello RDP 檔案。

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure hello 服務定義檔中的遠端桌面
這個方法可讓您在開發期間的 hello 應用程式的 tooenable 遠端桌面。 這個方法會要求加密的密碼儲存在您的服務組態檔案及任何更新 toohello 遠端桌面設定需要重新部署的 hello 應用程式。 如果您想 tooavoid 這些缺點在於，您應該使用 hello 遠端桌面延伸模組為基礎的上面所述的方法。  

您也可以使用 Visual Studio[啟用遠端桌面連線](../vs-azure-tools-remote-desktop-roles.md)使用 hello 服務定義檔的方法。  
下列的 hello 步驟說明 hello 變更所需的 toohello 服務模型檔案 tooenable 遠端桌面。 Visual Studio 將會在發佈時自動產生這些變更。

### <a name="set-up-hello-connection-in-hello-service-model"></a>設定 hello 服務模型中的 hello 連線
使用 hello**匯入**元素 tooimport hello **RemoteAccess**模組和 hello **RemoteForwarder**模組 toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef)檔案。

hello 服務定義檔應類似下列範例與 hello 的 toohello`<Imports>`加入項目。

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
hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg)檔案應該會類似下列範例的 toohello，記下 hello`<ConfigurationSettings>`和`<Certificates>`項目。 必須指定憑證 hello [toohello 雲端服務上傳](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)。

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
[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)
