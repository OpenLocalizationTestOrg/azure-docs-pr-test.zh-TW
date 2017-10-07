---
title: "aaaHow tooconfigure 使用者佈建 Azure AD tooan 組件庫的應用程式 |Microsoft 文件"
description: "如何快速設定豐富的使用者帳戶佈建和解除佈建 tooapplications hello Azure AD 應用程式庫中已列出"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>如何 tooconfigure 使用者佈建 Azure AD tooan 組件庫的應用程式

*使用者帳戶佈建*就是建立、 更新和/或停用使用者帳戶記錄應用程式的本機使用者設定檔存放區中的 hello 操作。 大部分的 SaaS 應用程式和雲端儲存 hello 使用者角色和權限在自己的本機使用者設定檔存放區，和其本機存放區中的這類使用者記錄的存在是*必要*的單一登入及存取 toowork。

在 hello Azure 入口網站，hello**佈建**索引標籤 hello 左側的導覽窗格中的企業應用程式會顯示該應用程式支援哪些佈建模式。 這可能是下列其中一個值：

## <a name="configuring-an-application-for-manual-provisioning"></a>設定應用程式以進行手動佈建

*手動*佈建表示必須以手動方式使用該應用程式所提供的 hello 方法來建立使用者帳戶。 這可能表示登入該應用程式的系統管理員入口網站，然後使用 Web 架構使用者介面新增使用者。 或者，它可能會使用該應用程式所提供的機制，來上傳含有使用者帳戶詳細資料的試算表。 提供由 hello 應用程式或連絡 hello 應用程式開發人員 toodetermine wat 機制可用，請參閱 hello 文件。

如果手動 hello 模式顯示給定的應用程式，這表示，任何自動的 Azure AD 佈建連接器 hello 應用程式尚未建立。 或表示 hello 應用程式並不支援 hello 先決條件使用者管理 API 時哪些 toobuild 自動化佈建的連接器。

如果您想要 toorequest 支援給定的應用程式的自動佈建，您可以填寫在要求<http://aka.ms/aadapprequest>。

## <a name="configuring-an-application-for-automatic-provisioning"></a>設定應用程式以進行自動佈建

「自動」表示已經為此應用程式開發 Azure AD 佈建連接器。 如需有關 hello Azure AD 佈建服務和它的運作方式，請參閱[自動化使用者佈建和取消佈建 tooSaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)。

如需有關如何 tooprovision 特定使用者和群組 tooan 應用程式，請參閱[管理使用者帳戶佈建的企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)。

hello 實際步驟需要的 tooenable 及設定自動佈建 hello 應用程式而有所不同。

>[!NOTE]
>您應該開始尋找 hello 安裝教學課程特定的 toosetting 上佈建您的應用程式，並遵循這些步驟 tooconfigure hello 應用程式與 Azure AD toocreate hello 佈建的連接。 
>
>

應用程式教學課程，請參閱[清單的教學課程有關 tooIntegrate SaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)。

設定佈建是 tooreview 時很重要的事 tooconsider 及設定 hello 屬性對應，以及定義哪些使用者 （或群組） 的屬性流程，從 Azure AD toohello 應用程式的工作流程。 這包括設定 hello 「 比對屬性 」 會使用的 toouniquely 找出並符合 hello 兩個系統之間的使用者/群組。 如需這個重要程序的詳細資訊。

## <a name="next-steps"></a>後續步驟
[在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

