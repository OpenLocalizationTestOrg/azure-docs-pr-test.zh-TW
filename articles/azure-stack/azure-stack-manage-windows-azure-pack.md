---
title: "從 Azure 堆疊 aaaManage Windows Azure Pack 虛擬機器 |Microsoft 文件"
description: "深入了解如何 toomanage hello Azure 堆疊中的使用者入口網站中的 Windows Azure Pack (WAP) Vm。"
services: azure-stack
documentationcenter: 
author: walterov
manager: byronr
editor: 
ms.assetid: 213c2792-d404-4b44-8340-235adf3f8f0b
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: walterov
ms.openlocfilehash: 97dbe34055667a72fddc8507ae389562e885a32e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a>從 Azure Stack 管理 Windows Azure 套件虛擬機器
在 hello Azure 堆疊開發套件，您可以啟用從 hello Azure 堆疊使用者入口網站 tootenant 虛擬機器執行於 Windows Azure 組件的存取。 租用戶可使用 hello Azure 堆疊入口 toomanage 其現有的 IaaS 虛擬機器和虛擬網路。 這些資源是透過使用在 Windows Azure 套件 hello 基礎 Service Provider Foundation (SPF) 和 Virtual Machine Manager (VMM) 元件。 具體而言，租用戶可以：

* 瀏覽資源
* 檢查設定值
* 停止或啟動虛擬機器
* 透過遠端桌面通訊協定 (RDP) 連線 tooa 虛擬機器
* 建立和管理檢查點
* 刪除虛擬機器和虛擬網路

Windows Azure Pack 連接器 hello 提供此功能的 Azure 堆疊 （預覽）。 本文將說明如何 tooconfigure hello 針對單一節點的 Azure 堆疊環境的連接器。

Hello 連接器此預覽版本，請注意 hello 下列各項：
* 使用 hello Windows Azure Pack Connector 只在測試環境中 （針對 Azure 堆疊與 Windows Azure Pack），而不是在生產部署。
* 您必須擁有 Windows Azure 套件更新彙總套件 (UR) 9.1 或更新版本，以及 System Center SPF 和 VMM UR 9 或更新版本。
* hello VMM 和 SPF 元件可以是 System Center 2012 R2 或 System Center 2016。
* 您必須在 Azure Stack 和 Windows Azure 套件都執行設定步驟。
* hello 指示適用於 toonon 雲端平台系統 (CPS) 環境中。
* tooreview hello 已知的問題，請參閱[疑難排解 Microsoft Azure 堆疊](azure-stack-troubleshooting.md)。


## <a name="architecture"></a>架構
hello 下列圖表顯示 hello Windows Azure Pack 連接器 hello 主要元件。

![hello Windows Azure Pack 連接器元件](media/azure-stack-manage-wap/image1.png)

請注意下列詳細資料的 hello:
* hello Azure 堆疊使用者入口網站從這兩個雲端 （Azure 堆疊和 Windows Azure Pack） 中存取 hello 資源資訊。
* hello 使用者必須具有兩個環境中有效的帳戶。
* hello Azure 堆疊使用者入口網站必須具有網路存取 toohello 元件在 Windows Azure 組件上執行。
* 在 hello **WAP** > 一節的 hello 圖表中，您可以查看 hello 新 Windows Azure Pack Connector 模組 （WAP 擴充功能和連接器），並 hello 現有 Windows Azure Pack 租用戶 API 與 SPF 和 VMM 元件。


## <a name="identity-management"></a>身分識別管理
Windows Azure Pack 租用戶 API hello 必須信任 hello Azure 堆疊安全性權杖服務 (STS)。

當使用者執行透過 hello Azure 堆疊入口網站的動作目標的 Windows Azure Pack 的資源時，hello 入口網站會使用 hello Windows Azure Pack 租用戶 API。 因此，hello 提供使用者驗證語彙基元必須來自受信任的 STS。 請參閱下列圖表中的 hello:

![Windows Azure 套件連接器驗證的圖表](media/azure-stack-manage-wap/image2.png)

