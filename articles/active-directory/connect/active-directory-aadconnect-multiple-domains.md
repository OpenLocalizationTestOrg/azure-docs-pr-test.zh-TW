---
title: "aaaAzure AD 連接多個網域"
description: "本文件說明如何使用 O365 與 Azure AD 安裝及設定多個最上層網域。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>與 Azure AD 同盟的多網域支援
hello 下列文件指引如何 toouse 多個最上層網域和子網域時將與 Office 365 或 Azure AD 網域加入同盟。

## <a name="multiple-top-level-domain-support"></a>多個最上層網域支援
若要讓多個最上層網域與 Azure AD 同盟，您需要一些讓單一最上層網域同盟時不需要的額外組態。

當使用 Azure AD 同盟網域時，在 Azure 中的 hello 網域會設定數個屬性。  其中一個重要屬性是 IssuerUri。  這是 URI，會使用 Azure AD tooidentify hello 語彙基元的 hello 網域是與相關聯。  hello URI 不需要 tooresolve tooanything，但它必須是有效的 URI。  根據預設，Azure AD 設定此 toohello hello federation service 識別碼中值您內部部署 AD FS 組態。

> [!NOTE]
> hello federation service 識別碼是可唯一識別同盟服務的 URI。  hello federation service 是 AD FS 該函式的執行個體，為 hello 安全性權杖服務。 
> 
> 

您可以使用 hello PowerShell 命令檢視 IssuerUri `Get-MsolDomainFederationSettings -DomainName <your domain>`。

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

當我們想 tooadd 最上層的網域不止一個，就會發生問題。  例如，假設您已設定 Azure AD 和內部部署環境之間的同盟。  在本文中我使用 bmcontoso.com。現在我已加入第二個最上層網域 bmfabrikam.com。

![網域](./media/active-directory-multiple-domains/domains.png)

當我們嘗試的 tooconvert 我們 bmfabrikam.com 網域 toobe 同盟時，我們會收到錯誤。  hello 原因是，Azure AD 包含不允許 hello IssuerUri 屬性 toohave hello 相同值的多個網域的條件約束。  

