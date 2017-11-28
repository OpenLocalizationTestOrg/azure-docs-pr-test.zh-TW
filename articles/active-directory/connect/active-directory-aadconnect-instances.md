---
title: "Azure AD Connect︰同步服務執行個體 | Microsoft Docs"
description: "本頁記載 Azure AD 執行個體的特殊考量。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="1b94c-103">Azure AD Connect：執行個體的特殊考量</span><span class="sxs-lookup"><span data-stu-id="1b94c-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="1b94c-104">Azure AD Connect 最常搭配 hello 全球執行個體的 Azure AD 和 Office 365。</span><span class="sxs-lookup"><span data-stu-id="1b94c-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="1b94c-105">但還有其他執行個體，而它們有不同的 URL 需求和其他特殊考量。</span><span class="sxs-lookup"><span data-stu-id="1b94c-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="1b94c-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="1b94c-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="1b94c-107">hello [Microsoft 雲端德國](http://www.microsoft.de/cloud-deutschland)是統領雲端由德文的資料信任項。</span><span class="sxs-lookup"><span data-stu-id="1b94c-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="1b94c-108">在 [proxy 伺服器的 Url tooopen</span><span class="sxs-lookup"><span data-stu-id="1b94c-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="1b94c-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="1b94c-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="1b94c-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="1b94c-110">\*.windows.net</span></span> |
| <span data-ttu-id="1b94c-111">+憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="1b94c-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="1b94c-112">當您登入 tooyour Azure AD 租用戶時，您必須在 hello onmicrosoft.de 網域中使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b94c-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="1b94c-113">目前不存在於 hello Microsoft 雲端德國的功能：</span><span class="sxs-lookup"><span data-stu-id="1b94c-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="1b94c-114">無法使用 **Azure AD Connect Health**。</span><span class="sxs-lookup"><span data-stu-id="1b94c-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="1b94c-115">無法使用「自動更新」。</span><span class="sxs-lookup"><span data-stu-id="1b94c-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="1b94c-116">**密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。</span><span class="sxs-lookup"><span data-stu-id="1b94c-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="1b94c-117">無法使用其他 Azure AD Premium 服務。</span><span class="sxs-lookup"><span data-stu-id="1b94c-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="1b94c-118">Microsoft Azure Government 雲端</span><span class="sxs-lookup"><span data-stu-id="1b94c-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="1b94c-119">hello [Microsoft Azure 政府雲端](https://azure.microsoft.com/features/gov/)是美國政府的雲端。</span><span class="sxs-lookup"><span data-stu-id="1b94c-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="1b94c-120">此雲端是以舊版的 DirSync 提供支援。</span><span class="sxs-lookup"><span data-stu-id="1b94c-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="1b94c-121">從 Azure AD connect 組建 1.1.180 hello 新一代 hello 雲端的支援。</span><span class="sxs-lookup"><span data-stu-id="1b94c-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="1b94c-122">這個層代使用僅限美國根據的端點，且有不同的 Url tooopen 清單中您的 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1b94c-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="1b94c-123">在 [proxy 伺服器的 Url tooopen</span><span class="sxs-lookup"><span data-stu-id="1b94c-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="1b94c-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1b94c-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="1b94c-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="1b94c-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="1b94c-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1b94c-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="1b94c-127">+憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="1b94c-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="1b94c-128">Azure AD Connect 不能 tooautomatically 偵測 Azure AD 租用戶位於 hello 政府雲端。</span><span class="sxs-lookup"><span data-stu-id="1b94c-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="1b94c-129">相反地，您需要下列動作，當您安裝 Azure AD Connect tootake hello。</span><span class="sxs-lookup"><span data-stu-id="1b94c-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="1b94c-130">啟動 hello Azure AD Connect 的安裝。</span><span class="sxs-lookup"><span data-stu-id="1b94c-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="1b94c-131">當您看見 hello 應該 tooaccept hello 使用者授權合約的第一頁時，不會繼續，但保留 hello 安裝精靈執行。</span><span class="sxs-lookup"><span data-stu-id="1b94c-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="1b94c-132">啟動 regedit 並變更登錄機碼 hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello 值`2`。</span><span class="sxs-lookup"><span data-stu-id="1b94c-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="1b94c-133">請返回 toohello Azure AD Connect 的安裝精靈、 接受 hello 使用者授權合約，並繼續。</span><span class="sxs-lookup"><span data-stu-id="1b94c-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="1b94c-134">在安裝期間，請確定 toouse hello**自訂組態**安裝路徑 （以及不快速安裝）。</span><span class="sxs-lookup"><span data-stu-id="1b94c-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="1b94c-135">然後，繼續如往常般 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="1b94c-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="1b94c-136">目前不存在於 hello Microsoft Azure 政府雲端的功能：</span><span class="sxs-lookup"><span data-stu-id="1b94c-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="1b94c-137">無法使用 **Azure AD Connect Health**。</span><span class="sxs-lookup"><span data-stu-id="1b94c-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="1b94c-138">無法使用「自動更新」。</span><span class="sxs-lookup"><span data-stu-id="1b94c-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="1b94c-139">**密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。</span><span class="sxs-lookup"><span data-stu-id="1b94c-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="1b94c-140">無法使用其他 Azure AD Premium 服務。</span><span class="sxs-lookup"><span data-stu-id="1b94c-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b94c-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b94c-141">Next steps</span></span>
<span data-ttu-id="1b94c-142">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="1b94c-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
