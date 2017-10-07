---
title: "透過 Azure Active Directory Join aaaExtending 雲端功能 tooWindows 10 裝置 |Microsoft 文件"
description: "提供 Windows 10 裝置可以利用 Azure Active Directory 上註冊的 Azure AD Join tooget 的方式的詳細的概觀。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端
## <a name="what-is-azure-active-directory-join"></a>什麼是 Azure Active Directory Join？
Azure Active Directory Join (Azure AD Join) 是在 hello 裝置的 Azure Active Directory tooenable 集中式管理中註冊屬公司擁有的裝置 hello 功能。 它可讓使用者，例如員工和學生 tooconnect toohello 企業雲端透過 Azure Active Directory。 這可讓簡化的 Windows 部署和存取 tooorganizational 應用程式及任何 Windows 裝置的資源，同時公司以及個人擁有 (BYOD)。

Azure AD Join 的目標對象是雲端優先/僅限雲端的企業 (通常是不具內部部署 Windows Server Active Directory 基礎結構的中小型企業)。 可以加入該，Azure AD，並也會使用在無法執行這項傳統網域聯結 （行動裝置，例如），或針對主要需要 tooaccess Office 365 或其他與 Azure AD 整合的 SaaS 應用程式的使用者的裝置上的大型組織。

雖然仍提供 hello 傳統網域加入的 hello 內部部署的最佳體驗能夠加入網域的裝置上，加入 Azure AD 是適用於不能加入網域的裝置。 也適用於管理 hello 雲端中的使用者加入 azure AD。 它是藉由使用行動裝置管理功能進行管理，而不是使用傳統網域管理工具，像是群組原則和 System Center Configuration Manager (SCCM)。