Hello 開發套件在環境中，Windows Azure Pack and Azure 堆疊有獨立的身分識別提供者。 從 hello Azure 堆疊入口網站存取這兩種環境的使用者必須擁有的 hello 中這兩個身分識別提供者名稱相同的使用者主體名稱 (UPN)。 例如，hello 帳戶 *azurestackadmin@azurestack.local* 也應該存在於 hello STS for Windows Azure Pack 中。 在 AD FS 並未設定 toosupport 輸出信任關係，您會建立信任從 hello Windows Azure Pack 元件 (租用戶 API) toohello Azure 堆疊 AD FS 執行個體。

## <a name="prerequisites"></a>必要條件

### <a name="download-hello-windows-azure-pack-connector"></a>下載 Windows Azure Pack 連接器 hello
在 hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc)，請下載 hello.exe 檔案，並將它解壓縮 tooyour 本機電腦。 稍後，您可以複製可以存取 Windows Azure Pack 環境的 hello 內容 tooa 電腦。

### <a name="deployment-option-requirement"></a>部署選項需求
與 Windows Azure Pack toointegrate，可以使用 AD FS hello 或 hello Azure Active Directory 選項來部署 Azure 堆疊。

### <a name="connectivity-requirements"></a>連線能力需求
1. 從 hello 電腦存取 hello Azure 堆疊使用者入口網站，請確定您可以透過 hello web 瀏覽器存取 hello Windows Azure Pack 租用戶入口網站。
2. hello AzS WASP01 Azure 堆疊上的虛擬機器必須能夠 tooconnect toohello Windows Azure Pack 租用戶入口網站的電腦。 使用 Ping.exe tooverify 網路連線。 
3.  您必須擁有 hello 新連接器服務的有效憑證。 這些 SSL 憑證必須由受信任的憑證授權單位 (CA) 發行。 您不得使用自我簽署的憑證。 hello SSL 憑證必須受 Azure 堆疊 (特別是 hello AzS WASP01 VM)，而且 hello 租用戶的任何其他電腦可以使用 tooaccess hello Azure 堆疊使用者入口網站。
 
    >[!NOTE]
    因為 AzS WASP01 hello Server Core 安裝選項執行 Windows Server，您可以使用命令列工具，例如 Certutil.ext tooimport hello 憑證。 例如，您可以在其中複製 hello.cer 檔案 tooc:\temp 上 AzS WASP01，然後執行 hello 命令**certutil addstore"CA""c:\temp\certname.cer"**。

4.  tooestablish RDP 連線 tooWindows 透過 hello Azure 堆疊入口網站的 Azure Pack 租用戶虛擬機器，hello Windows Azure Pack 環境必須允許遠端桌面流量 toohello 租用戶 Vm。
5.  Azure 堆疊租用戶虛擬機器與 Windows Azure Pack 租用戶虛擬機器之間的連線，其外部 IP 位址必須可路由傳送 hello 兩個環境。 這種連線能力也可能包括建立 DNS 伺服器 tooresolve 虛擬機器名稱 hello 環境之間的關聯。

