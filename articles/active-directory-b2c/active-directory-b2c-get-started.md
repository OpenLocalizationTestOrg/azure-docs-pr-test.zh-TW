---
title: "Azure Active Directory B2C：建立 Azure Active Directory B2C 租用戶 | Microsoft Docs"
description: "Toocreate Azure Active Directory B2C 租用戶的如何主題"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="27a32-103">在 hello Azure 入口網站中建立的 Azure Active Directory B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="27a32-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="27a32-104">編輯 Sipi。</span><span class="sxs-lookup"><span data-stu-id="27a32-104">Edited by Sipi.</span></span>

<span data-ttu-id="27a32-105">本快速入門協助您在數分鐘內建立 Microsoft Azure Active Directory (Azure AD) B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="27a32-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="27a32-106">當您完成時，您可以 B2C 租用戶 toouse 註冊 B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27a32-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27a32-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="27a32-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="27a32-108">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="27a32-108">Log in tooAzure</span></span>

<span data-ttu-id="27a32-109">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="27a32-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="27a32-110">建立 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="27a32-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="27a32-111">B2C 功能無法在您現有的租用戶中啟用。</span><span class="sxs-lookup"><span data-stu-id="27a32-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="27a32-112">您需要 toocreate Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="27a32-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="27a32-113">恭喜，您已建立 Azure Active Directory B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="27a32-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="27a32-114">您是 hello 租用戶全域管理員。</span><span class="sxs-lookup"><span data-stu-id="27a32-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="27a32-115">您可視需要新增其他「全域管理員」。</span><span class="sxs-lookup"><span data-stu-id="27a32-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="27a32-116">tooswitch tooyour 新租用戶中，按一下 hello*管理新的租用戶連結*。</span><span class="sxs-lookup"><span data-stu-id="27a32-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![管理新租用戶連結](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="27a32-118">如果您打算 toouse B2C 租用戶在實際執行應用程式，請閱讀 hello 文章上[預覽 B2C 租用戶與實際執行延展](active-directory-b2c-reference-tenant-type.md)。</span><span class="sxs-lookup"><span data-stu-id="27a32-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="27a32-119">那里已知問題，當您刪除現有的 B2C 租用戶，並重新建立 hello 與相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="27a32-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="27a32-120">您需要 toocreate B2C 租用戶與不同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="27a32-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="27a32-121">連結您的租用戶 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27a32-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="27a32-122">您需要 toolink 您 Azure AD B2C 租用戶 tooyour Azure 訂用帳戶 tooenable B2C 的所有功能，並支付使用費用。</span><span class="sxs-lookup"><span data-stu-id="27a32-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="27a32-123">詳細資訊，讀取 toolearn[本文](active-directory-b2c-how-to-enable-billing.md)。</span><span class="sxs-lookup"><span data-stu-id="27a32-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="27a32-124">如果您不要連結您的 Azure AD B2C 租用戶 tooyour Azure 訂用帳戶，某些功能會封鎖，而且您會看到一則警告訊息 （「 連結的 toothis B2C 租用戶或 hello 訂用帳戶沒有訂用帳戶需要您注意。"） hello B2C 設定中。</span><span class="sxs-lookup"><span data-stu-id="27a32-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="27a32-125">請務必先進行此步驟，然後才將您的應用程式傳送到生產環境。</span><span class="sxs-lookup"><span data-stu-id="27a32-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="27a32-126">輕鬆存取 toosettings</span><span class="sxs-lookup"><span data-stu-id="27a32-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="27a32-127">您也可以存取 hello 刀鋒視窗中輸入`Azure AD B2C`中**搜尋資源**頂端 hello hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="27a32-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="27a32-128">在 hello 結果清單中，選取  **Azure AD B2C** tooaccess hello B2C 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="27a32-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27a32-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27a32-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="27a32-130">在 B2C 租用戶中註冊您的 B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="27a32-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
