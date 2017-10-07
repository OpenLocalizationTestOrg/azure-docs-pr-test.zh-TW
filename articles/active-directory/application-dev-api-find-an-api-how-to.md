---
title: "自訂開發的應用程式所需的特定 API 的 aaaHow toofind |Microsoft 文件"
description: "您必須在自訂的 tooaccess 特定 API tooconfigure hello 權限如何開發 Azure AD 應用程式"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>如何 toofind 特定 API 所需的自訂開發的應用程式

存取 tooAPIs 要求設定存取領域和角色。 如果您想 tooexpose 資源應用程式 web 應用程式開發介面 tooclient 應用程式，您需要 tooconfigure 存取領域和角色 hello 應用程式開發介面。 如果您想用戶端應用程式 tooaccess web API，您會需要 tooconfigure 權限 tooaccess hello API hello 應用程式註冊。

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>設定資源應用程式 tooexpose web 應用程式開發介面

當您的 web 應用程式開發介面，公開 （expose） hello 應用程式開發介面會顯示在 hello**選取應用程式開發介面**清單加入權限 tooan 應用程式註冊時。 tooadd 存取領域，請依照下列所述的 hello 步驟[新增存取領域 tooyour 資源應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application)。

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>設定用戶端應用程式 tooaccess web 應用程式開發介面

當您將權限 tooyour 應用程式註冊時，您可以**加入應用程式開發介面存取**tooexposed web Api。 tooaccess web 應用程式開發介面，請遵循所述的 hello 步驟[新增認證或權限 tooaccess web Api](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis)。

## <a name="next-steps"></a>後續步驟

-   [整合應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [了解 hello Azure Active Directory 應用程式資訊清單](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


