---
title: "aaaUse 現有 NPS 伺服器 tooprovide Azure MFA 功能 |Microsoft 文件"
description: "hello Azure 多重要素驗證的網路原則伺服器延伸模組是簡單的解決方案 tooadd 以雲端為基礎的兩個步驟 vericiation 功能 tooyour 現有驗證基礎結構。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>將現有的 NPS 基礎結構與 Azure Multi-Factor Authentication 整合

hello Azure MFA 的網路原則伺服器 (NPS) 擴充功能新增雲端式 MFA 功能 tooyour 驗證基礎結構使用您現有的伺服器。 以 hello NPS 擴充功能，您可以加入通話、 簡訊或電話應用程式驗證 tooyour 現有的驗證流程，而不需要 tooinstall 設定及維護新的伺服器。 

公司想 tooprotect VPN 連線，但不部署 hello Azure MFA Server 建立此延伸模組。 hello NPS 擴充做為 RADIUS 和以雲端為基礎的 Azure MFA tooprovide 之間配接器的第二個因素，同盟或已同步使用者的驗證。

使用 Azure MFA hello NPS 延伸模組時, hello 驗證流程包括下列元件的 hello: 

1. **NAS/VPN 伺服器**來自 VPN 用戶端收到要求，並將它們轉換成要求 tooNPS 的 RADIUS 伺服器。 
2. **NPS 伺服器**連接 tooActive 目錄 tooperform hello 的主要驗證 hello RADIUS 會要求，並成功時，會傳遞 hello 要求 tooany 安裝擴充功能。  
3. **NPS 擴充**hello 次要驗證的要求 tooAzure MFA 觸發程序。 一旦 hello 延伸模組接收到 hello 回應和 hello MFA 挑戰成功，它會藉由提供包含 MFA 宣告，Azure STS 所發出的安全性權杖中的 hello NPS 伺服器完成 hello 驗證要求。  
4. **Azure MFA**進行通訊與 Azure Active Directory tooretrieve hello 使用者的詳細資訊，以及執行 hello 次要驗證使用的驗證方法設定 toohello 使用者。

hello 下列圖表說明此高層級的驗證要求流程： 

