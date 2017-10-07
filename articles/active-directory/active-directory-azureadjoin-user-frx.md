---
title: "安裝程式期間使用 Azure AD 的新裝置 aaaSet |Microsoft 文件"
description: "說明使用者如何在初次執行體驗期間設定 Azure AD Join 的主題。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>設定期間使用 Azure AD 設定新裝置
在 Windows 10 中，使用者可以 hello 初次執行體驗 (FRX) 加入其裝置 tooAzure Active Directory (Azure AD)。 這可讓組織 toodistribute 壓縮包裝的裝置 tootheir 員工或學生，或讓使用者選擇他們自己的裝置 (CYOD)。
如果裝置上安裝 Windows 10 專業版或 Windows 10 Enterprise edition，則 hello 遇到公司擁有的裝置的預設值 toohello 安裝程序。

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin 裝置 tooAzure AD
1. 當您開啟新裝置，並啟動 hello 安裝程序時，您應該會看到 hello**準備**訊息。 請遵循您的裝置 hello 提示 tooset。
2. 首先，自訂您的地區及語言， 接著，接受 hello Microsoft 軟體授權條款。
   ![自訂您的區域](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. 選取要用於連接 toohello 網際網路 toouse hello 網路。
4. 選取您是使用自己的裝置，還是公司擁有的裝置。 如果屬公司所擁有，請按一下**此裝置隸屬 toomy 組織**。 這樣會啟動 hello 體驗 Azure AD Join。 如果您使用的是 Windows 10 專業版，就會看到以下畫面。
   <center>
   ![[誰是這部電腦的擁有者] 畫面](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. 輸入由您的組織所提供 tooyou hello 認證。
   <center>
   ![登入畫面](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. 當您輸入使用者名稱之後，系統就會在 Azure AD 中找到相符的租用戶。 如果您是在同盟網域，您將會重新導向的 tooyour 在內部部署安全權杖服務 (STS) 伺服器--例如，Active Directory Federation Services (AD FS)。
7. 如果您是在非同盟網域的使用者，請直接在 hello Azure AD 主控的頁面上輸入認證。 如果您的組織之前已設定公司商標，此時您也會看到組織的標誌及支援文字。
8. 系統會提示您進行 Multi-Factor Authentication 查問。 IT 系統管理員可以設定這項查問。
9. Azure AD 會查看該使用者/裝置是否需要在行動裝置管理 (MDM) 中註冊。
10. Windows Azure AD 中註冊 hello 組織目錄中的 hello 裝置和註冊行動裝置管理 中，如果適當的話。
11. 如果您是受管理的使用者，Windows 會帶領您 toohello 桌面透過 hello 自動登入程序。
12. 如果您是同盟的使用者，您會被導向 toohello Windows 登入畫面 tooenter 您的認證。

> [!NOTE]
> 若要加入內部部署 Windows Server Active Directory 網域中 hello Windows 不支援全新的體驗。 因此，如果您計劃 toojoin 電腦 tooa 網域，您應該選取 hello 連結**使用本機帳戶設定 windows<**改為。 然後您可以在您的電腦上聯結 hello 網域從 hello 設定，為 「 您已經完成之前。
> 
> 

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

