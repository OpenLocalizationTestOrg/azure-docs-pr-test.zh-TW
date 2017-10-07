---
title: "設定從 Azure AD 與 Windows 10 裝置的 aaaSet |Microsoft 文件"
description: "說明使用者如何加入 tooAzure AD 透過 hello 設定功能表。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>從 [設定] 使用 Azure AD 設定 Windows 10 裝置
如果您已經使用 Windows 7 或 Windows 8 與電腦或裝置已升級的 tooWindows 10，您可以加入 tooAzure Active Directory (Azure AD) 透過 hello 設定功能表。

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD hello 設定 功能表
1. 從 hello**啟動**功能表上，按一下 hello**設定**常用鍵。
2. 從 [設定] 中選取 [系統]->[關於]->[加入 Azure AD]。
   
   <center>
   ![加入 Azure AD 設定 功能表中 hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. 按一下**繼續**hello Azure AD Join 訊息視窗中。
   
   <center>
   ![加入 Azure AD 訊息視窗](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. 提供您的登入認證。 此登入體驗將會包含所需的 toocomplete 驗證的所有 hello 步驟。 如果您是同盟租用戶的一部分，您的系統管理員將提供您組織所裝載的 hello 同盟體驗。
   <center>
   ![提供登入認證](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. 如果您的組織已加入 tooAzure AD 設定 Azure Multi-factor Authentication Server，提供 hello 第二個因素，才能繼續。
6. 按一下**接受**上 hello**允許管理此裝置 toobe**螢幕。
7. 您應該會看到 「 您的裝置現在是 Azure AD 中的聯結的 tooyour 組織"hello 訊息。

## <a name="additional-information"></a>其他資訊
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)