![驗證流程圖](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>規劃您的部署

hello NPS 擴充功能會自動處理備援性，因此您不需要特殊的設定。

您可以視需要建立數量不拘且具有 Azure MFA 功能的 NPS 伺服器。 如果您安裝多部伺服器，您應該為每部伺服器使用不同的用戶端憑證。 建立每個伺服器的憑證，意味著您可以個別更新每個憑證，無須擔心所有的伺服器皆停機。

VPN 伺服器路由傳送驗證要求，因此需要 toobe 留意 hello 新的 Azure MFA 啟用 NPS 伺服器。

## <a name="prerequisites"></a>必要條件

hello NPS 擴充功能的目的在於 toowork 與您現有的基礎結構。 請確定您擁有 hello 下列必要條件，才能開始。

### <a name="licenses"></a>授權

hello Azure MFA 的 NPS 延伸模組是與使用 toocustomers [Azure Multi-factor Authentication Server 的授權](multi-factor-authentication.md)（隨附於 Azure AD Premium、 EMS 或 MFA 訂閱）。

### <a name="software"></a>軟體

Windows Server 2008 R2 SP1 或更新版本。

### <a name="libraries"></a>程式庫

這些程式庫會自動安裝 hello 副檔名。
-   [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [適用於 Windows PowerShell 1.1.1660 版本的 Microsoft Azure Active Directory 模組](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

使用 hello NPS 延伸模組的每個人都必須是 Active Directory 的同步處理的 tooAzure 使用 Azure AD Connect，以及必須註冊 MFA。

當您安裝 hello 延伸模組時，您會需要 Azure AD 租用戶 hello 目錄識別碼和系統管理員認證。 您可以找到您目錄的識別碼在 hello [Azure 入口網站](https://portal.azure.com)。 身為管理員，選取 hello 登入**Azure Active Directory**圖示 hello 左邊，然後選取**屬性**。 複製 hello GUID 在 hello**目錄識別碼**方塊，並將其儲存。 當您安裝 hello NPS 擴充功能時，您可以使用與 hello 租用戶識別碼的此 GUID。

![在 Azure Active Directory 屬性下尋找您的目錄識別碼](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>準備您的環境

您安裝 hello NPS 擴充功能之前，您會想 tooprepare 您環境 toohandle hello 驗證流量。

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>啟用 hello 已加入網域的伺服器上的 NPS 角色

hello NPS 伺服器連接 tooAzure Active Directory，並驗證 hello MFA 要求。 為此角色選擇一部伺服器。 我們建議您選擇不會處理來自其他服務，要求的伺服器，因為 hello NPS 擴充功能會擲回的任何不是 RADIUS 要求的錯誤。

1. 在您的伺服器上開啟 [hello**新增角色及功能精靈**從 hello 伺服器管理員的快速入門] 功能表。
2. 將您的安裝類型選為 [角色型或功能型安裝]。
3. 選取 hello**網路原則與存取服務**伺服器角色。 視窗可能會快顯 tooinform 您所需的功能 toorun 此角色。
4. 繼續透過 hello 精靈 hello 確認頁面。 選取 [安裝]。

既然您已指定給 NPS 伺服器，您也應該設定此伺服器 toohandle hello VPN 解決方案從連入 RADIUS 要求。

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>設定您的 VPN 解決方案 toocommunicate 與 hello NPS 伺服器

根據您使用的 VPN 解決方案，hello 步驟 tooconfigure RADIUS 驗證原則而有所不同。 設定此原則 toopoint tooyour NPS RADIUS 伺服器。

### <a name="sync-domain-users-toohello-cloud"></a>同步處理網域使用者 toohello 雲端

一定已在您的租用戶上完成此步驟，但它是，Azure AD Connect 同步處理您的資料庫最近良好 toodouble 檢查。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 選取 [Azure Active Directory]  >  [Azure AD Connect]
3. 確認同步處理狀態為 [已啟用]，且上次同步處理為不到一小時前。

如果您需要關閉同步處理新回合 tookick，我們 hello 中的指示[Azure AD Connect 同步： 排程器](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler)。

### <a name="determine-which-authentication-methods-your-users-can-use"></a>判斷您的使用者可以使用的驗證方法

有兩個因素會影響與 NPS 擴充部署搭配提供的驗證方法：

1. hello hello RADIUS 用戶端之間使用的密碼加密演算法 (VPN、 Netscaler 伺服器或其他) 與 hello NPS 伺服器。
   - **PAP** hello 定域機組中支援的 Azure MFA 的所有 hello 驗證方法： 通話、 單向簡訊、 行動裝置應用程式通知和行動裝置應用程式的驗證碼。
   - **CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知。
2. hello 輸入 hello 用戶端應用程式的方法 (VPN、 Netscaler 伺服器或其他) 可以處理。 Hello VPN 用戶端比方說，有一些方法 tooallow hello 使用者 tootype 文字或行動裝置應用程式的驗證程式碼中？

當您部署的 hello NPS 擴充功能時，使用這些方法可供您使用者的因素 tooevaluate。 如果您的 RADIUS 用戶端支援 PAP，但 hello 用戶端 UX 沒有驗證程式碼的輸入的欄位，然後電話和行動裝置應用程式通知 hello 兩個支援的選項。

您可以在 Azure 中[停用不受支援的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。

### <a name="enable-users-for-mfa"></a>針對 MFA 啟用使用者

部署 hello 完整 NPS 擴充功能之前，您需要 tooenable MFA hello 想 tooperform 雙步驟驗證的使用者。 更立即 tootest hello 延伸模組，當您將它部署，您必須至少一個測試帳戶完全註冊多重要素驗證。

使用測試帳戶啟動這些步驟 tooget:
1. 登入太[https://aka.ms/mfasetup](https://aka.ms/mfasetup)測試帳戶。 
2. 請遵循 hello 提示 tooset 驗證方法。
3. 建立條件式存取原則或[變更 hello 使用者狀態](multi-factor-authentication-get-started-user-states.md)toorequire hello 測試帳戶的雙步驟驗證。 

您的使用者也需要 toofollow 這些步驟 tooenroll 之前它們向 hello NPS 擴充功能。

## <a name="install-hello-nps-extension"></a>安裝 hello NPS 擴充功能

> [!IMPORTANT]
> 不同於 hello VPN 存取點的伺服器上安裝 hello NPS 擴充功能。

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>下載並安裝 Azure MFA hello NPS 延伸模組

1.  [下載 hello NPS 擴充](https://aka.ms/npsmfa)從 Microsoft 下載中心 hello。
2.  將複製 hello 二進位 toohello 想 tooconfigure 網路原則伺服器。
3.  執行*setup.exe*依照 hello 安裝指示。 如果您遇到錯誤，請仔細檢查該 hello hello 必要條件 > 一節中的兩個程式庫已成功安裝。

### <a name="run-hello-powershell-script"></a>執行 hello PowerShell 指令碼

hello 安裝程式會在這個位置建立 PowerShell 指令碼： `C:\Program Files\Microsoft\AzureMfa\Config` （其中 C:\ 是安裝磁碟機）。 這個 PowerShell 指令碼會執行下列動作的 hello:

-   建立自我簽署憑證。
-   建立 hello 公開金鑰的 hello 憑證 toohello 服務主體上 Azure AD 的關聯。
-   存放區 hello hello 本機電腦憑證存放區中的憑證。
-   授與存取 toohello 憑證的私用的索引鍵 tooNetwork 使用者。
-   重新啟動 hello NPS。

除非您想 toouse 自己憑證 （而不是 hello 的自我簽署憑證 hello 的 PowerShell 指令碼會產生），執行 PowerShell 指令碼 hello toocomplete hello 安裝程式。 如果您在多部伺服器上安裝 hello 延伸模組，每一個應該有它自己的憑證。

1. 以系統管理理員身分執行 Windows PowerShell。
2. 變更目錄。

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. 執行 hello hello 安裝程式所建立的 PowerShell 指令碼。

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell 會提示您輸入您的租用戶識別碼。 使用 hello 從 hello hello 必要條件 > 一節中的 Azure 入口網站複製的目錄識別碼 GUID。
5. 登入 tooAzure AD 系統管理員身分。
6. Hello 指令碼完成時，PowerShell 會顯示成功訊息。  

重複上述步驟，在您想要進行負載平衡 tooset 任何其他 NPS 伺服器上。

>[!NOTE]
>如果您使用您自己的憑證，而非產生憑證以 hello PowerShell 指令碼，請確定它們對齊 toohello NPS 命名慣例。 hello 主旨名稱必須是**CN =\<TenantID\>，OU = Microsoft NPS 擴充功能**。 

## <a name="configure-your-nps-extension"></a>設定 NPS 擴充功能

本節包含成功部署 NPS 擴充功能的設計考量和建議。

### <a name="configuration-limitations"></a>設定限制

- hello Azure MFA 的 NPS 擴充功能不包含工具 toomigrate 使用者和從 MFA Server toohello 雲端的設定。 基於這個理由，我們建議使用新的部署，而不是現有部署的 hello 延伸模組。 如果您使用現有部署的 hello 延伸模組，您的使用者具有 tooperform 證明總再次 toopopulate 他們 MFA 詳細說明 hello 雲端中。  
- hello NPS 擴充功能會使用的 hello UPN hello 從內部部署 Active directory tooidentify hello Azure MFA 上執行 hello 次要驗證 hello 延伸模組可以使用者設定的 toouse 不同的識別項，例如識別碼或自訂的 Active Directory 的替代登入UPN 以外的欄位。 請參閱[進階組態選項的 hello NPS 擴充功能的多重要素驗證](multi-factor-authentication-advanced-vpn-configurations.md)如需詳細資訊。
- 並非所有的加密通訊協定都支援所有的驗證方法。
   - **PAP** 支援通話、單向簡訊、行動裝置應用程式通知和行動裝置應用程式驗證碼
   - **CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知

### <a name="control-radius-clients-that-require-mfa"></a>控制需要 MFA 的 RADIUS 用戶端

一旦您啟用 MFA 的 RADIUS 用戶端使用 hello NPS 擴充功能時，所有的用戶端驗證是必要的 tooperform MFA。 如果您想要 tooenable MFA 某些 RADIUS 用戶端而非其他電腦，則可以設定兩部 NPS 伺服器，並在其中只有一個元件上安裝 hello 延伸模組。 設定您想要 toorequire MFA toosend 要求 toohello NPS 伺服器 hello 延伸模組，以設定和副檔名 hello 未設定其他 RADIUS 用戶端 toohello NPS 伺服器的 RADIUS 用戶端。

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>針對未註冊 MFA 的使用者做準備

如果您未註冊為 MFA 的使用者，您可以決定當他們嘗試 tooauthenticate 時，會發生什麼事。 使用 hello 登錄設定*REQUIRE_USER_MATCH* hello 登錄路徑中*HKLM\Software\Microsoft\AzureMFA* toocontrol hello 功能的行為。 此設定具有單一組態選項︰

| 索引鍵 | 值 | 預設值 |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | 未設定 (對等 tooTRUE) |

hello 此設定的目的是 toodetermine 哪些 toodo，當使用者未註冊為 MFA。 當 hello 索引鍵不存在、 未設定，或設 tooTRUE，hello 使用者未註冊，然後 hello 延伸失敗 hello MFA 挑戰。 當 hello 機碼設定 tooFALSE hello 使用者註冊，而不需執行 MFA 就會繼續驗證。

您可以選擇 toocreate 這個機碼，然後將它設定 tooFALSE，雖然您的使用者是登入，且可能不是所有註冊的 Azure MFA 尚未。 不過，因為設定 hello 索引鍵允許的 MFA toosign 中未註冊的使用者，您應該移除之前進行 tooproduction 這個機碼。

## <a name="troubleshooting"></a>疑難排解

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>如何確認該 hello 用戶端憑證已安裝，如預期般？

尋找 hello hello hello 憑證存放區和 hello 私密金鑰的核取中的安裝程式所建立的自我簽署的憑證具有權限授與 toouser **NETWORK SERVICE**。 hello 憑證的主體名稱的**CN \<tenantid\>，OU = Microsoft NPS 擴充功能**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>如何確認我的用戶端憑證是在 Azure Active Directory 中的相關聯的 toomy 租用戶？

開啟 PowerShell 命令提示字元並執行下列命令的 hello:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

這些命令會列印所有租用戶關聯 hello NPS 擴充功能的執行個體，您的 PowerShell 工作階段中的 hello 憑證。 尋找您的憑證將用戶端憑證匯出為具 hello 私密金鑰 [Base 64 編碼 X.509(.cer)] 檔案，並與從 PowerShell hello 清單比較。

有效-從且有效的時間戳記，也就是人類看得懂的格式，可以為使用的 toofilter 明顯 misfits 出，如果 hello 命令會傳回一個以上的憑證之前。

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>為何要求會失敗並出現 ADAL 權杖錯誤？

這個錯誤可能是因為 tooone 多種原因所造成。 使用下列 toohelp 疑難排解的步驟：

1. 重新啟動 NPS 伺服器。
2. 確認已如預期安裝用戶端憑證。
3. 請確認該 hello 憑證與您的租用戶相關聯的 Azure AD。
4. 請確認該 https://login.microsoftonline.com/ 可從執行 hello 延伸模組的 hello 伺服器存取。

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>驗證為何失敗，發生錯誤，指出找不到該 hello 使用者 HTTP 記錄檔中？

確認 AD Connect 正在執行，且該 hello 使用者存在於 Windows Active Directory 與 Azure Active Directory 中。

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>為何我會在記錄中看到 HTTP 連線錯誤，且我的所有驗證都失敗？

請確認該 https://adnotifications.windowsazure.com 可從執行 hello NPS 延伸模組的 hello 伺服器存取。


## <a name="next-steps"></a>後續步驟

- 設定替代識別碼登入，或不應該執行中的雙步驟驗證的 ip 設定的例外狀況清單[進階組態選項的 hello NPS 擴充功能的多重要素驗證](nps-extension-advanced-configuration.md)

- [針對 Azure Multi-factor Authentication 解決 hello NPS 擴充功能中的錯誤訊息](multi-factor-authentication-nps-errors.md)
