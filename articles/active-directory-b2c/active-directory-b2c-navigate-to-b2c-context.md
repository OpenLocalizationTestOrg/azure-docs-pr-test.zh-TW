---
title: "Azure Active Directory B2C： 切換 tooa B2C 租用戶 |Microsoft 文件"
description: "Tooswitch 放入您的 Active Directory B2C 的 hello 內容的租用戶"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 572f9ab283ecac68d284bb04fdfc98575bcf9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="switching-tooyour-azure-ad-b2c-tenant"></a><span data-ttu-id="2c685-103">切換 tooyour Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="2c685-103">Switching tooyour Azure AD B2C tenant</span></span>

<span data-ttu-id="2c685-104">在訂單 tooconfigure Azure AD B2C，您會需要 toobe hello 內容，您的 Azure AD B2C 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="2c685-104">In order tooconfigure Azure AD B2C, you need toobe in hello context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="2c685-105">登入您的 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="2c685-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="2c685-106">toonavigate tooyour Azure AD B2C 租用戶中，您必須 hello Azure AD B2C 租用戶的全域管理員身分登入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2c685-106">toonavigate tooyour Azure AD B2C tenant, you must be logged into hello Azure portal as a global administrator of hello Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="2c685-107">登入 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2c685-107">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="2c685-108">按一下您的電子郵件地址或 hello 右上角中的圖片，以切換租用戶。</span><span class="sxs-lookup"><span data-stu-id="2c685-108">Switch tenants by clicking your email address or picture in hello top-right corner.</span></span>
1. <span data-ttu-id="2c685-109">在 hello`Directory`隨即出現，且想 toomanage 選取 hello Azure AD B2C 租用戶的清單。</span><span class="sxs-lookup"><span data-stu-id="2c685-109">In hello `Directory` list that appears, select hello Azure AD B2C tenant that you wish toomanage.</span></span>

<span data-ttu-id="2c685-110">hello Azure 入口網站會重新整理。</span><span class="sxs-lookup"><span data-stu-id="2c685-110">hello Azure Portal will refresh.</span></span>  <span data-ttu-id="2c685-111">現在您已登入您的 Azure AD B2C 租用戶的 hello 內容中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2c685-111">Now you are signed into hello Azure Portal in hello context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-toohello-b2c-features-blade"></a><span data-ttu-id="2c685-112">瀏覽 toohello B2C 功能刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="2c685-112">Navigate toohello B2C features blade</span></span>

1. <span data-ttu-id="2c685-113">按一下**瀏覽**hello 左側導覽上。</span><span class="sxs-lookup"><span data-stu-id="2c685-113">Click **Browse** on hello left hand navigation.</span></span>
1. <span data-ttu-id="2c685-114">按一下**> 更多服務**然後搜尋`Azure AD B2C`hello 左側的導覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="2c685-114">Click **> More services** and then search for `Azure AD B2C` in hello left navigation pane.</span></span>  <span data-ttu-id="2c685-115">(toopin tooyour 左側的開始面板，按一下 Azure AD B2C hello 星狀 toohello 左邊)</span><span class="sxs-lookup"><span data-stu-id="2c685-115">(toopin tooyour left-hand Startboard, click hello star toohello left of Azure AD B2C)</span></span>
1. <span data-ttu-id="2c685-116">按一下**Azure AD B2C** tooaccess hello B2C 功能刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c685-116">Click **Azure AD B2C** tooaccess hello B2C features blade.</span></span>
   
    ![瀏覽 tooB2C 功能刀鋒視窗的螢幕擷取畫面](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="2c685-118">您需要 toobe hello B2C 租用戶 toobe 無法 tooaccess hello B2C 功能刀鋒視窗的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="2c685-118">You need toobe a Global Administrator of hello B2C tenant toobe able tooaccess hello B2C features blade.</span></span> <span data-ttu-id="2c685-119">其他租用戶的全域管理員或所有租用戶的使用者均無法存取。</span><span class="sxs-lookup"><span data-stu-id="2c685-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="2c685-120">您可以使用 hello 右上角的 hello Azure 入口網站中的 hello 租用戶切換器，以切換 tooyour B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2c685-120">You can switch tooyour B2C tenant by using hello tenant switcher in hello top right corner of hello Azure portal.</span></span>
