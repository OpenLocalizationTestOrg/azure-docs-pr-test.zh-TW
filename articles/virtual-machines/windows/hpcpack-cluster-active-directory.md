---
title: "組件 aaaHPC 叢集與 Azure Active Directory |Microsoft 文件"
description: "了解 toointegrate HPC Pack 2016 Azure 與 Azure Active Directory 中的叢集化"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>使用 Azure Active Directory 管理 Azure 中的 HPC Pack 叢集
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) 支援與 [Azure Active Directory](../../active-directory/index.md) (Azure AD) 整合，以便系統管理員在 Azure 中部署 HPC Pack 叢集。



請遵循下列高的層級工作的 hello 本文章中的 hello 步驟： 
* 手動整合 HPC Pack 叢集與 Azure AD 租用戶
* 在 Azure 中管理和排程 HPC Pack 叢集中的工作 

HPC Pack 叢集解決方案整合與 Azure AD 會遵循標準步驟 toointegrate 其他應用程式和服務。 本文假設您已熟悉 Azure AD 中的基本使用者管理。 如需詳細資訊及背景，請參閱 hello [Azure Active Directory 文件](../../active-directory/index.md)hello 遵循 > 一節。

## <a name="benefits-of-integration"></a>整合的優點


Azure Active Directory (Azure AD) 是多租用戶雲端式目錄和身分識別管理服務，提供單一登入 (SSO) 存取 toocloud 解決方案。

HPC Pack 叢集與 Azure AD 的整合可協助您達成下列目標 hello:

