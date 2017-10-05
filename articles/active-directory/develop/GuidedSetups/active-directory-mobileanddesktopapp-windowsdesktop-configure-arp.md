---
title: "Azure AD v2 Windows Desktop 快速入門 - 設定 | Microsoft Docs"
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
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="54783-103">將應用程式的註冊資訊新增到您的應用程式</span><span class="sxs-lookup"><span data-stu-id="54783-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="54783-104">在這個步驟中，您需要將應用程式識別碼新增到您的專案。</span><span class="sxs-lookup"><span data-stu-id="54783-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="54783-105">開啟 `App.xaml.cs` 並將包含 `ClientId` 的那一行取代為：</span><span class="sxs-lookup"><span data-stu-id="54783-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="54783-106">下一步</span><span class="sxs-lookup"><span data-stu-id="54783-106">What is Next</span></span>

[<span data-ttu-id="54783-107">測試和驗證</span><span class="sxs-lookup"><span data-stu-id="54783-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)