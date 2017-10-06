---
title: "aaaChoose Azure 的混合式身分識別解決方案 |Microsoft 文件"
description: "收到 hello 可用的混合式身分識別解決方案和您 toomake hello 最佳身分識別控管決定為您的組織建議的基本知識。"
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Microsoft 混合式身分識別解決方案
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)混合式身分識別解決方案可讓您與 Azure AD，同時仍管理使用者在內部 toosynchronize 在內部部署目錄物件。 hello 先決策 toomake 規劃您在內部部署 Windows Server Active Directory 與 Azure AD 會為您想 toouse 同步處理身分識別或同盟身分識別的 toosynchronize 時。 同步身分識別，並選擇性地密碼雜湊，讓使用者 toouse hello 相同密碼 tooaccess 在內部部署和雲端架構的組織資源。 如需更進階的案例需求，例如單一登入 (SSO) 或內部部署 MFA，您需要 toodeploy Active Directory Federation Services (AD FS) toofederate 身分識別。 

有數個選項可用來設定混合式身分識別。 本文章提供您選擇適合組織以便於部署的 hello 和特定身分識別和存取管理需求的資訊 toohelp。 當您考慮哪些身分識別模型最適合貴組織的需求，您也需要 toothink 有關時間、 現有的基礎結構、 複雜度和成本。 這些因素對每個組織而言不同，並可能隨時間改變。 不過，如果您的需求就會變更，您也可以 hello 彈性 tooswitch tooa 不同的身分識別模型。

> [!TIP]
> 這些解決方案全都由 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 傳遞。

## <a name="synchronized-identity"></a>已同步處理的身分識別 
已同步處理身分識別與 Azure AD 是最簡單方式 toosynchronize hello 內部部署目錄物件 （使用者和群組）。 

