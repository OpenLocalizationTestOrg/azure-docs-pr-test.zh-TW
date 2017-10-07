---
title: "Sipi 測試檔案 |Microsoft 文件"
description: "測試檔案 toocheck ReadyForTest 相依性"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="31d58-103">Sipi 測試檔案</span><span class="sxs-lookup"><span data-stu-id="31d58-103">Sipi test file</span></span>

<span data-ttu-id="31d58-104">本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="31d58-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="31d58-105">當您完成時，使用 hello Azure B2C 租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31d58-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31d58-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="31d58-106">Prerequisites</span></span>

<span data-ttu-id="31d58-107">toobuild 接受取用者註冊和登入的應用程式，您必須先 tooregister hello 應用程式與 Azure Active Directory B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="31d58-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="31d58-108">使用 hello 中所述的步驟，以取得自己的租用戶[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="31d58-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="31d58-109">從 Azure AD B2C hello 刀鋒視窗 hello Azure 入口網站中建立的應用程式必須從 hello 管理相同的位置。</span><span class="sxs-lookup"><span data-stu-id="31d58-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="31d58-110">如果您編輯使用 PowerShell 或另一個入口網站的 hello B2C 應用程式，它們會變成不受支援，無法搭配 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="31d58-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="31d58-111">查看詳細資料中 hello[發生錯誤的應用程式](#faulted-apps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="31d58-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="31d58-112">瀏覽 tooB2C 設定</span><span class="sxs-lookup"><span data-stu-id="31d58-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="31d58-113">登入 toohello [Azure 入口網站](https://portal.azure.com/)為 hello hello B2C 租用戶的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="31d58-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="31d58-114">選擇 [下一步] 步驟會依據您所註冊的 hello 應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="31d58-114">Choose next steps based on hello application type you are registering:</span></span>