![同盟錯誤](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>SupportMultipleDomain 參數
tooworkaround，我們需要能夠使用 hello 完成不同 IssuerUri tooadd`-SupportMultipleDomain`參數。  這個參數會搭配 hello 下列 cmdlet:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

這個參數可讓 Azure AD 設定 hello IssuerUri，讓它基礎 hello hello 網域名稱。  它將會成為 Azure AD 中所有目錄的唯一項目。  使用 hello 參數允許 hello PowerShell 命令 toocomplete 成功。

![同盟錯誤](./media/active-directory-multiple-domains/convert.png)

看看我們新 bmfabrikam.com 網域的 hello 設定，可以看到 hello 下列：

![同盟錯誤](./media/active-directory-multiple-domains/settings.png)

請注意，`-SupportMultipleDomain`不會變更 hello adfs.bmcontoso.com 上其他端點，也就是仍設定的 toopoint tooour 同盟服務。

另一項，`-SupportMultipleDomain`沒有可確保 hello AD FS 系統將 hello 正確的簽發者值包含在 Azure ad 簽發的權杖中。 它會 hello 網域一部分 hello 使用者 UPN，以及將此設定為在 hello IssuerUri，也就是 https://{upn 尾碼 hello 網域} / adfs/services/信任。 

因此在驗證 tooAzure AD 或 Office 365 時，hello 使用者的權杖中的 hello IssuerUri 項目會是在 Azure AD 中使用的 toolocate hello 網域。  如果相符項目找不到 hello 驗證將會失敗。 

例如，如果使用者的 UPN 是bsimon@bmcontoso.com，toohttp://bmcontoso.com/adfs/services/trust 會集中 hello 語彙基元的 AD FS 問題的 hello IssuerUri 項目。 這會符合 hello Azure AD 組態，並驗證將會成功。

hello 下面是 hello 實作此邏輯的自訂的宣告規則：

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> 在順序 toouse hello-SupportMultipleDomain 切換嘗試 tooadd 新時，或轉換已加入網域，您需要 toohave 設定同盟的信任 toosupport 它們原本。  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Tooupdate hello 信任 AD FS 與 Azure AD 之間的方式
如果您並未設定 AD FS 與 Azure AD 執行個體之間的 hello 同盟信任，您可能需要 toore-建立信任。  這是因為時最初設定，而不 hello`-SupportMultipleDomain`參數，hello IssuerUri 設 hello 預設值。  在 hello 低於您的螢幕擷取畫面可以看到 hello IssuerUri 設定 toohttps://adfs.bmcontoso.com/adfs/services/trust。

因此現在，如果我們已成功地在 hello Azure AD 入口網站中加入新的網域，然後嘗試 tooconvert 使用`Convert-MsolDomaintoFederated -DomainName <your domain>`，得到下列錯誤 hello。

![同盟錯誤](./media/active-directory-multiple-domains/trust1.png)

如果您嘗試 tooadd hello`-SupportMultipleDomain`交換器我們將會收到下列錯誤 hello:

![同盟錯誤](./media/active-directory-multiple-domains/trust2.png)

只嘗試 toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello 上原始網域也會導致錯誤。

![同盟錯誤](./media/active-directory-multiple-domains/trust3.png)

使用下列 tooadd 額外的最上層網域的 hello 步驟。  如果您已加入網域並不是使用 hello`-SupportMultipleDomain`參數開頭 hello 移除和更新您的原始網域的步驟。  如果您尚未新增最上層網域尚未就可以開始新增網域，使用 PowerShell 的 Azure AD Connect 的 hello 步驟。

使用下列步驟 tooremove hello Microsoft Online 信任 hello，並更新您的原始網域。

1. 在 AD FS 同盟伺服器上，開啟 [AD FS 管理]  
2. Hello 左側展開**信任關係**和**信賴憑證者信任**
3. 在右邊的 hello，刪除 hello **Microsoft Office 365 識別平台**項目。
   ![移除 Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. 已在機器上[Azure Active Directory 的 Windows PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)上面執行 hello 下列安裝： `$cred=Get-Credential`。  
5. 輸入您正在同盟與 hello Azure AD 網域 hello 使用者名稱和密碼的全域管理員
6. 在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`
7. 在 PowerShell 中輸入 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`。  這是 hello 原始網域。  上述網域會使用 hello:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

使用下列步驟 tooadd hello 新增最上層網域使用 PowerShell 的 hello

1. 已在機器上[Azure Active Directory 的 Windows PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)上面執行 hello 下列安裝： `$cred=Get-Credential`。  
2. 輸入您正在同盟與 hello Azure AD 網域 hello 使用者名稱和密碼的全域管理員
3. 在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`
4. 在 PowerShell 中輸入 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

使用下列步驟 tooadd hello 新增最上層網域使用 Azure AD Connect 的 hello。

1. 啟動 Azure AD Connect 從 hello 桌面或 [開始] 功能表
2. 選擇 [新增其他 Azure AD 網域] ![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add1.png)
3. 輸入您的 Azure AD 和 Active Directory 認證
4. 選取您想為同盟 tooconfigure hello 第二個網域。
   ![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add2.png)
5. 按一下 [安裝]

### <a name="verify-hello-new-top-level-domain"></a>確認 hello 新增最上層網域
使用 hello PowerShell 命令`Get-MsolDomainFederationSettings -DomainName <your domain>`您可以檢視 hello 更新 IssuerUri。  hello 以下螢幕擷取畫面顯示 hello 同盟設定在我們的原始網域 http://bmcontoso.com/adfs/services/trust 更新

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

而且 hello IssuerUri 我們新的網域上已設定 toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>子網域的支援
當您新增子網域時，由於 hello 方式 Azure AD 會處理網域，它會繼承 hello hello 父項設定。  這表示該 hello IssuerUri 需要 toomatch hello 父代。

因此，假設我有 bmcontoso.com，後來再加入 corp.bmcontoso.com。這表示該 hello IssuerUri corp.bmcontoso.com 的使用者將需要 toobe **http://bmcontoso.com/adfs/services/trust。**  Azure AD 實作上述 hello 標準規則，但是會產生為簽發者的語彙基元**http://corp.bmcontoso.com/adfs/services/trust。** 這不會符合 hello 網域的必要的值，驗證將會失敗。

### <a name="how-tooenable-support-for-sub-domains"></a>Tooenable 支援子網域的方式
這個 hello 周圍的順序 toowork 中 AD FS 信賴憑證者信任的 Microsoft Online 需要 toobe 更新。  toodo，您必須設定自訂宣告規則，使它剝 hello 使用者的 UPN 尾碼從任何子網域時建構 hello 自訂簽發者值。 

hello 下列宣告會這樣做：

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
hello hello 規則運算式中的最後一個號碼設定 hello 多少沒有根網域中的父網域。 此處我所擁有的是 bmcontoso.com，因此必須有 2 個父網域。 如果三個父網域已保留 toobe (也就是： corp.bmcontoso.com)，然後 hello 數目已經三個。 可看出 Eventualy 範圍、 hello 相符項目一律都會 toomatch hello 的定義域的最大值。 "{2，3}"會比對兩個 toothree 網域 (也就是： bmfabrikam.com 和 corp.bmcontoso.com)。

使用下列步驟 tooadd hello 自訂宣告 toosupport 子網域。

1. 開啟 [AD FS 管理]
2. 以滑鼠右鍵按一下 hello Microsoft 線上 RP trust，然後選擇 編輯宣告規則
3. 選取 hello 第三個宣告規則，並取代![宣告編輯](./media/active-directory-multiple-domains/sub1.png)
4. 取代 hello 目前宣告：
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![取代宣告](./media/active-directory-multiple-domains/sub2.png)

5. 按一下 [確定]。  按一下 [套用]。  按一下 [確定]。  關閉 [AD FS 管理]。

