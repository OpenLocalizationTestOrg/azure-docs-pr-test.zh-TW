---
title: "aaaHow tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory |Microsoft 文件"
description: "設定您已加入網域的 Windows 裝置 tooregister 自動且無訊息地與 Azure Active Directory。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory

toouse [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)，您的電腦必須向 Azure Active Directory (Azure AD)。 您可以在組織中取得一份已註冊的裝置使用 hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)指令程式在 hello [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0)。 

本文章提供您 hello 步驟來設定與 Azure AD 組織中的 hello 自動註冊的 Windows 網域的裝置。


如需下列詳細資訊︰

- 有關條件式存取，請參閱 [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)。 
- Windows 10 裝置 hello 工作地點和增強的 hello 體驗時向 Azure AD，請參閱[hello 企業版的 Windows 10： 使用工作用裝置](active-directory-azureadjoin-windows10-devices-overview.md)。
- Windows 10 企業版 E3 中的 CSP，請參閱 hello [CSP 概觀中的 Windows 10 企業版 E3](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview)。


## <a name="before-you-begin"></a>開始之前

開始設定您的環境中的 hello 自動註冊的 Windows 網域的裝置之前，您應該熟悉 hello 支援案例和 hello 條件約束。  

tooimprove hello 可讀性的 hello 描述，本主題會使用下列詞彙的 hello: 

- **目前的 Windows 裝置**-此一詞是指 toodomain 聯結的裝置執行 Windows 10 或 Windows Server 2016。
- **舊版的 Windows 裝置**-此一詞是指 tooall**支援**加入網域的 Windows 裝置的非執行 Windows 10 或 Windows Server 2016。  


### <a name="windows-current-devices"></a>現行 Windows 裝置

- 對於執行 hello Windows 桌面作業系統的裝置，我們建議使用 Windows 10 年度更新 （版本 1607年） 或更新版本。 
- hello Windows 目前裝置的註冊**是**支援在非同盟的環境，例如密碼雜湊同步處理設定。  


### <a name="windows-down-level-devices"></a>舊版 Windows 裝置

