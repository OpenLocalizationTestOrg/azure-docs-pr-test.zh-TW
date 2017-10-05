---
title: "將個人裝置加入至您的組織 | Microsoft Docs"
description: "說明使用者要如何向他們的公司網路註冊其個人的 Windows 10 裝置，同時也提供 BYOD 案例的部署步驟。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a>將個人裝置加入至您的組織
## <a name="to-join-a-windows-10-device-to-your-organization"></a>將 Windows 10 裝置加入至您的組織
1. 在 [開始] 功能表中，選取 [設定]。
2. 選取 [帳戶]，然後按一下 [您的帳戶]。
3. 按一下 [ **加入工作或學校帳戶**]，然後在您的組織帳戶中進行輸入。
4. 在您組織的登入頁面上，輸入您的使用者名稱和密碼，然後按一下 [ **確定**]。
5. 接著系統會提示您完成多重要素驗證挑戰。 (這項挑戰可由 IT 管理員設定)。
6. Azure Active Directory (Azure AD) 會檢查這個裝置是否需要註冊行動裝置管理。
7. 接著 Windows 會在 Azure AD 的組織目錄中註冊裝置，並註冊行動裝置管理 (如果適用)。
8. 如果您是受管理的使用者，Windows 會透過自動登入將您導向桌面。
9. 如果您是同盟使用者，便會將您導向 Windows 登入畫面，以輸入您的認證。

## <a name="additional-information"></a>其他資訊
* [適合企業使用的 Windows 10：使用裝置工作的方式](active-directory-azureadjoin-windows10-devices-overview.md)
* [透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能](active-directory-azureadjoin-user-upgrade.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [將已加入網域裝置連接到 Azure AD 以體驗 Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

