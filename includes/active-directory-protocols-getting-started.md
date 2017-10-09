---
title: "aaaAzure AD.NET 通訊協定概觀 |Microsoft 文件"
description: "如何 toouse HTTP 訊息 tooauthorize 存取 tooweb 應用程式和 web 應用程式開發介面使用 Azure AD 租用戶中。"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## 向 AD 租用戶註冊應用程式
首先，您將需要 tooregister 您的應用程式與 Azure Active Directory (Azure AD) 租用戶。 這會讓您的應用程式的應用程式識別碼，以及啟用它 tooreceive token。

* 登入 toohello [Azure 入口網站](https://portal.azure.com)。
* 在您的帳戶在 hello 右上角的 hello 頁面，即可選擇 Azure AD 租用戶。
* Hello 左側導覽窗格中，按一下**Azure Active Directory**。
* 按一下 [應用程式註冊]，然後按一下 [新增]。
* 依照 hello 提示，並建立新的應用程式。 在本教學課程中，不論它是 Web 應用程式或原生應用程式都沒關係，但如果您想要 Web 應用程式或原生應用程式的特定範例，請查看我們的[快速入門](../articles/active-directory/develop/active-directory-developers-guide.md)。
  * Web 應用程式，提供 hello**登入 URL**這是應用程式的 hello 基底 URL，使用者可以登入在例如`http://localhost:12345`。
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 原生應用程式，提供**重新導向 URI**，哪些 Azure AD 將會使用 tooreturn 權杖回應。 輸入值特定 tooyour 應用程式。 例如`http://MyFirstAADApp`
* 當您完成註冊之後時，Azure AD 會指派您的應用程式的唯一用戶端識別碼、 hello 應用程式識別碼。 您將需要這個值在 hello 下一步 區段中，因此將它複製從 hello 應用程式頁面。
