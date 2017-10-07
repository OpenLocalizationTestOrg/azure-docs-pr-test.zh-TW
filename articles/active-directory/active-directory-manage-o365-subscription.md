---
title: "您在 Azure 中的 Office 365 訂閱的 aaaManage hello 目錄 |Microsoft 文件"
description: "管理 Azure Active Directory 和 hello Azure 傳統入口網站使用 Office 365 訂用帳戶目錄"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>管理 Office 365 訂用帳戶在 Azure 中的 hello 目錄
本文說明如何 toomanage Office 365 訂用帳戶，使用 hello Azure 傳統入口網站建立的目錄。 您必須是 hello 服務系統管理員或共同管理員的 Azure 訂用帳戶 toosign toohello Azure 傳統入口網站中。 如果您尚未擁有 Azure 訂用帳戶，您可以立即註冊 [免費 30 天試用版](https://azure.microsoft.com/trial/get-started-active-directory/) ，並使用此連結在 5 分鐘內部署第一個雲端解決方案。 確定 toouse hello 工作或學校帳戶，您使用 toosign tooOffice 365。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

完成 hello Azure 訂用帳戶之後，您可以登入 toohello Azure 傳統入口網站，並存取 Azure 服務。 按一下 hello Active Directory 延伸模組 toomanage hello 驗證 Office 365 使用者的相同目錄。

如果您已經有 Azure 訂用帳戶，就也簡單 hello 程序 toomanage 的其他目錄。 在此範例中，Michael Smith 可能擁有適用於 Contoso.com 的 Office 365 訂用帳戶。他也擁有使用其 Microsoft 帳戶 msmith@hotmail.com 所註冊的 Azure 訂用帳戶。在此情況下，他要管理兩個目錄。

| 訂用帳戶 | Office 365 | Azure |
| --- | --- | --- |
|   顯示名稱 |Contoso |預設 Azure Active Directory (Azure AD) 目錄 |
|   網域名稱 |contoso.com |msmithhotmail.onmicrosoft.com |

他會登入 tooAzure 使用 Microsoft 帳戶，以便他可以啟用 Azure AD 功能，例如多重要素驗證時，他想 toomanage hello 使用者身分在 hello Contoso 目錄中。 下列圖表中的 hello 有助於 tooillustrate hello 程序。

![圖表 toomanage 兩個獨立的目錄](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

在此情況下，hello 兩個目錄彼此各自獨立的。

## <a name="toomanage-two-independent-directories"></a>toomanage 兩個獨立的目錄
若要針對 Michael Smith toomanage 兩個目錄時登入為 tooAzure msmith@hotmail.com，他必須完成下列步驟的 hello:

> [!NOTE]
> 只有當使用者使用 Microsoft 帳戶登入時，才能完成下列步驟。 如果 hello 使用者登入工作或學校帳戶，hello 選項太**使用現有目錄**無法使用。 工作或學校帳戶可以只由其主目錄 （也就是 hello 目錄 hello 工作或學校帳戶的儲存位置，而該 hello 公司或學校擁有） 進行驗證。
>
>

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)為msmith@hotmail.com。
2. 按一下 [新增]  >  [應用程式服務]  >  [Active Directory]  >  [目錄]  >  [自訂建立]。
3. 按一下 使用現有的目錄中，而且選取 hello**我已準備好立即登出的 toobe**核取方塊。
4. 登入 toohello Azure 傳統入口網站以 Contoso.onmicrosoft.com 的全域管理員身分 (例如， msmith@contoso.com)。
5. 當系統提示您太**搭配 Azure 使用 hello Contoso 目錄？**，按一下 **繼續**。
6. 按一下 [ **立即登出**]。
7. 登入 toohello Azure 傳統入口網站，做為msmith@hotmail.com。 hello Contoso 目錄和 hello 預設目錄會出現在 hello Active Directory 延伸模組。

完成這些步驟之後, msmith@hotmail.com hello Contoso 目錄中的全域系統管理員。

## <a name="tooadminister-resources-as-hello-global-admin"></a>hello 全域管理員 tooadminister 資源
現在讓我們假設 Jane Doe 需要管理的網站，和相關聯的資料庫資源 hello Azure 訂用帳戶msmith@hotmail.com。她可以這麼做，Michael Smith 必須 toocomplete 下列額外步驟：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello Azure 訂用帳戶使用 hello 服務系統管理員帳戶 (在此範例中， msmith@hotmail.com)。
2. 傳送嗨訂用帳戶 toohello Contoso 目錄： 按一下**設定** > **訂閱**> 選取 hello 訂用帳戶 >**編輯目錄**> 選取**Contoso (Contoso.com)**。 Hello 傳輸、 工作或學校的一部分移除共同管理員的 hello 訂用帳戶的帳戶。
3. Jane Doe 加入為 hello 訂用帳戶的共同管理員： 按一下**設定** > **管理員**> 選取 hello 訂用帳戶 >**新增**> 類型**JohnDoe@Contoso.com**.

## <a name="next-steps"></a>後續步驟
如需 hello 訂用帳戶與目錄之間的關聯性的詳細資訊，請參閱[訂用帳戶的目錄相關聯的方式](active-directory-how-subscriptions-associated-directory.md)。
