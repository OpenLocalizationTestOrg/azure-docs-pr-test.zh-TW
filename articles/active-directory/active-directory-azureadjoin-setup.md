---
title: "為您的使用者註冊 Azure AD Join aaaSetting |Microsoft 文件"
description: "說明系統管理員如何設定 Azure AD Join 以用於內部部署目錄及裝置註冊。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>在組織中設定 Azure AD Join
設定 Azure Active Directory Join (Azure AD Join) 之前，您需要 tooeither 同步處理您的內部部署目錄的使用者 toohello 雲端或手動建立在 Azure AD 中的 受管理的帳戶。

同步處理您在內部部署使用者 tooAzure AD 中說明的詳細指示[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

toomanually 建立及管理 Azure AD 中的使用者，請參閱太[Azure AD 中的使用者管理](https://msdn.microsoft.com/library/azure/hh967609.aspx)。

## <a name="set-up-device-registration"></a>設定裝置註冊
1. Toohello Azure 入口網站管理員身分登入。
2. 在 hello 左窗格中，選取  **Active Directory**。
3. 在 hello**目錄**索引標籤上，選取您的目錄。
4. 選取 hello**設定** 索引標籤。
5. 移 toohello**裝置**> 一節。
6. 在 hello**裝置**索引標籤上，hello 下列設定：  
   * **最大數目的裝置每個使用者**： 選取 hello 的使用者可以在 Azure AD 中擁有的裝置數目上限。  如果使用者達到此配額時，它們將無法 tooadd 其他裝置之前無法移除一或多個現有的裝置。
   * **需要 MULTI-FACTOR AUTH tooJOIN 裝置**： 設定使用者是否需要的 tooprovide 第二個驗證因素 toojoin 其裝置 tooAzure AD。 如需有關 Azure Multi-factor Authentication 的詳細資訊，請參閱[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。
   * **使用者可能 AZURE AD JOIN 裝置**： 選取 hello 使用者和群組允許 toojoin 裝置 tooAzure AD。
   * **其他系統管理員在 AZURE AD 加入裝置**: Azure AD Premium 或 hello Enterprise Mobility Suite (EMS)，您可以選擇哪些使用者授與本機系統管理員權限 toohello 裝置。 全域系統管理員和裝置擁有者預設會授與本機系統管理員權限。

<center>![設定裝置註冊](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

設定 Azure AD Join 為您的使用者之後，它們可以連接 tooAzure AD 透過其公司或個人裝置。

以下是您可以使用 tooenable 使用者 tooset 註冊 Azure AD Join hello 三個案例：

* 使用者將公司擁有的裝置直接 tooAzure AD。
* 使用者網域加入公司擁有裝置 toohello 在內部部署 Active Directory，然後將擴充 hello 裝置 tooAzure AD。
* 使用者新增工作或學校帳戶 tooWindows 個人裝置上

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

