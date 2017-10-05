---
title: "Azure Active Directory B2C：建立 Azure Active Directory B2C 租用戶 | Microsoft Docs"
description: "有關如何建立 Azure Active Directory B2C 租用戶的主題"
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
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="3daba-103">在 Azure 入口網站中建立 Azure Active Directory B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="3daba-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="3daba-104">編輯 Sipi。</span><span class="sxs-lookup"><span data-stu-id="3daba-104">Edited by Sipi.</span></span>

<span data-ttu-id="3daba-105">本快速入門協助您在數分鐘內建立 Microsoft Azure Active Directory (Azure AD) B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3daba-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="3daba-106">完成後，您便有 B2C 租用戶可用於註冊 B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3daba-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3daba-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="3daba-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="3daba-108">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="3daba-108">Log in to Azure</span></span>

<span data-ttu-id="3daba-109">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3daba-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="3daba-110">建立 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="3daba-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="3daba-111">B2C 功能無法在您現有的租用戶中啟用。</span><span class="sxs-lookup"><span data-stu-id="3daba-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="3daba-112">您必須建立 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3daba-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="3daba-113">恭喜，您已建立 Azure Active Directory B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3daba-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="3daba-114">您是租用戶的「全域管理員」。</span><span class="sxs-lookup"><span data-stu-id="3daba-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="3daba-115">您可視需要新增其他「全域管理員」。</span><span class="sxs-lookup"><span data-stu-id="3daba-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="3daba-116">若要切換到新的租用戶，請按一下*管理新租用戶連結*。</span><span class="sxs-lookup"><span data-stu-id="3daba-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![管理新租用戶連結](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="3daba-118">如果您打算將 B2C 租用戶用於生產應用程式，請閱讀 [生產級別租用戶與預覽 B2C 租用戶](active-directory-b2c-reference-tenant-type.md)一文。</span><span class="sxs-lookup"><span data-stu-id="3daba-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="3daba-119">當您刪除現有的 B2C 租用戶並使用相同的網域名稱加以重建時，會發生已知的問題。</span><span class="sxs-lookup"><span data-stu-id="3daba-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="3daba-120">您需要使用不同的網域名稱建立 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3daba-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="3daba-121">將您的租用戶連結至您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3daba-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="3daba-122">您必須將您的 Azure AD B2C 租用戶連結至您的 Azure 訂用帳戶，才能啟用所有的 B2C 功能，並支付使用費用。</span><span class="sxs-lookup"><span data-stu-id="3daba-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="3daba-123">若要深入了解，請閱讀[這篇文章](active-directory-b2c-how-to-enable-billing.md)。</span><span class="sxs-lookup"><span data-stu-id="3daba-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="3daba-124">如果您未將 Azure AD B2C 租用戶連結到您的 Azure 訂用帳戶，有些功能會遭到封鎖，您將會在 B2C 設定中看見警告訊息 (「沒有訂用帳戶與此 B2C 租用戶連結，或訂用帳戶需要您的注意。」)。</span><span class="sxs-lookup"><span data-stu-id="3daba-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="3daba-125">請務必先進行此步驟，然後才將您的應用程式傳送到生產環境。</span><span class="sxs-lookup"><span data-stu-id="3daba-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="3daba-126">輕鬆存取設定</span><span class="sxs-lookup"><span data-stu-id="3daba-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="3daba-127">您也可以在入口網站頂端的 [搜尋資源] 中尋入 `Azure AD B2C` 來存取刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3daba-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="3daba-128">在結果清單中選取 [Azure AD B2C] 以存取 B2C 設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3daba-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3daba-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3daba-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3daba-130">在 B2C 租用戶中註冊您的 B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="3daba-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