### <a name="iis-requirements"></a>IIS 需求
裝載 hello Windows Azure Pack 租用戶入口網站 （這可能是實體的主機、 虛擬機器或多部虛擬機器） 的 hello 電腦必須有 hello URL 重寫 IIS 擴充功能安裝。 如果尚未安裝，您可以從[這裡](https://www.iis.net/downloads/microsoft/url-rewrite)下載。 如果多個虛擬機器裝載 hello 租用戶入口網站，請在每個虛擬機器上安裝 hello 擴充功能。

## <a name="configure-azure-stack"></a>設定 Azure Stack
設定 Windows Azure Pack 連接器 hello 之前，您必須啟用 hello Azure 堆疊使用者入口網站中的多個雲端模式。 這個模式可讓使用者 tooselect 從哪些雲端 tooaccess 資源。

tooenable 多雲端模式中，您必須 Azure 堆疊部署後執行 hello 新增 AzurePackConnector.ps1 指令碼。 hello 下表描述 hello 指令碼參數。


|  參數 | 說明 | 範例 |   
| -------- | ------------- | ------- |  
| AzurePackClouds | Windows Azure Pack 連接器 hello 的 Uri。 這些 Uri 應該對應 toohello Windows Azure Pack 租用戶入口網站。 | @{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}<br><br>  （根據預設，hello 連接埠值為 40005）。 |  
| AzureStackCloudName | 標籤 toorepresent hello 本機堆疊 Azure 雲端。| "AzureStack" |
| DisableMultiCloud | 交換器 toodisable 多雲端模式。| N/A |
| | |

立即部署之後，或更新版本，您可以執行 hello 新增 AzurePackConnector.ps1 指令碼。 toorun hello 指令碼之後立即進行部署、 使用 hello 相同完成 Azure 堆疊部署所在的 Windows PowerShell 工作階段。 否則，您可以開啟新的 Windows PowerShell 工作階段，以系統管理員身分 （登入為 hello azurestackadmin 帳戶）。

1. 使用下列命令 （具有值特定 tooyour 環境） 的 hello 執行 hello 新增 AzurePackConnector.ps1 指令碼。 請注意，hello 新增 AzurePackConnector 指令碼可讓您 tooadd 多個 Windows Azure Pack 連接器端點。
 
 ```powershell
    $cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local", `
    (ConvertTo-SecureString -String "<password>" -AsPlainText -Force))
    $session = New-PSSession -ComputerName 'azs-ercs01' `
     -Credential $cred `
     -ConfigurationName PrivilegedEndpoint `
     -Authentication Credssp

    # Enable Multicloud
    Invoke-Command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
    @{CloudName = "AzurePack_1"; CloudEndpoint = "https://waptenantportal1:40005"},`
    @{CloudName = "AzurePack_2"; CloudEndpoint = "https://waptenantportal2:40005" } `
    -AzureStackCloudName "AzureStack" }

 ```
> [!NOTE]
> Hello 目前組建中發生問題時的 hello 新增 AzurePackConnector 指令碼結束後，它會保留在輪詢迴圈長的時間 （幾分鐘的時間） 之前結束。 您會看到 hello 訊息之後**VERBOSE： 步驟 「 設定 Azure Pack 連接器 」 狀態: 「 成功 」**，您可以停止 hello 指令碼，或等到它本身就會停止。 因為 hello 組態已成功，它將不會有所差別。

2. 記下所產生的指令碼，為您指定每個 Windows Azure Pack 環境的 hello 輸出檔。 hello 檔位於： \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput。 這些檔案包含必要的 tooconfigure hello 目標 Windows Azure Pack 環境的 hello 資訊。 您可以將此檔案當做參數 tooa 指令碼，這些指示中的更新版本。 這個檔案包含下列資訊的 hello:

    * **AzurePackConnectorEndpoint**： 包含 hello 端點 toohello Windows Azure Pack 連接器服務。
    * **AuthenticationIdentityProviderPartner**： 包含下列值組的 hello:
        * 驗證權杖簽章 hello Windows Azure Pack 租用戶 API 的憑證必須 tootrust tooaccept 呼叫從 hello Azure 堆疊入口網站擴充功能。

        * hello"Realm"hello 簽署憑證與相關聯。 例如：https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/。

3.  包含 hello 輸出檔的瀏覽 toohello 資料夾 (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput)，並複製 hello 檔案 tooyour 本機電腦。 hello 檔案看起來類似 toothis: AzurePack-06-27-15-50.txt。

