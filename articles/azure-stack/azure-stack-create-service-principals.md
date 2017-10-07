---
title: "服務主體的 Azure 堆疊 aaaCreate |Microsoft 文件"
description: "描述如何 toocreate 新的服務主體，可以搭配 Azure Resource Manager toomanage 存取 tooresources hello 以角色為基礎的存取控制。"
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a>提供應用程式存取 tooAzure 堆疊
當應用程式需要存取 toodeploy 或 Azure 堆疊中設定資源透過 Azure 資源管理員時，您會建立服務主體，也就是您的應用程式的認證。  然後，您可以委派只能 hello 必要的權限 toothat 服務主體。  

例如，您可能會使用 Azure 資源管理員 tooinventory 組態管理工具的 Azure 資源。  在此案例中，您可以建立服務主體，和授與 hello 讀取器角色 toothat 服務主體，限制 hello 組態管理工具僅 tooread 的存取權。 

因為服務主體會是偏好的 toorunning hello 應用程式，以您自己的認證：

* 您可以指派不同於您自己的帳戶權限的權限 toohello 服務主體。 一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。
* 如果您的責任的變更，您並沒有 toochange hello 應用程式的認證。
* 執行無人看管的指令碼時，您可以使用憑證 tooautomate 驗證。  

## <a name="getting-started"></a>開始使用

根據您部署 Azure Stack 的方式，您會從建立服務主體開始。  此文件會引導您進行為 [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) 和 [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs) 建立服務主體的程序。  一旦您已建立服務主體 hello，整組步驟常見 tooboth AD FS 與 Azure Active Directory 可用太[委派權限](azure-stack-create-service-principals.md#assign-role-to-service-principal)toohello 角色。     

## <a name="create-service-principal-for-azure-ad"></a>為 Azure AD 建立服務主體

如果您部署了 Azure 堆疊 hello 身分識別存放區以使用 Azure AD，您可以建立服務主體就像您的 Azure 執行。  本節說明如何 tooperform hello 逐步 hello 入口網站。  請確認您已 hello[必要的 Azure AD 權限](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)開頭之前。

### <a name="create-service-principal"></a>建立服務主體
在本節中，您會在 Azure AD 中建立將代表您的應用程式的應用程式 (服務主體)。

1. 登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。
2. 選取 [Azure Active Directory] > [應用程式註冊] > [新增]   
3. Hello 應用程式提供名稱和 URL。 選取  **Web 應用程式 / 應用程式開發介面**或**原生**想 toocreate hello 種應用程式。 設定後 hello 值，請選取**建立**。

您已建立應用程式的服務主體。

### <a name="get-credentials"></a>取得認證
以程式設計方式登入時，您可以使用識別碼 hello 您的應用程式和驗證金鑰。 tooget 那些值，使用 hello 下列步驟：

1. 在 Active Directory 中，從 [應用程式註冊]選取您的應用程式。

2. 複製 hello**應用程式識別碼**並將它儲存在應用程式程式碼中。 hello hello 中的應用程式[範例應用程式](#sample-applications)區段，請參閱 toothis hello 用戶端識別碼值。

     ![用戶端識別碼](./media/azure-stack-create-service-principal/image12.png)
3. toogenerate 需有驗證金鑰，選取**金鑰**。

4. 提供 hello 金鑰和 hello 金鑰的持續時間的描述。 完成時，選取 [儲存]。

在儲存之後 hello 索引鍵，會顯示 hello hello 機碼值。 因為您不能 tooretrieve hello 金鑰之後，請複製此值。 您提供 hello 索引鍵值 hello 應用程式識別碼 toosign hello 應用程式。 儲存您的應用程式可以擷取 hello 機碼值。

![儲存的金鑰](./media/azure-stack-create-service-principal/image15.png)


完成後，繼續太[將您的應用程式角色的指派](azure-stack-create-service-principals.md#assign-role-to-service-principal)。

## <a name="create-service-principal-for-ad-fs"></a>為 AD FS 建立服務主體
如果您已部署 AD FS 與 Azure 堆疊，可以使用 PowerShell toocreate 服務主體、 指派的角色存取權，以及 PowerShell 中使用該識別從登入。

### <a name="before-you-begin"></a>開始之前

[下載 hello 工具需要的 toowork 與 Azure 堆疊 tooyour 本機電腦。](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a>匯入 hello 識別 PowerShell 模組
下載 hello 工具之後，瀏覽 toohello 下載資料夾，並使用下列命令的 hello 匯入 hello 識別 PowerShell 模組：

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

當您匯入 hello 模組時，您可能會收到錯誤指出 「 AzureStack.Connect.psm1 未經數位簽署。 hello 指令碼不會執行 hello 系統上 」。 tooresolve 此問題，您可以設定執行原則 tooallow hello 指令碼執行下列命令，在提升權限的 PowerShell 工作階段中的 hello:

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a>建立服務主體的 hello
您可以建立服務主體執行 hello 下列命令，讓確定 tooupdate hello *DisplayName*參數：
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a>指派角色
您必須在建立服務主體的 hello，一次[tooa 角色指派給它](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>透過 PowerShell 登入
一旦您已指派一個角色，您可以登入 tooAzure 堆疊 hello 服務主體使用下列命令的 hello:

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a>指派角色 tooservice 主體
您的訂用帳戶中的 tooaccess 資源，您必須指派 hello 應用程式 tooa 角色。 決定哪些角色代表 hello hello 應用程式的正確權限。 toolearn 有關 hello 可用的角色，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。

您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。 權限是繼承的 toolower 範圍層級。 例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組和它所包含的任何資源。

1. 在 hello Azure 堆疊入口網站中，瀏覽 toohello 想 tooassign hello 應用程式的範圍層級。 例如，tooassign hello 訂用帳戶範圍，角色選取**訂閱**。 您可以改為選取資源群組或資源。

2. 選取 hello 特定訂用帳戶 （資源群組或資源） tooassign hello 應用程式。

     ![選取要指派的訂用帳戶](./media/azure-stack-create-service-principal/image16.png)

3. 選取 [存取控制 (IAM)]。

     ![選取存取](./media/azure-stack-create-service-principal/image17.png)

4. 選取 [新增] 。

5. 選取您想 tooassign toohello 應用程式的 hello 角色。

6. 搜尋並選取您的應用程式。

7. 選取**確定**toofinish 指派 hello 角色。 您會看到您 hello 清單中指派該範圍的 tooa 角色之使用者的應用程式。

既然您已建立服務主體，並指派角色，您可以開始使用這在您的應用程式 tooaccess Azure 堆疊資源。  

## <a name="next-steps"></a>後續步驟

[為 ADFS 新增使用者](azure-stack-add-users-adfs.md)
[管理使用者權限](azure-stack-manage-permissions.md)