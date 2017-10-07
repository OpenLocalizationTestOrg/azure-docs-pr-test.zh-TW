---
title: "Azure Active Directory B2C：自助式密碼重設 | Microsoft Docs"
description: "主題，示範如何 tooset 註冊自助式密碼重設您的取用者，於 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C：為您的取用者設定自助式密碼重設
以 hello 自助式密碼重設功能，您消費者 （已註冊的本機帳戶） 可以重設他們自己的密碼。 這會大幅降低您的支援人員 hello 負擔，特別是當您的應用程式有數百萬個使用以規則為基礎的取用者。 目前僅支援使用已驗證的電子郵件地址做為復原方法。 Hello 未來，我們會加入額外的修復方法 （已驗證的電話號碼、 安全性問題等）。

> [!NOTE]
> 本文件適用於 tooself 服務密碼重設登入原則的 hello 內容中使用。 如果您需要從應用程式叫用的可完全自訂密碼重設原則，請參閱 [這篇文章](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)。
> 
> 

依預設，您的目錄並不會開啟自助式密碼重設。 使用 hello 下列步驟 tooturn 它上：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)為 hello 訂用帳戶管理員。 這是的 hello 相同工作或學校帳戶或 hello 與您用 toocreate 您目錄的 Microsoft 帳戶。
2. 瀏覽 toohello hello hello 左邊的巡覽列上的 Active Directory 延伸模組。
3. 尋找您的目錄下 hello**目錄**索引標籤，然後按一下它。
4. 按一下 hello**設定** 索引標籤。
5. 捲動 toohello**使用者密碼重設原則**> 一節，並切換 hello**使用者啟用密碼重設**太選項**是**。 請注意該 hello**替代電子郵件地址**核取選項，讓它保持原狀。
   
    ![自助式密碼重設](./media/active-directory-b2c-reference-sspr/sspr.png)
6. 按一下**儲存**hello hello 頁底端。 大功告成！

tootest 使用 hello 「 立即執行 」 功能上任何身分識別提供者具有本機帳戶的登入的原則。 Hello 本機帳戶登入頁面上 （在您輸入電子郵件地址和密碼，或使用者名稱和密碼），按一下**無法存取您的帳戶？** tooverify hello 經驗。

> [!NOTE]
> hello 自助式密碼重設頁面可以使用來自訂 hello[公司品牌功能](../active-directory/active-directory-add-company-branding.md)。
> 
> 