4.  測試 hello 組態。

    a. 開啟瀏覽器，並登入 toohello Azure 堆疊使用者入口網站 (https://portal.local.azurestack.external/)。
    
    b. 為租用戶和 hello 入口網站載入登入之後，您會看到的錯誤不能 toofetch 訂閱或 hello Azure Pack 雲端擴充功能。 按一下**確定**tooclose 這些訊息。 (在您設定 Windows Azure 套件後這些錯誤訊息就會消失。)

    c. 請注意 hello**雲端**在 hello hello 入口網站的左上角的下拉式清單。

    ![hello Azure 堆疊使用者介面中的 hello 雲端選取器](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a>設定 Windows Azure 套件
只有此預覽版本連接器需要手動設定 Windows Azure 套件。

>[!IMPORTANT]
此預覽版本中，使用 hello Windows Azure Pack Connector 只在測試環境中，而不是在生產部署。

1.  安裝連接器的 MSI 檔案 hello Windows Azure Pack 租用戶入口網站的虛擬機器，然後安裝憑證。 (若您有多部租用戶入口網站虛擬機器，則必須在每部虛擬機器上都完成此步驟。)

    a. 在 檔案總管 中，複製 hello **WAPConnector** （什麼您之前下載） 的資料夾名為 tooa 資料夾**c:\temp** hello 租用戶入口網站的虛擬機器中。

    b. 開啟主控台或 RDP 連線 toohello 租用戶入口網站虛擬機器。

    c. 將目錄變更太**c:\temp\wapconnector\setup\scripts**，並執行的 hello**安裝 Connector.ps1**指令碼 tooinstall 三 MSI 檔案。 不需要任何參數。

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     d. 將目錄變更太**c:\inetpub**並確認已安裝的 hello 三個新的站台：

       * MgmtSvc-Connector

       * MgmtSvc-ConnectorExtension

       * MgmtSvc-ConnectorController

    e. 從 hello 相同**c:\temp\wapconnector\setup\scripts**資料夾中，執行 hello**設定 Certificates.ps1** tooinstall 憑證編寫指令碼。 根據預設，它會使用 hello 適用於在 Windows Azure Pack 中的 hello 租用戶入口網站的相同憑證。 請確定這是有效的憑證 （hello Azure 堆疊 AzS WASP01 虛擬機器和任何用戶端電腦存取 hello Azure 堆疊入口網站的信任）。 否則，通訊將無法運作。 (或者，您可以明確地傳遞憑證指紋做為參數使用 hello-憑證指紋參數。)

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    f. 下列三種服務，執行 hello toofinish hello 組態**設定 WapConnector.ps1** tooupdate hello Web.config 檔案參數的指令碼。

    |  參數 | 說明 | 範例 |   
    | -------- | ------------- | ------- |  
    | TenantPortalFQDN | Windows Azure Pack 租用戶網站 FQDN hello。 | tenant.contoso.com | 
    | TenantAPIFQDN | hello Windows Azure Pack 租用戶 API FQDN。 | tenantapi.contoso.com  |
    | AzureStackPortalFQDN | hello Azure 堆疊使用者入口網站，FQDN。 | portal.local.azurestack.external |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    g. 若您有多部租用戶入口網站虛擬機器，請在每部虛擬機器上重複步驟 1。

2. 安裝 hello 每個 Windows Azure Pack 租用戶 API 虛擬機器上的新租用戶 API MSI。

    a. 如果負載平衡器正在使用中，您可能想 toomark hello 虛擬機器為離線狀態。

    b. 在 檔案總管 中，複製 hello **WAPConnector** tooa 資料夾名為**c:\temp**每個租用戶 API 的電腦上。

    c. 複製 hello AzurePackConnectorOutput.txt 您稍早儲存檔案，太**c:\temp\WAPConnector**。

    d. 開啟主控台或 RDP 連線 toohello 租用戶 API VM 複製 hello 檔案。
    
    e. 將目錄變更太**c:\temp\wapconnector\setup\scripts**，並執行**更新 TenantAPI.ps1**。 這個新版本的 hello WAP 租用戶 API 包含變更 tooenable 與 hello 目前 STS，不僅與 hello Azure 堆疊中的 AD FS 執行個體的信任關係。

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    f.  重複步驟 2 執行 hello 租用戶 API 的任何其他虛擬機器上。
3. 從**只有一個**的 hello 租用戶 API Vm，hello 設定 TrustAzureStack.ps1 指令碼 tooadd 信任關係之間 hello 租用戶 API 和 hello AD FS 執行個體上執行 Azure 堆疊。 您必須使用的帳戶具有系統管理員存取 toohello Microsoft.MgmtSvc.Store 資料庫複本。 此指令碼有 hello 下列參數：

    | 參數 | 說明 | 範例 |
    | --------- | ------------| ------- |
   | SqlServer | hello hello 包含 hello Microsoft.MgmtSvc.Store 資料庫複本的 SQL Server 名稱。 這是必要參數。 | SQLServer | 
   | DataFile | 在 hello hello Azure 堆疊多雲端之模式的組態稍早所產生的 hello 輸出檔。 這是必要參數。 | AzurePack-06-27-15-50.txt | 
   | PromptForSqlCredential | 指出，hello 指令碼應該會提示您以互動方式的 SQL 驗證認證 toouse 連接 toohello SQL Server 執行個體時。 指定認證的 hello 必須有足夠的權限 toouninstall 資料庫，結構描述，並刪除使用者登入。 如果未提供，hello 指令碼會假設該目前使用者的內容有權存取。 | 不需要任何值。 |
   |  |  |

    如果您不知道 hello SQL Server toouse，您就可以進行探索。 Toohello 租用戶 API 的電腦連線、 使用 hello Unprotect Mgmtsvc-adminsite 命令 toounprotect hello 租用戶 API Web.config 檔案中，並尋找 hello hello 連接字串中的伺服器名稱。 請記住 toorun 保護 Mgmtsvc-adminsite 再次 tooprotect hello 租用戶 API Web.config 檔案。

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a>範例
hello 下列範例顯示完整的 Windows Azure Pack Connector 部署在單一節點 Azure 堆疊設定，以及兩個 Windows Azure Pack Express 安裝。 (每個快速安裝位於單一電腦上，與 hello 範例名稱*wapcomputer1*和*wapcomputer2*。)

```powershell
# Run hello following script on hello Azure Stack host
$cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local",`
     (ConvertTo-SecureString -String "p@ssw0rd" -AsPlainText -Force))
$session = New-PSSession -ComputerName 'azs-ercs01' -Credential $cred `
     -ConfigurationName PrivilegedEndpoint -Authentication Credssp
 
# Enable Multicloud
invoke-command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
     @{CloudName = "AzurePack_1"; CloudEndpoint = "https://wapcomputer1.contoso.com:40005"},`
     @{CloudName = "AzurePack_2"; CloudEndpoint = "https://wapcomputer2.contoso.com:40005"}`
     -AzureStackCloudName "AzureStack" }  

```
從 hello 下載 hello.exe 檔案[Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc)，將它解壓縮，並將複製 hello WAPConnector 資料夾 tooa **c:\temp** hello Windows Azure Pack 的電腦上的資料夾。 複製產生做為輸出 hello 至上一個指令碼中的 hello 檔案 (位於\\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector**資料夾。 (hello 檔案會看起來類似 toothis: AzurePack-06-27-15-50.txt。)然後，執行下列指令碼中，每一次的執行個體的 Windows Azure 套件 hello:

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for hello new Connector services
.\Configure-Certificates.ps1

# Configure hello Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install hello updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with hello Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a>疑難排解秘訣
1.  確保 Azure Stack 與 Windows Azure 套件之間有網路連線能力。 此連接應該是任何存取 hello Azure 堆疊入口網站的租用戶電腦與 hello Windows Azure Pack 租用戶入口網站虛擬機器之間執行 hello 新連接器服務。
2.  確保所有指定的 FQDN 都正確。
3.  請確定 hello hello 新連接器服務中使用的 SSL 憑證信任由 Azure 堆疊 (特別是 hello AzS WASP01 VM)，而且任何其他電腦 hello 租用戶可以使用 tooaccess hello Azure 堆疊使用者入口網站。
4. 若要檢閱已知的問題，請參閱 [Microsoft Azure Stack 疑難排解](azure-stack-troubleshooting.md)。


## <a name="next-steps"></a>後續步驟
[使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站](azure-stack-manage-portals.md)
