---
title: "aaaHow tooget Azure AD 租用戶 |Microsoft 文件"
description: "如何 tooget Azure Active Directory 租用戶註冊和建置應用程式。"
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Tooget Azure Active Directory 的租用戶
在 Azure Active Directory (Azure AD) 中， [租用戶](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) 代表組織。  它是 hello 組織接收及擁有當它註冊 Azure、 Microsoft Intune 或 Office 365 等 Microsoft 雲端服務的 Azure AD 服務的專用執行個體。  每個 Azure AD 租用戶都不同，並與其他 Azure AD 租用戶分開。  

租用戶上存放了 hello 使用者在公司和 hello 其相關資訊的密碼，使用者設定檔資料、 權限，以及等等。  此外，它也會包含群組、 應用程式和相關 tooan 組織和其安全性的其他資訊。

tooallow Azure AD 使用者 toosign tooyour 應用程式中的，您必須在您自己的租用戶中註冊您的應用程式。  在 Azure AD 租用戶中發佈應用程式 **完全免費**。  事實上，大部分的開發人員會建立數個租用戶和應用程式，以供實驗、開發、預備和測試等用途使用。  註冊和使用您的應用程式的組織可以選擇 toopurchase 授權，如果他們想 tootake 進階的目錄功能的優點。

因此，要如何取得 Azure AD 租用戶？  hello 程序可能會很少的不同如果您：

* [具有現有的 Office 365 訂用帳戶](#use-an-existing-office-365-subscription)
* [具有與 Microsoft 帳戶相關聯的現有 Azure 訂用帳戶](#use-an-msa-azure-subscription)
* [具有與組織帳戶相關聯的現有 Azure 訂用帳戶](#use-an-organizational-azure-subscription)
* [在從頭 toostart & 則沒有任何上述 hello](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>使用現有的 Office 365 訂用帳戶
如果您擁有現有的 Office 365 訂用帳戶，就已擁有 Azure AD 租用戶！ 您可以登入 toohello [Azure 入口網站](https://portal.azure.com)與您 O365 帳戶並開始使用 Azure AD。

## <a name="use-an-msa-azure-subscription"></a>使用 MSA Azure 訂用帳戶
如果您先前已使用個別的 Microsoft 帳戶註冊 Azure 訂用帳戶，則您已經有一個租用戶！  當登入 toohello [Azure 入口網站](https://portal.azure.com)，您將會自動登入 tooyour 預設租用戶。 您可用 toouse 此租用戶與您查看符合-但您可能會想 toocreate 組織的系統管理員帳戶。

toodo 因此，請遵循下列步驟。  或者，您可能想 toocreate 新的租用戶，並在下列類似的程序該租用戶中建立系統管理員。

1. 登入 hello [Azure 入口網站](https://portal.azure.com)與個別帳戶
2. 瀏覽 toohello"Azure Active Directory"hello 網站區段 (下在 hello 左的導覽列中，找到**更服務**)
3. 您應該自動登入 toohello 「 預設目錄 」，如果不是您可以切換目錄上您在 hello 右上角中的帳戶名稱即可。
4. 從 hello**快速工作**區段中，選擇**將使用者新增**。
5. 在 hello 新增使用者表單中提供下列詳細資料的 hello:

   * 名稱：(選擇適當的值)
   * 使用者名稱：(為此系統管理員選擇一個使用者名稱)
   * 設定檔: （填寫 hello 名字、 最後一個名稱、 工作職稱及部門適當的值）
   * 角色：全域系統管理員
6. 當您完成 hello 新增使用者表單，並收到 hello hello 新系統管理使用者的暫時密碼，因為您必須使用此新的使用者，在訂單 toochange hello 密碼 toologin 是確定 toorecord 此密碼。 您也可以傳送嗨密碼直接 toohello 使用者，並使用替代電子郵件。
7. 按一下**建立**toocreate hello 新使用者。
8. toochange hello 暫時密碼，登入[https://login.microsoftonline.com](https://login.microsoftonline.com)與此新使用者帳戶並變更 hello 密碼要求時。

## <a name="use-an-organizational-azure-subscription"></a>使用組織的 Azure 訂用帳戶
如果您先前已使用組織帳戶註冊 Azure 訂用帳戶，則您已經有一個租用戶！  在 hello [Azure 入口網站](https://portal.azure.com)，當您瀏覽過，您應該找到租用戶 「 更多服務 」 和 「"Azure Active Directory。  您是免費 toouse 此租用戶，如 調整。

## <a name="start-from-scratch"></a>從頭開始
如果所有上述 hello 胡說八道 tooyou，別擔心。  請瀏覽[https://account.windowsazure.com/organization](https://account.windowsazure.com/organization)與新的組織註冊 Azure toosign。  當您完成 hello 程序之後時，您必須非常 Azure AD 租用戶與您在註冊時選擇向上 hello 網域名稱。  在 hello [Azure 入口網站](https://portal.azure.com)，您可以藉由瀏覽過找到您的租用戶 hello 左側 nav.中的 「 Azure Active Directory"

註冊 Azure 的 hello 程序的一部分，您會需要的 tooprovide 信用卡詳細資料。  您可以放心繼續執行，您將不會被收取在 Azure AD 中發佈應用程式或建立新租用戶的費用。