![已同步處理的混合式身分識別](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Hello 最簡單且最快方法同步處理身分識別時，您的使用者仍然需要 toomaintain 不同的密碼以雲端為基礎的資源。 tooavoid，您也可以 （選擇性）[同步處理的使用者密碼雜湊](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization)tooyour Azure AD 目錄。 相同的使用者名稱和密碼，它們會使用內部部署同步處理密碼雜湊可讓使用者 toolog toocloud 組織資源，以在 hello。 Azure AD Connect 會定期檢查您的內部部署目錄變更，並且讓 Azure AD 目錄保持同步狀態。 當內部部署 Active Directory 的使用者屬性或密碼變更時，它會自動在 Azure AD 中更新。 

大部分的組織，只需 tooOffice 365、 SaaS 應用程式，以及其他 Azure AD 為基礎的資源在其使用者 toosign tooenable 建議 hello 預設密碼同步處理選項。 如果您無法解決，您將需要 toodecide 傳遞驗證與 AD FS 之間。

> [!TIP]
> 使用者密碼會儲存在 hello 形式表示 hello 實際使用者密碼的雜湊值的內部部署 Windows Server Active Directory。 雜湊值是單向數學函式 (hello 雜湊演算法) 的結果。 沒有密碼的單向函式 toohello 純文字版的 hello 方法 toorevert 的結果。 您無法使用密碼雜湊 toosign tooyour 在內部部署網路中。 當您選擇 toosynchronize 密碼時，Azure AD Connect 擷取密碼雜湊 hello 從內部部署 Active Directory 和適用於處理 toohello 密碼雜湊同步的 tooAzure AD 之前的額外安全性。 密碼同步化也可以對照密碼回寫 tooenable 自助式密碼重設 Azure AD 中。 此外，您可以加入網域的電腦是連線的 toohello 公司網路上的使用者啟用單一登入 (SSO)。 單一登入，以啟用的使用者只需要 tooenter username toosecurely 存取雲端資源。 

## <a name="pass-through-authentication"></a>傳遞驗證
[Azure AD 傳遞驗證](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication)會針對使用內部部署 Active Directory 並以 Azure AD 為基礎的服務，提供簡單的密碼驗證解決方案。 如果貴組織的安全性與相容性原則不允許傳送使用者的密碼，即使在雜湊的格式，以及您只需要已加入網域裝置 toosupport 桌面 SSO，則建議您評估使用傳遞驗證。 傳遞驗證不需要任何 hello 周邊網路，可簡化 hello 部署基礎結構相較於 AD FS 中的部署。 當使用者使用 Azure AD 登入時，此驗證方法會向您的內部部署 Active Directory 直接驗證使用者的密碼。

![傳遞驗證](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

使用傳遞驗證時，不需要複雜的網路基礎結構，也不需要 toostore hello 雲端中的內部部署密碼。 與單一登入，結合傳遞驗證登入 tooAzure AD 或其他雲端服務時，提供真正整合的經驗。

傳遞驗證已透過 Azure AD Connect 設定，其使用可接聽密碼驗證要求的簡單內部部署代理程式。 hello 代理程式可被輕易地部署的 toomultiple 機器 tooprovide 高可用性及負載平衡。 所有通訊都都會只輸出，因為沒有安裝在 DMZ 中的 hello 連接器 toobe 的需求。 hello hello 連接器的伺服器電腦需求如下所示：

- Windows Server 2012 R2 或更新版本
- 加入 tooa hello 透過它會驗證使用者的樹系中的網域

> [!NOTE]
> Azure AD 傳遞驗證目前為預覽狀態，可為支援新式驗證的網頁瀏覽器型用戶端和 Office 用戶端提供支援。 對於不支援的用戶端，例如舊版 Office 用戶端和 Exchange ActiveSync （包括行動裝置上的原生電子郵件用戶端），它是建議的 toouse hello 新式驗證對等。 新式驗證不只允許通過驗證，但也可以套用，例如多重要素驗證的條件式存取原則 toobe。 

傳遞驗證目前不支援使用 Windows 10 裝置加入 tooAzure 廣告時。 不過，您可以使用密碼雜湊同步處理，作為自動的後援 toosupport Windows 10 和 hello 舊版用戶端先前所述。 Hello 在預覽期間，密碼雜湊同步處理預設會啟用為 hello 登入 Azure AD Connect 中選項已選取的傳遞驗證。


## <a name="federated-identity-ad-fs"></a>同盟身分識別 (AD FS)
如需更進一步控制使用者如何存取 Office 365 和其他雲端服務，您可以使用 [Active Directory Federation Services (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016) 設定與單一登入 (SSO) 的目錄同步作業。 同盟使用者的登入與 AD FS 委派驗證 tooan 內部驗證使用者認證的伺服器。 在此模型中，在內部部署 Active Directory 認證絕不會傳遞 tooAzure AD。

![同盟身分識別](./media/choose-hybrid-identity-solution/federated-identity.png)

也稱為識別身分同盟，此登入方法可確保所有的使用者驗證，控制在內部部署，並且允許系統管理員 tooimplement 使用較嚴格的層級的存取控制。 識別身分同盟與 AD FS 是最複雜的 hello 選項，而且需要部署額外的伺服器在內部部署環境中。 識別身分同盟也認可 tooproviding 24x7 支援 Active Directory 和 AD FS 基礎結構。 因為如果您在內部部署的網際網路存取，網域控制站或 AD FS 伺服器無法使用，使用者無法登入 toocloud 服務必須支援這個高層級。

> [!TIP]
> 如果您決定 toouse 同盟與 Active Directory Federation Services (AD FS)，您可以選擇性地設定密碼同步化，以當作備份您的 AD FS 基礎結構失敗時。


## <a name="common-scenarios-and-recommendations"></a>常見案例和建議
以下是一些常見的混合式身分識別和存取管理案例的建議 toowhich 混合式身分識別選項 （或選項） 可能適用於每個。

|我需要：|PWS 和 SSO<sup>1</sup>| PTA 和 SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|同步處理新的使用者、 連絡人及群組帳戶會自動建立我的內部部署 Active Directory toohello 雲端中。|![建議](./media/choose-hybrid-identity-solution/ic195031.png)| ![建議](./media/choose-hybrid-identity-solution/ic195031.png) |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|設定 Office 365 混合式案例的租用戶|![建議](./media/choose-hybrid-identity-solution/ic195031.png)| ![建議](./media/choose-hybrid-identity-solution/ic195031.png) |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|啟用 在我的使用者 toosign 並存取雲端服務使用內部部署密碼|![建議](./media/choose-hybrid-identity-solution/ic195031.png)| ![建議](./media/choose-hybrid-identity-solution/ic195031.png) |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|使用公司認證實作單一登入|![建議](./media/choose-hybrid-identity-solution/ic195031.png)| ![建議](./media/choose-hybrid-identity-solution/ic195031.png) |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|請確定沒有密碼雜湊會儲存在 hello 雲端| |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|啟用內部部署 Multi-Factor Authentication 解決方案| | |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|對使用者支援智慧卡驗證<sup>4</sup>| | |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|
|在 hello Office 入口網站和 hello Windows 10 desktop 顯示密碼到期通知| | |![建議](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> 透過單一登入同步處理密碼。 

> <sup>2</sup> 傳遞驗證和單一登入。 

> <sup>3</sup> 與 AD FS 同盟的單一登入。

> <sup>4</sup>可以與您的企業 PKI tooallow 整合 AD FS 登入使用的憑證。 這些憑證可以是透過信任的佈建管道 (例如 MDM、GPO、智慧卡憑證 (包括 PIV/CAC 卡) 或 Hello for Business (cert-trust)) 部署的軟性憑證。 如需智慧卡驗證支援的詳細資訊，請參閱[這個部落格](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)。


## <a name="next-steps"></a>後續步驟
[深入了解 Azure 概念證明環境中的其他資訊](https://aka.ms/aad-poc)

[安裝 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[監視混合式身分識別同步處理](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

