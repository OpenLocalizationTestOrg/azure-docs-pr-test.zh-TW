---
title: "部署 App Service：Azure Stack | Microsoft Docs"
description: "部署 Azure Stack 中之 App Service 的詳細指導方針"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 41be7bca865f39b445e8f99450c4acde535c0806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooazure-stack"></a>新增應用程式服務資源提供者 tooAzure 堆疊

如果您想 tooenable，您的租用戶 toocreate web、 行動裝置版和其堆疊 Azure 訂用帳戶的 API 應用程式，您必須新增[Azure App Service 資源提供者](azure-stack-app-service-overview.md)tooyour Azure 堆疊部署。 請遵循本文章中的 hello 步驟。

## <a name="download-hello-required-components"></a>下載所需的 hello 元件

1. 下載 hello[上 Azure 堆疊 preview 安裝程式的應用程式服務](http://aka.ms/appsvconmasrc1installer)。

2. 下載 hello [Azure 堆疊部署 helper 指令碼的應用程式服務](http://aka.ms/appsvconmasrc1helper)。

3. 從 hello helper 指令碼 zip 檔案解壓縮 hello 檔案。 hello 下列檔案和資料夾結構會顯示：

   - Create-AppServiceCerts.ps1
   - Create-IdentityApp.ps1
   - 模組
      - AzureStack.Identity.psm1
      - GraphAPI.psm1
   
## <a name="create-certificates-required-by-app-service-on-azure-stack"></a>建立 Azure Stack 上之 App Service 所需的憑證

此第一個指令碼搭配 hello Azure 堆疊憑證授權單位 toocreate 三個憑證所需的應用程式服務。 Hello Azure 堆疊主機上執行 hello 指令碼，請確定您 azurestack\AzureStackAdmin 作為執行 PowerShell。

1. Azurestack\AzureStackAdmin 身分執行的 PowerShell 工作階段，執行 hello**建立 AppServiceCerts.ps1** hello 資料夾解壓縮 hello helper 指令碼的指令碼。 hello 指令碼會建立三個憑證中相同的資料夾 hello 建立憑證的指令碼應用程式服務時，必須的 hello。

2. 輸入密碼 toosecure hello.pfx 檔案，並記下它。 您將需要 tooenter hello 應用程式服務在 Azure 堆疊安裝程式中。

### <a name="create-appservicecertsps1-parameters"></a>Create-AppServiceCerts.ps1 參數

| 參數 | 必要/選用 | 預設值 | 說明 |
| --- | --- | --- | --- |
| pfxPassword | 必要 | Null | 使用 tooprotect hello 憑證私密金鑰的密碼 |
| DomainName | 必要 | local.azurestack.external | Azure Stack 區域和網域尾碼 |
| CertificateAuthority | 必要 | AzS-CA01.azurestack.local | 憑證授權單位端點 |

## <a name="use-hello-installer-toodownload-and-install-app-service-on-azure-stack"></a>使用 hello installer toodownload 並安裝 Azure 堆疊上的應用程式服務

hello appservice.exe 安裝程式將會：

* 會提示您 tooaccept hello Microsoft 和協力廠商軟體授權條款。
* 收集 Azure Stack 部署資訊。
* 建立 blob 容器中 hello 指定堆疊 Azure 儲存體帳戶。
* 下載 hello 所需的檔案 tooinstall hello 應用程式服務資源提供者。
* 準備 hello 安裝 toodeploy hello hello Azure 堆疊環境中的應用程式服務資源提供者。
* 上傳 hello 檔案 toohello 應用程式服務的儲存體帳戶。
* 部署 hello 應用程式服務資源提供者。
* 建立適用於 App Service 的 DNS 區域與項目。
* 註冊 hello 應用程式服務資源提供者。
* 註冊 hello 應用程式服務主機庫項目。

hello 下列步驟會引導您進行 hello 安裝階段。

> [!NOTE]
> 您*必須*使用提高權限的帳戶 （本機或網域系統管理員） toorun hello 安裝程式。 如果您以 azurestack\azurestackuser 身分登入，則系統會提示您提供已提高權限的認證。

1. 以 azurestack\AzureStackAdmin 身分執行 appservice.exe。

2. 按一下 [在您的 Azure Stack 雲端上部署 App Service]。

    ![Azure Stack 上的 App Service 安裝程式][1]

3. 檢閱並接受 hello Microsoft 發行前版本授權條款，然後按一下**下一步**。

4. 檢閱並接受 hello 協力廠商授權條款，然後按一下**下一步**。

5. 檢閱 hello 應用程式服務雲端組態資訊，然後按一下 **下一步**。

    ![Azure Stack App Service 上的 App Service 雲端設定][2]

    > [!NOTE]
    > hello 應用程式服務在 Azure 堆疊安裝程式提供單一節點 Azure 堆疊安裝 hello 預設值。 如果您部署 Azure 堆疊 （例如，hello 網域尾碼） 時，您可以自訂選項，會據以需要 tooedit hello 值，此視窗中。 例如，如果您使用 hello 網域尾碼 mycloud.com，您管理 Azure 資源管理員端點需要 toochange tooadminmanagement。[region]。 mycloud.com。

6. 按一下 hello**連接**按鈕的下一個 toohello **Azure 堆疊訂用帳戶**方塊。

   - 如果您使用 Azure Active Directory (Azure AD)，就必須輸入您的 Azure AD 管理帳戶和密碼。 按一下 [登入] 。 您*必須*輸入您部署 Azure 堆疊時，您所提供的 hello Azure AD 帳戶。
   - 如果您使用 Active Directory 同盟服務 (AD FS)，就必須提供您的管理帳戶，例如 azurestackadmin@azurestack.local。 輸入您的密碼，然後按一下 [登入]。

7. 選取您的訂閱中 hello **Azure 堆疊訂用帳戶**方塊。

8. 在 hello **Azure 堆疊位置**方塊中，選取 hello 對應您要部署的 toohello 區域的位置。 例如，選取 [本機]。 按一下 [下一步] 。

    ![Azure Stack 上的 App Service 訂用帳戶選取項目][3]

9. 輸入 hello**資源群組名稱**為您的應用程式服務部署。 根據預設，此屬性設定太**APPSERVICE 本機**。

10. 輸入 hello**儲存體帳戶名稱**想 App Service toocreate hello 安裝的一部分。 根據預設，此屬性設定太**appsvclocalstor**。

11. 輸入 hello 的使用的 toohost hello 應用程式服務資源提供者資料庫的執行個體 hello SQL Server 詳細資料。 按一下**下一步**，和 hello 安裝程式會驗證 hello SQL 連接屬性。

    ![Azure Stack 上的 App Service 資源群組、儲存體和 SQL Server 資訊][4]

12. 按一下 hello**瀏覽**按鈕的下一個 toohello**應用程式服務的預設 SSL 憑證檔案**方塊。 移 toohello **_.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。 如果您在建立 hello 憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。

13. 輸入當您建立 hello 憑證的 hello 憑證密碼。

14. 按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的 SSL 憑證檔案**方塊。 移 toohello **api.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。 如果您在建立憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。

15. 輸入當您建立 hello 憑證的 hello 憑證密碼。

16. 按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的根憑證檔案**方塊。 移 toohello **AzureStackCertificationAuthority**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。

17. 按一下 [下一步] 。 hello 安裝程式會確認提供的 hello 憑證密碼。

    ![Azure Stack 上的 App Service 憑證詳細資料][5]

18. 檢閱 hello 應用程式服務角色設定。 hello 預設值會填入 hello 最小建議執行個體的 Sku 為每個角色。 在規劃部署時 toohelp 係核心和記憶體需求的摘要。 進行選擇之後，按一下 [下一步]。

    - **控制器**：預設會選取一個標準 A1 執行個體。 這是建議的 hello 小。 hello 控制器角色負責管理和維護的 hello 雲端應用程式服務的 hello 健全狀況。
    - **管理**：預設會選取一個標準 A2 執行個體。 tooprovide 容錯移轉時，我們建議兩個執行個體。 hello 管理角色負責 hello 應用程式服務的 Azure 資源管理員和 API 端點、 入口網站擴充功能 （系統管理員、 租用戶，函式的入口網站），以及 hello 資料服務。
    - **發行者**：預設會選取一個標準 A1 執行個體。 這是建議的 hello 小。 hello 發行者角色會負責透過 FTP 和 web 部署的內容發佈。
    - **前端**：預設會選取一個標準 A1 執行個體。 這是建議的 hello 小。 hello 前端角色負責路由要求 tooApp 服務應用程式。
    - **共用背景工作**： 根據預設，已經選取一個標準 A1 執行個體，但是您可能想 tooadd 更多。 身為系統管理員，您可以定義您的供應項目，並選擇任何 SKU 層。 hello 層必須具有至少一個核心。 hello 共用背景工作角色負責主控 web、 行動裝置，或應用程式開發介面應用程式和 Azure 函式應用程式。

    ![Azure Stack 上的 App Service 角色設定][6]

    > [!NOTE]
    > Hello technial preview 中 hello 應用程式服務資源提供者安裝程式也會部署標準 A1 執行個體 toooperate 為簡單的檔案伺服器 toosupport Azure 資源管理員。 這會針對單一節點開發套件加以保留。 對於生產工作負載，在公開上市 hello 應用程式服務安裝程式可讓您 hello 使用高可用性檔案伺服器。

19. 選擇您的部署**Windows Server 2016**從 hello hello 應用程式服務雲端計算資源提供者中所提供的 VM 映像。 按一下 [下一步] 。

    ![Azure Stack 上的 App Service VM 映像選取項目][7]

20. Hello hello 雲端應用程式服務中設定的背景工作角色，請輸入使用者名稱和密碼。 針對所有其他的 App Service 角色，輸入使用者名稱和密碼。 按一下 [下一步] 。

    ![Azure Stack 上的 App Service 認證項目][8]

21. 在 hello 摘要畫面中，確認您所做的 hello 選擇。 toomake 變更 hello 畫面，請返回並修改您的選擇。 如果您要如何 hello 設定，請選取 [hello] 核取方塊。 toostart hello 部署中，按一下 **下一步**。

    ![Azure Stack 上的 App Service 選取項目摘要][9]

22. 追蹤 hello 安裝程序。 Azure 堆疊上的應用程式服務大約需要約 45 too60 分鐘 toodeploy 根據 hello 預設選取項目。

    ![Azure Stack 上的 App Service 安裝進度][10]

23. Hello 安裝程式已順利完成之後，請按一下**結束**。

## <a name="validate-hello-app-service-on-azure-stack-installation"></a>驗證 Azure 堆疊安裝上的 hello 應用程式服務

1. 在 hello Azure 堆疊管理員入口網站中瀏覽 toohello hello 安裝程式所建立的資源群組。 根據預設值，此群組是 **APPSERVICE-LOCAL**。

2. 找出 **CN0-VM**。 按一下 tooconnect toohello VM，**連接**hello 上**虛擬機器**刀鋒視窗。

3. 在此 vm 的 hello 桌面上，按兩下**網站雲端管理主控台**。

4. 跳過**管理的伺服器**。

5. 當所有 hello 機器顯示**準備**一或多個背景工作，請繼續進行 toostep 6。

6. 關閉遠端桌面的電腦 hello，並傳回 toohello hello 應用程式服務安裝程式的執行所在的電腦。

    > [!NOTE]
    > 您不需要一或多個工作者 toodisplay toowait**準備**toocomplete hello 安裝 Azure 堆疊上的應用程式服務。 不過，您需要至少一個背景工作的準備 toodeploy 行動、 web API 應用程式或 Azure 函式。

    ![Azure Stack 上的 App Service 受管理伺服器狀態][11]

## <a name="configure-an-azure-ad-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>設定虛擬機器規模集整合 Azure AD 服務主體上背景工作層和 SSO hello Azure 函式的入口網站和進階開發人員工具

>[!NOTE]
> 這些步驟適用於的 tooAzure AD 保護僅限 Azure 堆疊環境。

系統管理員需要 tooconfigure SSO 至：

* 啟用進階開發人員工具，應用程式服務 (Kudu) 中的 hello。
* 啟用 hello hello Azure 函式的入口網站體驗。

請遵循下列步驟：

1. 以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。

2. 移 hello 指令碼下載並解壓縮在 hello toohello 位置[先決條件步驟](#Download-Required-Components)。

3. [安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。

4. 在 hello 相同的 PowerShell 工作階段中執行 hello **CreateIdentityApp.ps1**指令碼。 當系統提示需要您的 Azure AD 租用戶識別碼時，請輸入您使用的 Azure 堆疊部署，例如 myazurestack.onmicrosoft.com hello Azure AD 租用戶識別碼。

5. 在 hello**認證**視窗中，輸入您的 Azure AD 服務系統管理員帳戶和密碼。 按一下 [確定] 。

6. 輸入 hello hello 憑證檔案的路徑和憑證密碼[稍早建立的憑證](# Create certificates toobe used by App Service on Azure Stack)。 針對此步驟建立預設的 hello 憑證是 sso.appservice.local.azurestack.external.pfx。

7. hello 指令碼在 hello 租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼名為**UpdateConfigOnController.ps1**。

    >[!NOTE]
    > 請記下 hello**應用程式識別碼**hello PowerShell 輸出中傳回。 您需要此資訊 toosearch 為其步驟 12 中。

8. 複製 hello 識別應用程式的憑證檔案和 hello 產生指令碼太**CN0 VM**使用遠端桌面工作階段。

9. 開啟新的瀏覽器視窗，並以登入 toohello Azure 入口網站 (portal.azure.com) hello **Azure Active Directory 服務系統管理員**。

10. 開啟 hello Azure AD 資源提供者。

11. 按一下 [應用程式註冊]。

12. 搜尋 hello**應用程式識別碼**步驟 7 的一部分傳回。 隨即列出 App Service 應用程式。

13. 按一下**應用程式**hello 清單，並開啟 hello**金鑰**刀鋒視窗。

14. 加入新的金鑰與**描述-函式的入口網站**，並設定 hello**到期日**太**永久有效**。

15. 按一下**儲存**，，然後複製 hello 產生索引鍵。

    >[!NOTE]
    > 是確定 toonote 或複製 hello 金鑰時產生。 儲存之後，您無法再次檢視，而且您需要 tooregenerate 新的金鑰。

    ![Azure Stack 上的 App Service 應用程式金鑰][12]

16. 傳回 toohello**應用程式註冊**在 Azure AD 中。

17. 按一下 [必要權限] > [授與權限] > [是]。

    ![Azure Stack 上的 App Service SSO 授與][13]

18. 傳回太**CN0 VM**，並開啟 hello**網站雲端管理主控台**一次。

19. 選取 hello**設定**節點 hello 左的窗格中，並尋找 hello **ApplicationClientSecret**設定。

20. 以滑鼠右鍵按一下並選取 [編輯]。 貼在步驟 15，產生的 hello 金鑰，然後按一下**確定**。

    ![Azure Stack 上的 App Service 應用程式金鑰][14]

21. 開啟系統管理員的 PowerShell 視窗。 瀏覽 toohello hello 指令碼檔案和憑證，已複製在步驟 7 中的目錄。

22. 執行 hello 指令碼檔案。 此指令碼檔案中 hello 應用程式服務在 Azure 堆疊設定輸入 hello 屬性，並起始所有前端及管理角色上的修復操作。

| 參數 | 必要/選用 | 預設值 | 說明 |
| --- | --- | --- | --- |
| DirectoryTenantName | 強制 | Null | Azure AD 租用戶識別碼。 提供 hello GUID 或字串，例如 myazureaaddirectory.onmicrosoft.com |
| TenantAzure Resource ManagerEndpoint | 強制 | management.local.azurestack.external | hello 租用戶 Azure 資源管理員端點 |
| AzureStackCredential | 強制 | Null | Azure AD 系統管理員 |
| CertificateFilePath | 強制 | Null | 路徑 toohello 識別應用程式的憑證檔案先前產生 |
| CertificatePassword | 強制 | Null | 使用 tooprotect hello 憑證私密金鑰的密碼 |
| DomainName | 必要 | local.azurestack.external | Azure Stack 區域和網域尾碼 |
| AdfsMachineName | 選用 | 在 Azure AD 部署，但需要在 AD FS 部署的 hello 案例中會忽略。 AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local |

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>設定虛擬機器規模集整合 AD FS 服務主體上背景工作層和 SSO hello Azure 函式的入口網站和進階開發人員工具

>[!NOTE]
> 這些步驟適用於的 tooAD FS 保護僅限 Azure 堆疊環境。

系統管理員需要 tooconfigure SSO 至：

* 針對背景工作層上的虛擬機器擴展集整合設定服務主體。
* 啟用進階開發人員工具，應用程式服務 (Kudu) 中的 hello。
* 啟用 hello hello Azure 函式的入口網站體驗。 

請遵循下列步驟：

1. 以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。

2. 移 hello 指令碼下載並解壓縮在 hello toohello 位置[先決條件步驟](#Download-Required-Components)。

3. [安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。

4. 在 hello 相同的 PowerShell 工作階段中執行 hello **CreateIdentityApp.ps1**指令碼。 當系統提示您提供 Azure AD 租用戶識別碼時，請輸入 **ADFS**。

5. 在 hello**認證**視窗中，輸入您的 AD FS 服務系統管理員帳戶和密碼。 按一下 [確定] 。

6. 提供 hello hello 憑證檔案的路徑和憑證密碼[稍早建立的憑證](# Create certificates toobe used by App Service on Azure Stack)。 針對此步驟建立預設的 hello 憑證是 sso.appservice.local.azurestack.external.pfx。

7. hello 指令碼在 hello 租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼名為**UpdateConfigOnController.ps1**。

8. 複製 hello 識別應用程式的憑證檔案和 hello 產生指令碼 toohello **CN0 VM**使用遠端桌面工作階段。

9. 傳回太**CN0 VM**。

10. 開啟系統管理員 PowerShell 視窗，並瀏覽 toohello hello 指令碼檔案和憑證，已複製在步驟 7 中的目錄。

11. 執行 hello 指令碼檔案。 此指令碼檔案中 hello 應用程式服務在 Azure 堆疊設定輸入 hello 屬性，並起始所有前端及管理角色上的修復操作。

| 參數 | 必要/選用 | 預設值 | 說明 |
| --- | --- | --- | --- |
| DirectoryTenantName | 強制 | Null | 使用**ADFS** hello AD FS 環境 |
| TenantAzure Resource ManagerEndpoint | 強制 | management.local.azurestack.external | hello 租用戶 Azure 資源管理員端點 |
| AzureStackCredential | 強制 | Null | hello AD FS 服務系統管理員帳戶 |
| CertificateFilePath | 強制 | Null | 路徑 toohello 識別應用程式的憑證檔案先前產生 |
| CertificatePassword | 強制 | Null | 使用 tooprotect hello 憑證私密金鑰的密碼 |
| DomainName | 必要 | local.azurestack.external | Azure Stack 區域和網域尾碼 |
| AdfsMachineName | 選用 | AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local |

## <a name="test-drive-app-service-on-azure-stack"></a>測試 Azure Stack 上的 App Service

您部署及註冊 hello 應用程式服務資源提供者之後，測試 toomake 確定租用戶可以將 web、 mobile 及 API 應用程式部署。

> [!NOTE]
> 您需要 toocreate hello 計劃中的 hello Microsoft.Web 命名空間提供項目。 然後，您需要 toohave 訂閱 toothis 優惠的租用戶訂用帳戶。 如需詳細資訊，請參閱[建立供應項目](azure-stack-create-offer.md)和[建立方案](azure-stack-create-plan.md)。
>
您*必須*有使用 Azure 堆疊上的應用程式服務的租用戶訂用帳戶 toocreate 應用程式。 服務系統管理員可以完成 hello 系統管理入口網站中的 hello 唯一功能是相關的 toohello 資源提供者管理的應用程式服務。 這些功能包括新增容量、設定部署來源，以及新增背景工作層和 SKU。
>
為準，hello 第三個技術預覽、 toocreate web、 mobile API 和 Azure 應用程式的功能，您必須使用 hello 租用戶入口網站，並有租用戶的訂用帳戶。 

1. 在 hello Azure 堆疊租用戶入口網站中，按一下 **新增** > **Web + 行動** > **Web 應用程式**。

2. 在 hello **Web 應用程式**刀鋒視窗中，輸入的名稱在 hello **Web 應用程式**方塊。

3. 按一下 [資源群組] 下方的 [新增]。 輸入的名稱在 hello**資源群組**方塊。

4. 按一下 [App Service 方案/位置] > [新建]。

5. 在 hello **App Service 方案**刀鋒視窗中，輸入的名稱在 hello **App Service 方案**方塊。

6. 按一下 [定價層] > [免費 - 共用] 或 [共用 - 共用] > [選取] > [確定] > [建立]。

7. 在下一分鐘 hello 新 web 應用程式的磚會顯示 hello 儀表板上。 按一下 hello 磚。

8. 在 hello **Web 應用程式**刀鋒視窗中，按一下 **瀏覽**tooview hello 預設網站，此應用程式。

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>部署 WordPress、DNN 或 Django 網站 (選擇性)

1. 在 hello Azure 堆疊租用戶入口網站中，按一下   **+** toohello Azure Marketplace、 部署如 Django 網站，請等待順利完成。 hello Django web 平台會使用檔案系統為基礎的資料庫。 它不需要任何額外的資源提供者，例如 SQL 或 MySQL。

2. 如果您也會部署 MySQL 資源提供者，您可以部署的 hello Marketplace WordPress 網站。 當系統提示您為資料庫參數時，輸入 hello 使用者名稱做為 *User1@Server1*使用 hello 使用者名稱和您選擇的伺服器名稱。

3. 如果您也會部署 SQL Server 資源提供者，您可以部署的 hello Marketplace DNN 網站。 當系統提示您為資料庫參數時，選擇 hello 電腦連線的 tooyour 資源提供者的 SQL server 的資料庫。

## <a name="next-steps"></a>後續步驟

您也可以嘗試其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)。

- [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)
- [MySQL 資源提供者](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy/app-service-exe-start.png
[2]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-cloud-configuration.png
[3]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-subscription-location-populated.png
[4]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-resource-group-sql.png
[5]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-certificates.png
[6]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-configuration.png
[7]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-vm-image-selection.png
[8]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-credentials.png
[9]: ./media/azure-stack-app-service-deploy/app-service-exe-selection-summary.png
[10]: ./media/azure-stack-app-service-deploy/app-service-exe-installation-progress.png
[11]: ./media/azure-stack-app-service-deploy/managed-servers.png
[12]: ./media/azure-stack-app-service-deploy/app-service-sso-keys.png
[13]: ./media/azure-stack-app-service-deploy/app-service-sso-grant.png
[14]: ./media/azure-stack-app-service-deploy/app-service-application-secret.png

<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
