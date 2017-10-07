---
title: "aaaAzure AD v2 Windows 桌面快速入門-Config |Microsoft 文件"
description: "Windows Desktop .NET (XAML) 應用程式可取得存取權杖，以及呼叫受 Azure Active Directory v2 端點保護之 API 的方法。"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>新增 hello 應用程式的註冊資訊 tooyour 應用程式
在此步驟中，您需要 tooadd hello 應用程式識別碼 tooyour 專案。

1.  開啟`App.xaml.cs`和取代包含 hello hello 行`ClientId`使用：

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>下一步

[測試和驗證](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