* 移除 hello HPC Pack 叢集 hello 傳統 Active Directory 網域控制站。 這有助於減少維護 hello 叢集，如果這不是您的商務和加速 hello 部署程序所需的 hello 成本。
* 下列由 Azure AD 的優點運用 hello:
    *   單一登入 
    *   在 Azure 中的 hello HPC Pack 叢集使用的本機 AD 身分識別 

    ![Azure Active Directory 環境](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>必要條件
* **Azure 虛擬機器中部署的 HPC Pack 2016 叢集** - 如需相關步驟，請參閱[在 Azure 中部署 HPC Pack 2016 叢集](hpcpack-2016-cluster.md)。 您需要 hello 的 hello 前端節點的 DNS 名稱 」 和 「 叢集管理員來完成這篇文章中的 hello 步驟 hello 認證。

  > [!NOTE]
  > HPC Pack 2016 之前的 HPC Pack 版本不支援 Azure Active Directory 整合。



* **用戶端電腦**-您需要 Windows 或 Windows Server 用戶端電腦太執行 HPC Pack 用戶端公用程式。 如果您只想 toouse hello HPC Pack web 入口網站或 REST API toosubmit 作業，您可以使用您選擇的任何用戶端電腦。

* **HPC Pack 用戶端公用程式**-使用 hello 可用的安裝套件可從 Microsoft 下載中心 hello 的 hello 用戶端電腦上安裝 hello HPC Pack 用戶端公用程式。


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>步驟 1： 註冊 hello HPC 叢集中的伺服器與 Azure AD 租用戶
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 按一下**Active Directory**在 hello 左的窗格中，，然後按一下hello 您訂用帳戶中所需的目錄。 您必須擁有的權限 tooaccess 資源 hello 目錄中。
3. 按一下 [使用者]，並確定已經建立或設定使用者帳戶。
4. 按一下 應用程式 > 新增，然後按一下新增我的組織正在開發的應用程式。 輸入下列資訊在 hello 精靈中的 hello:
    * **名稱** - HPCPackClusterServer
    * **類型** - 選取 [Web 應用程式和/或 Web API]
    * **登入 URL**-hello hello 範例中，預設為基底 URL`https://hpcserver`
    * **應用程式識別碼 URI** - `https://<Directory_name>/<application_name>`。 取代`<Directory_name`> 以您的 Azure AD 租用戶，例如，完整名稱的 hello `hpclocal.onmicrosoft.com`，並取代`<application_name>`hello 您先前選擇的名稱。

5. 已加入 hello 應用程式之後，請按一下**設定**。 設定下列屬性的 hello:
    * 針對 [應用程式為多租用戶]，選取 [是]
    * 選取**是**如**使用者指派必要的 tooaccess 應用程式**。

6. 按一下 [儲存] 。 儲存完成後，按一下 [管理資訊清單]。 此動作會下載您應用程式的資訊清單 JavaScript 物件標記法 (JSON) 檔案。 編輯 hello 下載資訊清單，找出 hello`appRoles`設定並新增下列應用程式角色的 hello:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. 儲存 hello 檔案。 然後在 hello 入口網站中，按一下**管理資訊清單** > **上傳資訊清單**。 然後，您可以上傳 hello 編輯資訊清單。
8. 按一下 使用者、選取使用者，然後按一下指派。 指派其中一個 hello 可用的角色 （HpcUsers 或 HpcAdminMirror） toohello 使用者。 與 hello 目錄中的其他使用者重複此步驟。 如需叢集使用者的背景資訊，請參閱[管理叢集使用者](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)。

   > [!NOTE] 
   > toomanage 使用者，我們建議您使用 hello Azure Active Directory 預覽刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>步驟 2: Hello HPC 叢集的用戶端向 Azure AD 租用戶

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 按一下**Active Directory**在 hello 左的窗格中，，然後按一下hello 您訂用帳戶中所需的目錄。 您必須擁有的權限 tooaccess 資源 hello 目錄中。
3. 按一下 應用程式 > 新增，然後按一下新增我的組織正在開發的應用程式。 輸入下列資訊在 hello 精靈中的 hello:

    * **名稱** - HPCPackClusterClient
    * **類型** - 選取 [原生用戶端應用程式]
    * **重新導向 URI** - `http://hpcclient`

4. 已加入 hello 應用程式之後，請按一下**設定**。 複製 hello**用戶端識別碼**值，並將其儲存。 您稍後在設定應用程式時需要此資訊。

5. 在**權限 tooother 應用程式**，按一下 **新增應用程式**。 搜尋並新增 hello HpcPackClusterServer 應用程式 （在步驟 1 中建立）。

6. 在 hello**委派的權限**下拉式清單中，選取**存取 HpcClusterServer**。 然後按一下 [儲存] 。


## <a name="step-3-configure-hello-hpc-cluster"></a>步驟 3： 設定 hello HPC 叢集

1. 連接 Azure toohello HPC Pack 2016 前端節點。

2. 啟動 HPC PowerShell。

3. 執行下列命令的 hello:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    其中

    * `AADTenant`指定 hello Azure AD 租用戶名稱例如`hpclocal.onmicrosoft.com`
    * `AADClientAppId`指定 hello hello 步驟 2 中建立的應用程式的用戶端識別碼。

4. 重新啟動 hello HpcSchedulerStateful 服務。

    中包含多個前端節點的叢集，您可以執行下列 PowerShell 命令 hello 前端節點 tooswitch hello 主要複本上 hello HpcSchedulerStateful 服務的 hello:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>步驟 4： 管理和提交從 hello 用戶端的工作

tooinstall hello HPC Pack 用戶端公用程式在您的電腦上從 hello Microsoft Download Center 下載 HPC Pack 2016 安裝程式檔案 （完整安裝）。 當您開始 hello 安裝時，請選擇 hello hello 安裝選項**HPC Pack 用戶端公用程式**。

tooprepare hello 用戶端電腦，安裝期間使用的 hello 憑證[HPC 叢集設定](hpcpack-2016-cluster.md)hello 用戶端電腦上。 使用標準 Windows 憑證管理程序 tooinstall hello 公開憑證 toohello**憑證 – 目前使用者** > **受信任的根憑證授權單位**儲存。 

您可以現在執行 hello HPC Pack 命令或使用 HPC Pack 作業管理員 GUI hello toosubmit 及管理叢集工作使用 hello Azure AD 帳戶。 工作提交的選項，請參閱[提交 HPC 作業 tooan HPC Pack 叢集在 Azure 中](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)。

> [!NOTE]
> 當您第一次嘗試 tooconnect toohello HPC Pack 叢集在 Azure 中的 hello 時，會出現快顯視窗。 輸入在您 Azure AD 認證 toolog。 hello 權杖後來會快取。 更新版本中使用 Azure hello 的連線 toohello 叢集快取權杖，除非驗證變更或 hello 快取清除。
>
  
例如，完成 hello 上一個步驟之後，您可以查詢從內部部署用戶端的工作，如下所示：

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>透過 Azure AD 整合提交作業的實用 Cmdlet 

### <a name="manage-hello-local-token-cache"></a>管理 hello 本機權杖快取

HPC Pack 2016 提供兩個新的 HPC PowerShell cmdlet toomanage hello 本機權杖快取。 這些 Cmdlet 可用於非互動方式提交作業。 請參閱下列範例中的 hello:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>設定 hello 送出工作使用 hello Azure AD 帳戶的認證 

某些情況下，您可能想在 hello HPC 叢集使用者下的 toorun hello 作業 （針對加入網域的 HPC 叢集，以一個網域使用者身分執行; 對於未加入網域的 HPC 叢集，hello 前端節點上一個本機使用者身分執行）。

1. 使用下列命令 tooset hello 認證 hello:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. 然後提交 hello 工作，如下所示。 hello 作業/工作會執行下 $localUser hello 計算節點上。

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   如果`–Credential`中未指定`Submit-HpcJob`，hello 工作或任務下執行本機對應的使用者為 hello Azure AD 帳戶。 （hello HPC 叢集會建立本機使用者以相同的名稱，為 Azure AD 帳戶 toorun hello 工作 hello hello）。
    
3. 設定 hello Azure AD 帳戶的擴充的資料。 使用 hello Azure AD 帳戶的 Linux 節點上執行 MPI 工作時，這非常有用。

   * 設定 hello Azure AD 帳戶本身的擴充的資料

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * 設定擴充資料並且以 HPC 叢集使用者身分執行
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