- 支援下列舊版的 Windows 裝置 hello:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- hello 舊版的 Windows 裝置的註冊**是**透過無接縫單一登入的非同盟環境中支援[Azure Active Directory 無接縫單一登入](https://aka.ms/hybrid/sso)。
- hello 舊版的 Windows 裝置的註冊**不**支援使用漫遊設定檔的裝置。 如果您倚賴設定檔或設定的漫遊，請使用 Windows 10。



## <a name="prerequisites"></a>必要條件

開始啟用 hello 自動登錄的組織中已加入網域的裝置之前，您需要確定您正在執行最新版的 Azure AD toomake 連接。

Azure AD Connect：

- 會保留在內部部署 Active Directory (AD) 和 Azure AD 中的 hello 裝置物件中的 hello 電腦帳戶的 hello 關聯。 
- 啟用其他裝置相關功能，例如 Windows Hello 企業版。



## <a name="configuration-steps"></a>組態步驟

本主題包含所有的一般組態案例的 hello 必要步驟。  
使用下列資料表 tooget 您案例所需的 hello 步驟的概觀的 hello:  



| 步驟                                      | 現行 Windows 和密碼雜湊同步處理 | 現行 Windows 和同盟 | 舊版 Windows |
| :--                                        | :-:                                    | :-:                            | :-:                |
| 步驟 1︰設定服務連接點 | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| 步驟 2︰設定宣告的發行           |                                        | ![勾選][1]                    | ![勾選][1]        |
| 步驟 3︰啟用非 Windows 10 裝置      |                                        |                                | ![勾選][1]        |
| 步驟 4︰控制部署與導入     | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| 步驟 5︰驗證已註冊的裝置          | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |



## <a name="step-1-configure-service-connection-point"></a>步驟 1︰設定服務連接點

在 hello 註冊 toodiscover Azure AD 租用戶資訊期間使用您的裝置 hello 服務連線點 (SCP) 物件。 在您內部部署 Active Directory (AD)、 hello 自動登錄的裝置已加入網域的 hello SCP 物件必須存在於 hello 設定命名內容分割 hello 電腦樹系。 每個樹系只有一個組態命名內容。 在多樹系 Active Directory 組態中，包含已加入網域的電腦的所有樹系中必須有 hello 服務連接點。

您可以使用 hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello 設定命名內容的樹系。  

Hello Active Directory 網域名稱與為樹系*fabrikam.com*，hello 設定命名內容為：

`CN=Configuration,DC=fabrikam,DC=com`

在您的樹系中 hello 自動登錄的裝置已加入網域的 hello SCP 物件位於：  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

根據您如何部署 Azure AD Connect，hello SCP 物件可能已設定。
您可以確認 hello hello 物件存在，以及擷取使用下列 Windows PowerShell 指令碼的 hello hello 探索值： 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

hello **$scp。關鍵字**輸出會顯示 hello Azure AD 租用戶的資訊，例如：

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

如果 hello 服務連接點不存在，可以建立執行 hello`Initialize-ADSyncDomainJoinedComputerSync`您 Azure AD Connect 的伺服器上的 cmdlet。 企業系統管理員認證是必要的 toorun 這個指令程式。  
hello cmdlet:

- 建立 hello 連接到 Azure AD Connect 的 Active Directory 樹系中的 hello 服務連接點。 
- 您需要 toospecify hello`AdConnectorAccount`參數。 這是設定為 Active Directory 連接器帳戶，在 Azure AD 中的連接的 hello 帳戶。 


hello 下列指令碼範例示範使用 hello cmdlet。 此指令碼，在`$aadAdminCred = Get-Credential`需要您 tootype 使用者名稱。 您需要在 hello 使用者主要名稱 (UPN) 格式的 tooprovide hello 使用者名稱 (`user@example.com`)。 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- 使用 hello Active Directory PowerShell 模組，而這需依賴 Active Directory Web 服務的網域控制站上執行。 執行 Windows Server 2008 R2 和更新版本的網域控制站可支援 Active Directory Web 服務。
- 只支援 hello **MSOnline PowerShell 模組版本 1.1.166.0**。 toodownload 這個模組中使用這個[連結](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)。   

執行 Windows Server 2008 或更早版本的網域控制站，使用下列 toocreate hello 服務連接點的 hello 指令碼。

在多樹系組態中，您應該使用下列指令碼 toocreate hello 服務連接點電腦所在的每個樹系中的 hello:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>步驟 2︰設定宣告的發行

在同盟的 Azure AD 設定裝置依賴 Active Directory Federation Services (AD FS)，或第 3 個合作對象在內部部署同盟服務 tooauthenticate tooAzure AD。 裝置驗證 tooget 存取語彙基元 tooregister 針對 hello Azure Active Directory 裝置註冊服務 (Azure DRS)。

使用整合式 Windows 驗證 tooan active Ws-trust （1.3 或 2005年版） 裝載端點 hello 內部 federation service 進行驗證的目前裝置的 Windows。

> [!NOTE]
> 使用 AD FS 時，必須啟用 **adfs/services/trust/13/windowstransport** 或 **adfs/services/trust/2005/windowstransport**。 如果您使用 hello Web 驗證 Proxy，也請確定此端點會透過 hello proxy 發佈。 您可以看到哪些端點會透過 hello AD FS 管理主控台的 啟用**服務 > 端點**。
>
>如果您沒有為您在內部部署的 federation service AD FS，請依照 您確定它們支援 Ws-trust 1.3 或 2005年端點，這些會發佈到 hello 的檔案中繼資料交換 (MEX) 的廠商 toomake hello 指示進行。

hello 下列宣告必須存在於 Azure DRS 的裝置註冊 toocomplete 收到 hello 語彙基元。 Azure DRS 會在某些這項資訊接著 hello 電腦帳戶在內部部署與 Azure AD Connect tooassociate hello 新建立的裝置物件所使用的 Azure AD 中建立裝置物件。

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

如果您有多個已驗證的網域名稱，您需要下列宣告電腦的 tooprovide hello:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

如果您已發行的 ImmutableID 的宣告 （例如，替代登入識別碼） 會需要 tooprovide 一個對應的宣告的電腦：

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

在 hello 下列各節，尋找的相關資訊：
 
- 每個宣告應該有 hello 值
- 定義在 AD FS 中看起來如何

hello 定義可協助您 tooverify hello 值是否存在，或如果您需要 toocreate 它們。

> [!NOTE]
> 如果您不使用 AD FS 進行您在內部部署的同盟伺服器，請遵循廠商的指示 toocreate hello 適當的組態 tooissue 這些宣告。

### <a name="issue-account-type-claim"></a>發出帳戶類型宣告

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-此宣告必須包含值為**DJ**，其可識別 hello 裝置做為已加入網域的電腦。 在 AD FS 中，您可以新增發行轉換規則，如下所示︰

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>發出 objectGUID hello 電腦帳戶在內部

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-此宣告必須包含 hello **objectGUID** hello 的值在內部部署電腦帳戶。 在 AD FS 中，您可以新增發行轉換規則，如下所示︰

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>發出 hello 電腦帳戶在內部的 objectSID

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-此宣告必須包含 hello hello **objectSid** hello 的值在內部部署電腦帳戶。 在 AD FS 中，您可以新增發行轉換規則，如下所示︰

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>當 Azure AD 中有多個經過驗證的網域名稱時，發出電腦的 issuerID

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-此宣告必須包含的 hello 任何 hello 的統一資源識別元 (URI) 驗證網域名稱與 hello 連接內部部署同盟服務 （AD FS 或第 3 個合作對象） 發行 hello 語彙基元。 在 AD FS 中，您可以加入發行轉換規則看起來像是 hello 的下方之後, 的特定順序 hello 的上方。 請使用者為必要，注意，一個 tooexplicitly 問題 hello 規則。 在下列 hello 規則，會加入第一個規則，用來識別使用者與電腦驗證。

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


在上述的 hello 宣告

- `$<domain>`hello AD FS 服務 url
- `<verified-domain-name>`是您需要使用其中一個已驗證的網域名稱 tooreplace 在 Azure AD 中的預留位置



如需有關驗證的網域名稱的詳細資訊，請參閱[新增自訂網域名稱 tooAzure Active Directory](active-directory-add-domain.md)。  
tooget 已驗證的公司網域的清單，您可以使用 hello [Get-msoldomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet。 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>當使用者存在 ImmutableID (例如已設定替代登入識別碼) 時，請發出電腦的 ImmutableID

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - 此宣告必須包含電腦的有效值。 在 AD FS 中，您可以新增發行轉換規則，如下所示︰

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>協助程式指令碼 toocreate hello AD FS 發行轉換規則

hello 下列指令碼可協助您建立 hello hello 發行轉換規則上面所述。

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>備註 

- 此指令碼會附加 hello 規則 toohello 現有規則。 不會執行 hello 指令碼兩次，因為 hello 設定的規則將會新增兩次。 請確定沒有對應的規則存在這些宣告 （hello 對應在情況下），才能再次執行 hello 指令碼。

- 如果您有多個已驗證的網域名稱 （如所示 hello Azure AD 入口網站或透過 hello Get MsolDomains cmdlet），來設定 hello 值**$multipleVerifiedDomainNames** hello 中編寫的指令碼太**$true**。 此外，也務必移除經由 Azure AD Connect 或透過其他方式所建立的任何現有 issuerid 宣告。 此規則的範例如下︰


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- 如果您已經發出**ImmutableID**宣告的使用者帳戶，來設定 hello 值**$immutableIDAlreadyIssuedforUsers** hello 中編寫的指令碼太**$true**。

## <a name="step-3-enable-windows-down-level-devices"></a>步驟 3：啟用舊版 Windows 裝置

如果有些已加入網域的裝置是舊版 Windows 裝置，您需要︰

- 在 Azure AD tooenable 使用者 tooregister 裝置設定的原則。
 
- 設定您在內部部署同盟服務 tooissue 宣告 toosupport**整合式 Windows 驗證 (IWA)**註冊的裝置。
 
- 新增 hello Azure AD 裝置驗證端點 toohello 本機內部網路區域驗證 hello 裝置時，會提示 tooavoid 憑證。

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>在 Azure AD tooenable 中使用者 tooregister 裝置設定原則

tooregister Windows 下層裝置，您需要確定已設定該設定 tooallow 使用者 tooregister 裝置在 Azure AD 中的 hello toomake。 在 hello Azure 入口網站，您可以找到此設定下：

`Azure Active Directory > Users and groups > Device settings`
    
hello 下列原則必須設定太**所有**:**使用者可以向 Azure AD 註冊其裝置**

![註冊裝置](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>設定內部部署同盟服務 

您在內部部署的同盟服務必須支援發行 hello **authenticationmehod**和**wiaormultiauthn**宣告時收到的驗證要求保留 toohello Azure AD 信賴憑證者合作對象resouce_params 參數編碼值，以顯示下列：

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

這類要求時，hello 內部同盟服務必須驗證 hello 使用者使用整合式 Windows 驗證，並成功時，它必須發出下列兩個宣告的 hello:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

在 AD FS 中，您必須加入該階段透過 hello 驗證方法的發行轉換規則。  

**tooadd 此規則：**

1. 在 hello AD FS 管理主控台中，移過`AD FS > Trust Relationships > Relying Party Trusts`。
2. Hello Microsoft Office 365 識別平台信賴憑證者信任物件，以滑鼠右鍵按一下，然後選取**編輯宣告規則**。
3. 在 hello**發行轉換規則**索引標籤上，選取**加入規則**。
4. 在 hello**宣告規則**範本清單中，選取**使用自訂規則傳送宣告**。
5. 選取 [下一步] 。
6. 在 hello**宣告規則名稱**方塊中，輸入**驗證方法宣告規則**。
7. 在 [hello**宣告規則**] 方塊中，下列規則類型 hello:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. 在同盟伺服器上，輸入下面的 hello PowerShell 命令來取代之後 **\<RPObjectName\>** 與 hello 信賴憑證者合作對象的物件名稱您 Azure AD 信賴憑證者信任物件。 此物件通常名為「Microsoft Office 365 身分識別平台」。
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>新增 hello Azure AD 裝置驗證端點 toohello 近端內部網路區域

註冊裝置中的使用者驗證 tooAzure 可以是您推送下列 URL toohello 近端內部網路區域，在 Internet Explorer 原則 tooyour 已加入網域裝置 tooadd hello AD 時，會提示 tooavoid 憑證：

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>步驟 4︰控制部署與導入

當您完成 hello 所需的步驟時，加入網域的裝置會準備 tooautomatically 向 Azure AD。 所有已加入網域且執行 Windows 10 年度更新版和 Windows Server 2016 的裝置會在裝置重新啟動或使用者登入時自動向 Azure AD 註冊。 Hello 網域聯結作業執行完成之後 hello 裝置將重新啟動時的 Azure AD 中註冊新裝置。

過了先前的工作地方聯結 tooAzure AD （例如針對 Intune) 轉換的裝置 」*已加入網域，AAD 已登錄*"; 不過花一些時間的這個程序 toocomplete 到期 toohello 標準的所有裝置上網域和使用者活動流程。

### <a name="remarks"></a>備註

- 您可以使用群組原則物件 toocontrol hello 首度發行的 Windows 10 和 Windows Server 2016 網域的電腦自動註冊。

- Windows 10 11 月版 2015年更新自動暫存器與 Azure AD**只**如果 hello 首度發行的群組原則物件設定。

- 您可以部署 toorollout hello 自動註冊的 Windows 下層電腦[Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)toocomputers 您選取。

- 如果您推送 hello 群組原則物件 tooWindows 8.1 已加入網域的裝置，就會嘗試註冊;不過最好是您使用 hello [Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)tooregister 所有 Windows 下層裝置。 

### <a name="create-a-group-policy-object"></a>建立群組原則物件 

toocontrol hello 首度發行目前的 Windows 電腦的自動註冊，您應該部署 hello**做為裝置註冊加入網域的電腦**想 tooregister 的群組原則物件 toohello 裝置。 例如，您可以部署 hello 原則 tooan 組織單位或 tooa 安全性群組。

**tooset hello 原則：**

1. 開啟**伺服器管理員**，然後前往太`Tools > Group Policy Management`。
2. 請移至 toohello 網域節點對應 toohello 想 tooactivate 自動登錄，目前的 Windows 電腦的網域。
3. 在 [群組原則物件] 上按一下滑鼠右鍵，然後選取 [新增]。
4. 輸入群組原則物件的名稱。 例如，*自動註冊 tooAzure AD*。 選取 [確定] 。
5. 以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯]。
6. 跳過**電腦設定** > **原則** > **系統管理範本** > **Windows元件** > **裝置註冊**。 以滑鼠右鍵按一下 [將已加入網域的電腦註冊為裝置]，然後選取 [編輯]。
   
   > [!NOTE]
   > 此群組原則範本已從舊版的 hello 群組原則管理主控台中重新命名。 如果您使用舊版的 hello 主控台，請移至太`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`。 

7. 選取 [已啟用]，然後選取 [套用]。
8. 選取 [確定] 。
9. 連結 hello 群組原則物件 tooa 您選擇的位置。 例如，您可以將它連結 tooa 特定組織單位。 您也可以將它連結 tooa 特定安全性群自動向 Azure AD 的電腦。 tooset 此原則中的所有已加入網域的 Windows 10 和 Windows Server 2016 電腦組織連結 hello 群組原則物件 toohello 網域。

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>非 Windows 10 電腦的 Windows Installer 套件

tooregister 加入網域的 Windows 下層電腦在同盟環境中，您可以下載並安裝從下載中心取得這些 Windows Installer 套件 (.msi)，在 hello[非 Windows 10 電腦的Microsoft工作地方聯結](https://www.microsoft.com/en-us/download/details.aspx?id=53554)頁面。

您可以使用軟體分派系統像 System Center Configuration Manager 部署 hello 封裝。 hello 封裝支援 hello 標準的無訊息安裝選項以 hello*安靜*參數。 System Center Configuration Manager 最新分支會提供額外的好處，從較早的版本，例如 hello 能力 tootrack 完成註冊。 如需詳細資訊，請參閱 [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)。

hello installer hello hello 使用者內容中執行的系統上建立排定的工作。 hello 使用者登入時 tooWindows 觸發 hello 工作。 hello 工作以無訊息方式註冊 hello 裝置與 Azure AD 與 hello 使用者認證驗證使用整合式 Windows 驗證之後。 toosee hello 排程的工作，請在 hello 裝置跳過**Microsoft** > **工作地點加入**，並前往 toohello 工作排程器程式庫。

## <a name="step-5-verify-registered-devices"></a>步驟 5︰驗證已註冊的裝置

您也可以使用 hello 您組織中查看已註冊的裝置成功[Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)指令程式在 hello [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0)。

此 cmdlet 的 hello 輸出會顯示在 Azure AD 中註冊的裝置。 tooget 所有裝置，都使用 hello **-所有**參數，然後再篩選它們使用 hello **deviceTrustType**屬性。 已加入網域的裝置具有**已加入網域**這個值。

## <a name="next-steps"></a>後續步驟

* [自動裝置註冊常見問題集](active-directory-device-registration-faq.md)
* [疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [疑難排解自動登錄的網域加入電腦 tooAzure AD – 非 Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
