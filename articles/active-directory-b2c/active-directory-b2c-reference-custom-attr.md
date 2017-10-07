---
title: "Azure Active Directory B2C：自訂屬性 | Microsoft Docs"
description: "在您取用者的 Azure Active Directory B2C toocollect 資訊 toouse 自訂屬性是如何"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active Directory B2C： 使用取用者的自訂屬性 toocollect 資訊
您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建資訊 (屬性)：名字、姓氏、城市、郵遞區號及其他屬性。 不過，每個消費者導向應用程式都有唯一需求與取用者的哪些屬性 toogather 上。 您可以使用 Azure AD B2C，擴充 hello 組儲存在每個取用者帳戶上的屬性。 您可以建立自訂的屬性上 hello [Azure 入口網站](https://portal.azure.com/)並將它用於註冊的原則，如下所示。 您也可以讀取和寫入這些屬性使用 hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)。

> [!NOTE]
> 自訂屬性會使用 [Azure AD Graph API 目錄結構描述擴充](https://msdn.microsoft.com/library/azure/dn720459.aspx)。
> 
> 

## <a name="create-a-custom-attribute"></a>建立自訂屬性
1. [遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。
2. 按一下 [使用者屬性] 。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供**名稱**hello 自訂屬性 (例如，"ShoeSize")，並選擇性地**描述**。 按一下 [建立] 。
   
   > [!NOTE]
   > 只有 hello"String"**資料型別**目前可用。
   > 
   > 

hello 自訂屬性現已推出的 hello 清單**使用者屬性**，與在您註冊的原則中使用。

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>在您的註冊原則中使用自訂屬性
1. [遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。
2. 按一下 [註冊原則] 。
3. 按一下 註冊原則 (例如，"B2C_1_SiUp 」) tooopen 它。 按一下**編輯**在 hello hello 刀鋒視窗最上方。
4. 按一下**註冊屬性**和選取 hello 自訂屬性 (例如，"ShoeSize")。 按一下 [確定] 。
5. 按一下**應用程式宣告**和選取 hello 自訂屬性。 按一下 [確定] 。
6. 按一下**儲存**在 hello hello 刀鋒視窗最上方。

您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。 您現在應該看到 「 ShoeSize"hello 註冊時，取用者期間所收集的屬性清單中，並查看它的 hello 語彙基元傳送後 tooyour 應用程式。

## <a name="notes"></a>注意事項
* 除了註冊原則，自訂屬性也可以使用於註冊或登入原則和設定檔編輯原則。
* 自訂屬性有已知的限制。 當這個選項只有在任何原則中，使用它的第一次建立 hello 不加入 toohello 清單**使用者屬性**。

