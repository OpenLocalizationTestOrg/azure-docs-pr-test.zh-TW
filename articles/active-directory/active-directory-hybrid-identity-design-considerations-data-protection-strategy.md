---
title: "aaaAzure Active Directory 混合式身分識別設計考量-定義的資料保護策略 |Microsoft 文件"
description: "您將定義 hello 資料保護策略的混合式身分識別方案 toomeet hello 商務需求所定義。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>定義混合式身分識別解決方案的資料保護策略
在這項工作，您將定義的混合式身分識別方案 toomeet hello 商務需求所定義中的 hello 資料保護策略：

* [判斷資料保護需求](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [判斷內容管理需求](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [判斷存取控制需求](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [判斷事件因應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>定義資料保護選項
如 [判斷目錄同步處理需求](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)中所述，Microsoft Azure AD 可以與您內部部署的 Active Directory 網域服務 (AD DS) 同步處理。 當他們嘗試 tooaccess 公司資源時，這項整合可讓組織 tooleverage Azure AD tooverify 使用者的認證。 這可以在兩個案例： 在其他內部部署和 hello 雲端中的資料。  在 Azure AD 中的存取 toodata 需要使用者透過安全性權杖服務 (STS) 進行驗證。

一旦經過驗證，hello 使用者主要名稱 (UPN) 從讀取 hello 驗證權杖，hello 複寫資料分割和容器對應會決定 toohello 使用者的網域。 Hello 授權系統 toodetermine 是否 hello 要求的存取 toohello 目標租用戶這位使用者所需的授權此工作階段中，會使用 hello 使用者存在、 已啟用的狀態和角色的詳細資訊。 特定授權的動作 （特別是，建立使用者，密碼重設） 會建立稽核記錄，可供租用戶系統管理員 toomanage 法規或調查。

透過網際網路連接到 Azure 儲存體您在內部部署資料中心中的資料移不一定永遠可行因 toodata 磁碟區、 頻寬可用性或其他考量。 hello [Azure 儲存體匯入/匯出服務](../storage/common/storage-import-export-service.md)提供硬體式放置/擷取的 blob 儲存體中資料的大型磁碟區選項。 它可讓您 toosend [BitLocker 加密](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2)硬碟機直接 tooan Azure 資料中心內，雲端操作員將上傳 hello 內容 tooyour 儲存體帳戶，或他們可以下載 Azure 資料 tooyour 磁碟機 tooreturntooyou。 只加密的磁碟會接受此處理程序 （使用 hello 作業安裝期間 hello 服務本身所產生的 BitLocker 金鑰）。 hello BitLocker 金鑰 tooAzure 個別提供，因此能提供超出訊號範圍的索引鍵共用。

由於傳輸中的資料可以發生在不同的案例中，也是使用 Microsoft Azure 的相關 tooknow[虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)tooisolate 租用戶流量，採用例如主機和客體層級的量值防火牆、 IP 封包篩選，封鎖連接埠，和 HTTPS 端點。 不過，Azure 的內部通訊大多也會加密，包括基礎結構對基礎結構和基礎結構對客戶 (內部部署) 的通訊。 另一個重要的案例是在 Azure 資料中心; 中的 hello 通訊Microsoft 會管理沒有 VM 可以模擬或竊聽 hello IP 位址，另一個網路 tooassure。 存取 Azure 儲存體或 SQL 資料庫時，或在連接 tooCloud 服務時，會使用 TLS/SSL。 在此情況下，hello 客戶系統管理員負責取得 TLS/SSL 憑證，並將它部署 tootheir 租用戶基礎結構。 虛擬機器之間移動的資料流量在 hello 相同部署中或在單一部署透過 Microsoft Azure 虛擬網路的租用戶之間可以保護透過加密的通訊協定，例如 HTTPS、 SSL/TLS，或其他項目。

根據您回答中的 hello 問題的方式[決定資料保護需求](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)，您應該能夠 toodetermine 您希望 tooprotect 資料以及如何 hello 混合式身分識別解決方案將協助您根據。 hello 表格顯示 hello Azure 支援可用選項的每個資料保護案例。

| 資料保護選項 | 在 hello 雲端待用 | 在內部部署中待用 | 傳輸中 |
| --- | --- | --- | --- |
| BitLocker 磁碟機加密 |X |X | |
| SQL Server tooencrypt 資料庫 |X |X | |
| VM 對 VM 加密 | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> 讀取[依功能遵循](https://azure.microsoft.com/support/trust-center/services/)在[Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)tooknow 深入了解每個 Azure 服務是否相容的 hello 認證。
> 由於資料保護的 hello 選項使用多層方法，這些選項之間的比較則不適用這項工作。 請確定您利用所有可用的 hello 資料將會每個狀態的選項。
>
>

## <a name="define-content-management-options"></a>定義內容管理選項
使用 Azure AD toomanage 混合式身分識別基礎結構的其中一個優點是 hello 程序是完全透明 hello 終端使用者的觀點。 hello 使用者將再試一次 tooaccess 共用資源、 hello 的資源需要驗證，hello 使用者將有的 toosend 順序 tooobtain 驗證要求 tooAzure AD hello 權杖和存取 hello 資源。 整個程序都會在背景執行，使用者無須動作。 它也是可能 toogrant 權限 tooa[群組](active-directory-manage-groups.md#getting-started-with-access-management)tooallow 順序中的使用者加以 tooperform 某些常見的動作。

有資料隱私權顧慮的組織通常需要對其解決方案進行資料分類。 如果目前的內部部署基礎結構已經使用資料分類，則可能 tooleverage Azure AD 為 hello 使用者的身分識別的主要儲存機制。 在 Windows Server 2012 R2 中，內部部署中用於資料分類的常用工具稱為 [資料分類工具組](https://msdn.microsoft.com/library/Hh204743.aspx) 。 此工具可以協助 tooidentify、 分類及保護您的私人雲端中的檔案伺服器上的資料。 它也是可能 tooleverage hello[自動檔案分類](https://technet.microsoft.com/library/hh831672.aspx)在 Windows Server 2012 tooaccomplish 這。

如果您的組織在位置中沒有資料分類，但需要 tooprotect 機密檔案而不需要加入新的伺服器內部部署，則可以使用 Microsoft [Azure Rights Management Service](https://technet.microsoft.com/library/JJ585026.aspx)。  Azure RMS 使用的安全加密、 身分識別及授權原則 toohelp，您的檔案和電子郵件，並可以跨多個裝置運作 — 手機、 平板電腦及電腦。 因為 Azure RMS 屬於雲端服務，則無需 tooexplicitly 會設定與其他組織信任之前，您可以與他們共用受保護的內容。 如果他們已有 Office 365 或 Azure AD 目錄，則會自動支援跨組織的共同作業。 您也可以只 hello 目錄屬性，Azure RMS 需要 toosupport 通用識別身分為您在內部部署 Active Directory 的帳戶使用 Azure Active Directory 同步處理服務 (AAD Sync) 或 Azure AD Connect 同步處理。

內容管理不可或缺的一部分 toounderstand 正在存取的資源，因此豐富的記錄功能，請務必 hello 身分識別管理解決方案。 Azure AD 提供超過 30 天的記錄，其中包括：

* 角色成員資格的變更 (例如： 加入 tooGlobal 系統管理員角色的使用者)
* 認證更新 (例如：密碼變更)
* 網域管理 (例如：驗證自訂網域、移除網域)
* 新增或移除應用程式
* 使用者管理 (例如：新增、移除、更新使用者)
* 新增或移除授權

> [!NOTE]
> 讀取[Microsoft Azure 安全性和稽核記錄檔管理](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf)tooknow 深入了解 Azure 中的記錄功能。
> 根據您回答中的 hello 問題的方式[判斷內容管理需求](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)，您應該能夠 toodetermine 方式 hello 內容 toobe 管理混合式身分識別方案中。 表 6 中公開的所有選項都是能夠與 Azure AD 整合，所以也就是更適合您的業務需求的重要 toodefine。
>
>

| 內容管理選項 | 優點 | 缺點 |
| --- | --- | --- |
| 集中式的內部部署 (Active Directory Rights Management Server) |負責分類 hello 資料的 hello 伺服器基礎結構的完整控制權 <br> Windows Server 中內建功能，不需要取得額外授權或訂用帳戶 <br> 可以與混合式案例中的 Azure AD 整合 <br> 支援 Microsoft Online Services，例如 Exchange Online 和 SharePoint Online 以及 Office 365 中的資訊版權管理 (IRM) 功能 <br> 支援內部部署 Microsoft 伺服器產品，例如 Exchange Server、SharePoint Server，以及執行 Windows Server 和檔案分類基礎結構 (FCI) 的檔案伺服器。 |較高，維護 （保留向上更新、 組態和升級），因為 IT 擁有 hello 伺服器 <br> 需要內部部署的伺服器基礎結構<br> 在原生狀態下不會使用 Azure 功能 |
| 集中於 hello 雲端 (Azure RMS) |更容易比較 toomanage toohello 內部部署方案 <br> 可以與混合式案例中的 AD DS 整合 <br>  完全與 Azure AD 整合 <br> 不需要伺服器的內部訂單 toodeploy hello 服務中 <br> 支援內部部署 Microsoft 伺服器產品，例如 Exchange Server、SharePoint Server，以及執行 Windows Server 和檔案分類基礎結構 (FCI) 的檔案伺服器 <br> IT 可透過 BYOK 功能完全控制其租用戶的金鑰。 |組織必須具有支援 RMS 的雲端訂用帳戶  <br> 貴組織的 RMS 項目必須有 Azure AD 目錄 toosupport 使用者驗證 |
| 混合式 (Azure RMS 與內部部署 Active Directory Rights Management Server 整合) |此案例會累積 hello 優點兩者集中於內部，並且在 hello 雲端中。 |組織必須具有支援 RMS 的雲端訂用帳戶  <br> 貴組織的 RMS，項目必須有 Azure AD 目錄 toosupport 使用者驗證 <br> Azure 雲端服務與內部部署基礎結構之間必須要有連線 |

## <a name="define-access-control-options"></a>定義存取控制選項
利用 hello 驗證、 授權和存取控制功能將無法 tooenable 的 Azure AD 中可用您公司 toouse 中央識別儲存機制同時使用者和合作夥伴允許 toouse 單一登入 (SSO)，hello 中所示下圖：

![](./media/hybrid-id-design-considerations/centralized-management.png)

集中式管理以及與其他目錄的完全整合

Azure Active Directory 提供 SaaS 應用程式的單一登入 toothousands，並在內部部署 web 應用程式。 請閱讀 hello [Azure Active Directory 同盟相容性清單： 單一登入的協力廠商身分識別提供者可以使用的 tooimplement](https://msdn.microsoft.com/library/azure/jj679342.aspx) hello SSO 協力廠商所測試的更多詳細的發行項Microsoft。 這個功能可讓組織 tooimplement 各種 B2B 狀況，同時保留 hello 身分識別和存取管理控制項。 不過，在 hello B2B 設計程序期間是重要 toounderstand hello 驗證方法，將由 hello 夥伴並驗證 azure 支援這個方法。 以下是 Azure AD 目前支援的方法：

* 安全性判斷提示標記語言 (SAML)
* OAuth
* Kerberos
* 權杖
* 憑證

> [!NOTE]
> 讀取[Azure Active Directory 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn151124.aspx)tooknow 更多詳細資料每個通訊協定以及其在 Azure 中的功能。
>
>

使用 hello Azure AD 支援、 行動商業應用程式可以使用 hello 相同輕鬆行動服務驗證經驗 tooallow 員工 toosign 至其行動裝置的應用程式，利用其公司的 Active Directory 認證。 利用此功能，支援 Azure AD 作為身分識別提供者與行動服務中以 hello 其他身分識別提供者已支援 （其中包含 Microsoft 帳戶、 Facebook ID、 Google ID 和 Twitter 識別碼）。 如果 hello 內部部署應用程式會使用 hello 位於 hello 公司的 AD DS 使用者的認證，hello 協力廠商和來自 hello 雲端使用者的存取權應該是透明的。 您可以管理使用者的條件式存取控制 too(cloud-based) web 應用程式、 web 應用程式開發介面、 Microsoft 雲端服務、 第 3 個合作對象 SaaS 應用程式和原生 （行動裝置） 的用戶端應用程式，並具有的安全性、 hello 優點稽核，在其中一個 reporting位置。 不過，建議使用 toovalidate 這在非生產環境中或使用有限的使用者。

> [!TIP]
> 是，Azure AD 不需要群組原則為 AD DS 含有重要 toomention。 在裝置的順序 tooenforce 原則您需要在行動裝置管理解決方案例如[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx)。
>
>

一旦 hello 使用者會使用 Azure AD 進行驗證，請務必 tooevaluate hello hello 使用者的存取層級會有它。 hello hello 使用者的存取層級必須在資源上可能會不同，而 Azure AD 可以加入額外的安全性層級控制存取 toosome 資源，您必須記住 hello 資源本身也可以有它自己的存取控制清單分開，例如 hello 存取控制是位於檔案伺服器中的檔案。 hello 圖摘要說明存取控制，您可以在混合式案例中的 hello 層級：

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Hello X 圖中顯示的圖表中的每個互動表示一個可以涵蓋 Azure AD 的存取控制案例。 每個案例的說明如下：

1. 條件式存取 tooapplications 屬於裝載在內部部署： 您可以使用已註冊的裝置存取原則的應用程式設定 toouse AD FS 與 Windows Server 2012 R2。 如需有關設定內部部署之條件式存取的詳細資訊，請參閱 [使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-conditional-access.md)。

2. Azure 入口網站的存取控制 toohello: Azure 也可讓您控制存取 toohello 入口網站使用以角色為基礎的存取控制 (RBAC))。 這個方法可讓 hello 公司 toorestrict hello 數量的個人可以在 hello Azure 入口網站中執行的操作。 藉由使用 RBAC toocontrol 存取 toohello 入口網站，IT 系統管理員可以使用下列存取管理方法的 hello 委派存取：

* 群組為基礎的角色指派： 可以從本機 Active Directory 指派存取 tooAzure AD 群組可以同步處理。 這可讓您 tooleverage hello 現有的投資，您的組織所做的工具和程序來管理群組。 您也可以使用 Azure AD Premium hello 委派的群組管理功能。
* 利用內建的 Azure 中的角色： 您可以使用三個角色-使用者和群組具有權限 toodo 只有 hello 工作所需 toodo 工作的擁有者、 參與者和讀取器，tooensure。
* 細微的存取權 tooresources： 您可以指派角色 toousers 和特定的訂用帳戶、 資源群組或個別的 Azure 資源，例如網站或資料庫群組。 如此一來，您可以確保使用者具有存取 tooall hello 資源所需，就不需要 toomanage 沒有存取 tooresources。

> [!NOTE]
> 如果您要建置的應用程式，並要 toocustomize hello 存取控制，所以也可能 toouse 供授權的 Azure AD 應用程式角色。 檢閱這[WebApp-RoleClaims-DotNet 範例](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet)如何 toobuild 應用程式 toouse 這項功能。
>
>

3. Office 365 應用程式使用 Microsoft Intune 的條件式存取： IT 系統管理員可以提供條件式存取裝置原則 toosecure 公司資源，而在 hello 相同時間相容的裝置 tooaccess hello 讓資訊工作者服務。 如需詳細資訊，請參閱 [Office 365 服務的條件式存取裝置原則](active-directory-conditional-access-device-policies.md)。

4. Saas 應用程式的條件式存取：[這項功能](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx)允許您 tooconfigure 每個應用程式多因素驗證存取規則與 hello 能力 tooblock 權限的使用者不在受信任的網路上。 您可以套用 hello 多因素驗證規則 tooall 使用者被指派 toohello 應用程式，或只適用於使用者在指定的安全性群組。 存取 hello 應用程式來自 IP 位址，在內部，可能會從 hello 多因素驗證需求排除使用者 hello 組織的網路。

由於存取控制的 hello 選項使用多層方法，這些選項之間的比較則不適用這項工作。 請確定您利用所有可用的每個案例中，您需要 toocontrol 存取 tooyour 資源的選項。

## <a name="define-incident-response-options"></a>定義事件回應選項
Azure AD 可協助 IT tooidentity 潛在安全性風險 hello 透過在環境中監視使用者活動，IT 能夠利用 Azure AD 存取與使用方式報表 hello 完整性與您的組織目錄的安全性功能 toogain 可見性。 利用此資訊，為 IT 系統管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。  [Azure AD Premium 訂用帳戶](active-directory-get-started-premium.md)具有一組安全性報告，可讓 IT tooobtain 這項資訊。 [Azure AD 報告](active-directory-view-access-usage-reports.md) 歸類如下：

* **異常報表**： 包含登入事件，我們發現 toobe 異常。 我們的目標是 toomake 您注意這類活動，並讓您 toobe 無法 toomake 判斷事件是否可疑。
* **整合式應用程式報告**：可供深入了解雲端應用程式在組織中的使用方式。 Azure Active Directory 提供與數千個雲端應用程式的整合。
* **錯誤報告**： 指出佈建帳戶 tooexternal 應用程式時可能發生的錯誤。
* **使用者特定報告**：顯示特定使用者的裝置/登入活動資料。
* **活動記錄**： 包含 hello 過去 24 小時、 過去 7 天內所有稽核事件的記錄或過去 30 天，以及群組活動變更、 和密碼重設和註冊活動。

> [!TIP]
> 也可以協助 hello 事件回應小組工作的大小寫的其他報表為 hello[認證外洩的使用者](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx)報表。  此報告會呈現這些外洩的認證清單與您的租用戶之間的任何相符項目。
>
>

Azure AD 中還有其他可在事件回應調查期間使用的重要內建報告，包括：

* **密碼重設活動**: hello 系統管理員提供深入了解如何主動 hello 組織中使用密碼重設。
* **密碼重設註冊活動**：可讓您深入了解哪些使用者註冊了密碼重設方法，以及他們選取了哪些方法。
* **群組活動**： 提供變更 toohello 群組的歷程記錄 (例如： 使用者加入或移除)，由 hello 存取面板中。

此外 toohello 核心報告有哪些可用功能在 Azure AD Premium，可以也運用在事件回應調查過程中，IT 能夠利用稽核報告 tooobtain 資訊例如：

* 角色成員資格的變更 (例如： 加入 tooGlobal 系統管理員角色的使用者)
* 認證更新 (例如：密碼變更)
* 網域管理 (例如：驗證自訂網域、移除網域)
* 新增或移除應用程式
* 使用者管理 (例如：新增、移除、更新使用者)
* 新增或移除授權

由於事件回應 hello 選項使用多層方法，這些選項之間的比較則不適用這項工作。 請確定您利用所有選項適用於每個案例中，您需要 toouse Azure AD 的報告功能做為您的公司事件回應程序的一部分。

## <a name="next-steps"></a>後續步驟
[判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)
