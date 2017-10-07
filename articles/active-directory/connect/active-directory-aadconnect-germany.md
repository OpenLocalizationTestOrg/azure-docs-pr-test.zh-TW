---
title: "aaaAzure AD 連線 Microsoft 雲端德國"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您與 Azure AD 整合 Office 365、 Azure 和 SaaS 應用程式的通用識別身分的 tooprovide。"
keywords: "簡介 tooAzure AD Connect，Azure AD Connect 的概觀，什麼是 Azure AD Connect，安裝 active directory，德國，黑色樹系"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="dbf0f-105">Microsoft Cloud Germany 中的 Azure AD Connect - 公開預覽</span><span class="sxs-lookup"><span data-stu-id="dbf0f-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="dbf0f-106">簡介</span><span class="sxs-lookup"><span data-stu-id="dbf0f-106">Introduction</span></span>
<span data-ttu-id="dbf0f-107">Azure AD Connect 可進行內部部署 Active Directory 與 Azure Active Directory 之間的同步處理。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="dbf0f-108">目前，有許多 hello 案例[Microsoft 雲端德國](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx)必須由 hello 運算子。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="dbf0f-109">使用 Microsoft 雲端德國時，您必須知道的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dbf0f-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="dbf0f-110">下列 Url，必須先在 proxy 伺服器進行同步處理 toooccur 成功 hello:</span><span class="sxs-lookup"><span data-stu-id="dbf0f-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="dbf0f-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="dbf0f-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="dbf0f-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="dbf0f-112">*.windows.net</span></span>
  * * <span data-ttu-id="dbf0f-113">憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="dbf0f-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="dbf0f-114">當您登入時 tooyour Azure AD 目錄中時，您必須使用的帳戶 hello onmicrosoft.de 網域中。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="dbf0f-115">下列功能的 hello 便無法使用：</span><span class="sxs-lookup"><span data-stu-id="dbf0f-115">hello following features are not available:</span></span>
  * <span data-ttu-id="dbf0f-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="dbf0f-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="dbf0f-117">自動更新</span><span class="sxs-lookup"><span data-stu-id="dbf0f-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="dbf0f-118">下載</span><span class="sxs-lookup"><span data-stu-id="dbf0f-118">Download</span></span>
<span data-ttu-id="dbf0f-119">您可以下載 Azure AD Connect 從 hello 入口網站中的 hello Azure AD Connect 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="dbf0f-120">使用 hello toolocate hello Azure AD Connect 刀鋒視窗下方的指示。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="dbf0f-121">hello Azure AD Connect 刀鋒伺服器</span><span class="sxs-lookup"><span data-stu-id="dbf0f-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="dbf0f-122">一旦您已登入 toohello Azure 入口網站，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="dbf0f-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="dbf0f-123">移 tooBrowse</span><span class="sxs-lookup"><span data-stu-id="dbf0f-123">Go tooBrowse</span></span>
2. <span data-ttu-id="dbf0f-124">選取 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbf0f-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="dbf0f-125">然後選取 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="dbf0f-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="dbf0f-126">您應該會看到下列 hello:</span><span class="sxs-lookup"><span data-stu-id="dbf0f-126">You should see hello following:</span></span>

![Azure AD Connect 刀鋒視窗](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="dbf0f-128">hello 下表描述顯示在 [hello] 刀鋒視窗中的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="dbf0f-129">Title</span><span class="sxs-lookup"><span data-stu-id="dbf0f-129">Title</span></span> | <span data-ttu-id="dbf0f-130">說明</span><span class="sxs-lookup"><span data-stu-id="dbf0f-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dbf0f-131">同步處理狀態</span><span class="sxs-lookup"><span data-stu-id="dbf0f-131">SYNC STATUS</span></span> |<span data-ttu-id="dbf0f-132">讓您知道已啟用或停用同步處理。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="dbf0f-133">上次同步處理</span><span class="sxs-lookup"><span data-stu-id="dbf0f-133">LAST SYNC</span></span> |<span data-ttu-id="dbf0f-134">hello 上次成功同步處理完成。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="dbf0f-135">同盟網域</span><span class="sxs-lookup"><span data-stu-id="dbf0f-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="dbf0f-136">顯示目前設定的同盟網域的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="dbf0f-137">安裝</span><span class="sxs-lookup"><span data-stu-id="dbf0f-137">Installation</span></span>
<span data-ttu-id="dbf0f-138">tooinstall Azure AD Connect，您可以使用 hello 文件[這裡](active-directory-aadconnect.md#install-azure-ad-connect)。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="dbf0f-139">進階功能和其他資訊</span><span class="sxs-lookup"><span data-stu-id="dbf0f-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="dbf0f-140">如需自訂設定或進階組態的其他資訊和指引，請從 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)著手。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="dbf0f-141">此頁面會提供資訊和連結 tooadditional 指引。</span><span class="sxs-lookup"><span data-stu-id="dbf0f-141">This page provides information and links tooadditional guidance.</span></span>

