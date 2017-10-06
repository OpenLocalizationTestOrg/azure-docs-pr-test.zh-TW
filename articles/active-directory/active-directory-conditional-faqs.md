---
title: "aaaAzure Active Directory 條件式存取常見問題集 |Microsoft 文件"
description: "取得 Azure Active Directory 中的條件式存取相關常見問題的解答 toofrequently。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Azure Active Directory 條件式存取常見問題集

## <a name="which-applications-work-with-conditional-access-policies"></a>哪些應用程式會使用條件式存取原則？

如需有關使用條件式存取原則之應用程式的資訊，請參閱[在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器](active-directory-conditional-access-supported-apps.md)。

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>是否會針對 B2B 共同作業與來賓使用者強制套用條件式存取原則？

系統會針對企業對企業 (B2B) 共同作業使用者強制執行原則。 不過，在某些情況下，使用者可能不能 toosatisfy hello 原則需求。 例如，來賓使用者的組織可能不支援多重要素驗證。 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>沒有 SharePoint Online 原則也適用於 tooOneDrive 商務嗎？

是。 SharePoint Online 原則也適用於 tooOneDrive 商務。


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>為什麼我無法在用戶端應用程式 (例如 Word 或 Outlook) 上設定原則？

條件式存取原則會設定服務的存取需求。 驗證 toothat 服務時，它會強制執行。 hello 原則未直接在用戶端應用程式上設定。 而是在用戶端呼叫服務時套用。 例如，在 SharePoint 上設定的原則會套用 tooclients 呼叫 SharePoint。 在 Exchange 上設定的原則會套用 tooOutlook。

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>條件式存取原則是否套用 tooservice 帳戶？

條件式存取原則會套用 tooall 使用者帳戶。 這包括作為服務帳戶的使用者帳戶。 通常，自動執行的服務帳戶無法滿足條件式存取原則的 hello 的需求。 例如，可能需要多重要素驗證。 您可以利用條件式存取原則管理設定，將服務帳戶排除在原則之外。 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>是否有提供「圖形 API」來設定條件式存取原則？

目前沒有。 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>不支援的裝置平台的 hello 預設排除原則為何？

目前，只會對 iOS 和 Android 裝置的使用者強制執行條件式存取原則。 其他裝置平台上的應用程式，根據預設，不會影響 hello 適用於 iOS 和 Android 裝置的條件式存取原則。 租用戶系統管理員可以選擇 toooverride hello 全域原則 toodisallow 存取 toousers 不支援的平台上。


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>條件式存取原則對 Microsoft Teams 有何用途？  

Microsoft Teams 在核心產能情節中非常依賴 Exchange Online 和 SharePoint Online，例如會議、行事曆和檔案共用。 當使用者登入時，這些雲端應用程式設定的條件式存取原則會套用 tooMicrosoft 小組。

在 Azure Active Directory 條件式存取原則中，也支援將 Microsoft Teams 當作個別的雲端應用程式。 當使用者登入時，憑證授權單位設定原則的雲端應用程式會套用 tooMicrosoft 小組。

適用於 Windows 和 Mac 的 Microsoft Teams 桌面用戶端支援新式驗證。 新式驗證將登入跨平台根據 hello Azure Active Directory 驗證程式庫 (ADAL) tooMicrosoft Office 用戶端應用程式整合。 
