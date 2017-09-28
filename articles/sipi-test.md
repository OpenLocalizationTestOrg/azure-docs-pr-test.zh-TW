---
title: "Sipi 測試檔案 |Microsoft 文件"
description: "若要檢查 ReadyForTest 相依性的測試檔案"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="f6bbd-103">Sipi 測試檔案</span><span class="sxs-lookup"><span data-stu-id="f6bbd-103">Sipi test file</span></span>

<span data-ttu-id="f6bbd-104">本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="f6bbd-105">當您完成時，應用程式就已註冊完成，以便在 Azure B2C 租用戶中使用。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6bbd-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f6bbd-106">Prerequisites</span></span>

<span data-ttu-id="f6bbd-107">若要建置可接受取用者註冊與登入的應用程式，您必須先使用 Azure Active Directory B2C 租用戶註冊該應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="f6bbd-108">使用 [建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)中概述的步驟來建立您自己的租用戶。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="f6bbd-109">在 Azure 入口網站中從 [Azure AD B2C] 刀鋒視窗建立的應用程式，必須從相同的位置進行管理。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="f6bbd-110">如果您使用 PowerShell 或另一個入口網站編輯 B2C 應用程式，系統則不支援這些應用程式支援且無法搭配 Azure AD B2C 運作。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="f6bbd-111">如需詳細資料，請參閱[ 發生錯誤的應用程式](#faulted-apps)一節。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="f6bbd-112">瀏覽至 B2C 設定</span><span class="sxs-lookup"><span data-stu-id="f6bbd-112">Navigate to B2C settings</span></span>

<span data-ttu-id="f6bbd-113">以 B2C 租用戶的全域管理員身分登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f6bbd-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="f6bbd-114">根據您所註冊的應用程式類型，選擇後續步驟：</span><span class="sxs-lookup"><span data-stu-id="f6bbd-114">Choose next steps based on the application type you are registering:</span></span>