![公司裝置和個人裝置搭配內部部署 Active Directory 和 Azure AD 的概觀](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>為什麼企業應該採用 Azure AD Join？
* **在大部分的企業 hello 雲端**： 如果您已經移動，或要移動 tooa 模型，您會降低您在內部部署耗用量並想 toooperate hello 定域機組中更多，Azure AD Join 獲益您。 或許您已經手動或透過同步處理內部部署 Active Directory 的方式建立了 Azure AD 帳戶。 無論如何，您擁有帳戶在 Azure AD 中，您可以使用它 toosign tooWindows 10 中。 您的使用者可以將其電腦 tooAzure AD 透過任一 hello 的全新體驗 (OOBE) 或 hello 設定功能表。 加入之後，使用者會喜歡單一登入 (SSO) 存取 toocloud 資源，如 Office 365，在瀏覽器中或在 Office 應用程式。
* **教育機構**： 我們了解有關通常 hello 案例的其中一個是教育機構，有兩種使用者類型： 學生版和教職員版。 教職員版成員被視為長期 hello 組織的成員，因此建立內部部署帳戶是合理的。 但學生 shorter-term hello 組織的成員，因此可以在 Azure AD 中管理。 這表示，而不是儲存在內部 toohello 雲端可以推送目錄小數位數。 這也表示學生可以登入其 Azure AD 帳戶與 tooWindows 並取得存取 tooOffice 365 資源，在瀏覽器中或在 Office 應用程式。
* **零售企業**： 我們聽說來自客戶的另一個案例是其 desire toomanage 季節性背景工作更容易。  同樣地，較長期、全職員工的帳戶通常是在已加入網域的電腦上建立為內部部署帳戶。 但季節性工作者屬於 shorter-term hello 組織，因此很理想 toomanage 其中使用者授權可以更輕鬆地四處移動它們。 與 Office 365 授權的 hello 雲端中建立這些使用者帳戶可讓 hello 登入 tooWindows 和 Office 應用程式與 Azure AD 帳戶的使用者 tooget hello 優點。 同時，在他們離職之後，您也能對他們的授權保有更大的處理彈性。
* **其他企業**：即使您在內部部署 Active Directory 中維護使用者，您仍然可以享受到將使用者加入 Azure AD 的好處。 這是因為 Azure AD 為 Azure AD 和內部部署資源提供簡化的加入經驗、有效率的裝置管理、自動的行動裝置管理註冊和單一登入功能。  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Azure AD Join 提供哪些功能？
您可以使用 Azure AD Join 取得 hello 下列：

* **公司擁有裝置的自動佈建**： 使用 Windows 10，使用者可以在 hello 鶈蜪經驗中，不需要 IT 涉入設定全新、 這些裝置。
* **支援新式的表單係數**： 加入 Azure AD 的運作方式沒有 hello 傳統網域加入功能的裝置上。  
* **支援針對現有的組織帳戶**： 使用者不再需要 toocreate 和維護個人的 Microsoft 帳戶 tooget hello 公司所核發的裝置上的最佳體驗，與 Windows 8 所顯示的一樣。 他們可以改為在 Azure AD 中使用現有的工作帳戶。 對許多組織來說，這基本上表示使用者可以設定和登入以 hello tooWindows 相同他們使用 tooaccess Office 365 的認證。
* **自動的行動裝置管理註冊**： 裝置可以自動註冊行動裝置管理連線時 tooAzure AD。 此程序適用於 Microsoft Intune 與協力廠商的行動裝置管理解決方案。 當 Intune 完成裝置管理時，IT 系統管理員可以監視/管理一起加入網域的裝置 hello SCCM 管理主控台中的 Azure AD 加入裝置。
* **單一登入 toocompany 資源**： 使用者享受單一登入 hello Windows 桌面 tooapps 及 hello 雲端，例如 Office 365 和無數依賴 Azure AD 進行驗證，透過的商務應用程式中的資源[Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md)。 公司擁有的裝置已加入的 tooAzure AD 也喜歡 SSO tooon 內部部署資源，當 hello 裝置到公司網路，以及從任何地方時這些資源會公開透過 hello [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/Dn768219.aspx)。
* **OS 狀態漫遊**：協助工具設定、網站及 Wi-Fi 密碼和其他設定都在公司擁有的裝置之間同步處理，而不需使用個人的 Microsoft 帳戶。
* **企業專用的 Windows 市集**: hello Windows 市集支援應用程式擷取和使用 Azure AD 帳戶授權。 組織可以大量授權的應用程式，使其可用 toohello 使用者在其組織中。

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>不同的裝置如何與 Azure AD Join 搭配運作？
| 公司裝置 （聯結的 tooon 內部部署網域） | 公司裝置 （聯結的 toohello 雲端） | 個人裝置 |
| --- | --- | --- |
| 使用者可以使用工作認證登入 Windows (就像他們現在所做的一樣) |使用者可以登入 tooWindows 與 Azure AD 中管理的工作認證。 這在三種情況下與公司裝置有關： <ol><li>hello 組織在內部部署 （例如，小型企業） 沒有 Active Directory。</li><li>hello 組織並不會在 Active Directory 中建立的所有使用者帳戶 （比方說，學生、 顧問或季節性的背景工作的帳戶未在 Active Directory 中建立）。</li><li>hello 組織具有無法聯結的 tooan （內部） 的網域，例如電話或平板電腦執行行動裝置版 SKU （例如，採取次要裝置 tooa factory/零售樓層） 的公司裝置。</li></ol> Azure AD Join 在受管理和同盟組織中支援加入公司裝置。 |使用者登入 tooWindows 使用其個人的 Microsoft 帳戶認證 （無變化）。 |
| 使用者擁有存取 tooroaming 設定及 hello 企業 Windows 市集。 這些服務會使用工作帳戶，不需要個人的 Microsoft 帳戶。 這需要組織 tooconnect 其內部部署 Active Directory tooAzure AD。 |使用者可以執行自助式設定。 他們可以移透過 hello 首次執行經驗 (FRX) 透過其工作帳戶做為替代的 toohaving IT 佈建 hello 裝置，儘管支援這兩種方法。 |使用者可輕鬆新增未在 Active Directory 或 Azure AD 中管理的工作帳戶。 |
| 使用者擁有 SSO 功能，從 hello toowork 桌面應用程式、 網站和資源--包括在內部部署資源和雲端應用程式都使用 Azure AD 進行驗證。 |裝置會自動在 hello 企業目錄 (Azure AD) 中註冊，並自動在行動裝置管理中註冊。 (Azure AD Premium 功能。) |使用者在應用程式及 toowebsites/資源與此工作帳戶擁有 SSO 功能。 |
| 使用者可以將其個人的 Microsoft 帳戶 tooaccess 他們的個人圖片和檔案而不會影響企業資料。 （漫遊設定繼續使用其工作帳戶 toowork）。hello Microsoft 帳戶啟用 SSO，以及不再磁碟機 hello 漫遊的設定。 |使用者可以在 winlogon 上執行自助式密碼重設 (SSPR)，這表示他們能夠重設忘記的密碼。 (Azure AD Premium 功能。) |使用者有存取 toohello 企業 Windows 存放區，讓他們可以取得並使用其個人裝置上的特定業務應用程式。 |

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

