---
title: "不需要透過 Windows Hello 的商務和 Azure AD 密碼 aaaAuthenticating 識別 |Microsoft 文件"
description: "提供 Windows Hello 企業版概觀以及部署 Windows Hello 企業版的其他資訊。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>透過 Windows Hello 企業版不需要密碼就能驗證身分識別
hello 目前方法的驗證，以單獨的密碼不安全的足夠 tookeep 使用者。 使用者會重複使用和忘記密碼。 密碼是 breachable、 phishable、 容易出錯的 toocracks 和猜得到。 它們也會取得困難 tooremember 而容易出錯的 tooattacks 喜歡 」[傳遞 hello 雜湊](https://technet.microsoft.com/dn785092.aspx)"。

## <a name="about-windows-hello-for-business"></a>關於 Windows Hello 企業版
對於組織和取用者來說，Windows Hello 企業版是超越密碼的私密金鑰/公開金鑰或憑證式驗證方法。 這種形式的驗證會仰賴可以取代密碼和抗拒 toobreaches、 竊取的行為和網路釣魚的金鑰組認證。

 Windows Hello 企業版可讓使用者驗證 tooa Microsoft 帳戶、 Windows Server Active Directory 帳戶，Microsoft Azure Active Directory (Azure AD) 帳戶或非 Microsoft 服務可支援快速識別線上 (FIDO) 驗證。 初始雙步驟驗證期間 Windows Hello 的商務註冊之後, hello 使用者的裝置上設定 Windows Hello 的商務與 hello 使用者設定鍵筆勢，這可以是 Windows Hello 或 PIN。 hello 使用者提供 hello 筆勢 tooverify 其身分識別。 Windows 然後使用 Windows Hello 的商務 tooauthenticate hello 使用者，並幫助他們 tooaccess 受保護資源和服務。

hello 私用金鑰可僅透過像是 PIN、 生物識別技術或遠端裝置上 「 使用者筆勢 」 像 hello 使用者的智慧卡使用 toosign toohello 裝置中。 這項資訊是連結的 tooa 憑證或非對稱金鑰組。 若是 attested hello 裝置是否受信任的平台模組 (TPM) 晶片的硬體 hello 私用金鑰。 hello 私密金鑰永遠不會離開裝置 hello。

hello 公開金鑰會向 Azure Active Directory 和 Windows Server Active Directory （適用於內部部署）。 身分識別提供者 (IDPs) 對應 hello 公開金鑰 hello 使用者 toohello 私用金鑰來驗證 hello 使用者，並提供登入資訊透過一次密碼 (OTP)、 PhoneFactor 或不同的通知機制。

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>為什麼企業應該採用 Windows Hello 企業版
藉由啟用 Windows Hello 企業版，企業可透過下列動作，使其資源更安全：

* 使用硬體慣用選項來設定 Windows Hello 企業版。 這表示將會在可用時於 TPM 1.2 或 TPM 2.0 上產生金鑰。 無法使用 TPM 時，軟體將會產生 hello 索引鍵。
* 定義 hello 既複雜又冗長 hello 釘選，以及是否 Hello 使用量啟用組織中。
* 設定 Windows Hello 的商務 toosupport 類似智慧卡的情況下使用憑證為基礎的信任。

## <a name="how-windows-hello-for-business-works"></a>Windows Hello 企業版的運作方式
1. Hello 硬體上產生金鑰由 TPM 或軟體。 許多裝置都具備整合裝置的密碼編譯金鑰所保護 hello 硬體的內建 TPM 晶片。 TPM 1.2 或 TPM 2.0 會產生金鑰或從 hello 產生索引鍵建立的憑證。
2. hello TPM 驗證這些硬體繫結機碼。
3. 單一 unlock 筆勢解除鎖定裝置 hello。 此筆勢允許存取 toomultiple 資源 hello 裝置是否已加入網域或 Azure AD 聯結。

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Hello Windows Hello 的商務生命週期的運作方式
![Windows Hello 企業版生命週期](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

hello 上述圖表說明 hello 私密/公開金鑰組和 hello hello 身分識別提供者的驗證。 以下將詳細說明每個步驟：

1. hello 使用者證明其身分識別，透過多個內建的校訂方法 （手勢，實體智慧卡，多重要素驗證） 和傳送此資訊 tooan 身分識別提供者 (IDP) Azure Active Directory 等或在內部部署 Active Directory。
2. hello 裝置然後建立 hello 金鑰、 驗證 hello 金鑰、 接受 hello 此金鑰的公開部分、 附加與站台陳述式、 登入時，並傳送 toohello IDP tooregister hello 索引鍵。
3. Hello IDP 註冊 hello 的 hello 金鑰的公開部分，因為 hello IDP 挑戰 hello 裝置 toosign 與 hello 金鑰 hello 私用部分。
4. hello IDP 接著會驗證和問題 hello 可讓使用者 hello 與 hello 裝置存取受保護的 hello 資源的驗證 token。 IDPs 可以撰寫跨平台應用程式或使用瀏覽器支援 （透過 JavaScript/Webcrypto 應用程式開發介面） toocreate 並使用 Windows Hello 的商務使用者的認證。

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>商務 Windows Hello 的 hello 部署需求
### <a name="at-hello-enterprise-level"></a>Hello 企業層級
* hello 企業的 Azure 訂用帳戶。

### <a name="at-hello-user-level"></a>Hello 使用者層級
* hello 使用者的電腦執行 Windows 10 專業版或 Enterprise。

如需詳細的部署指示，請參閱[商務 hello 組織中啟用 Windows Hello](active-directory-azureadjoin-passport-deployment.md)。

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

