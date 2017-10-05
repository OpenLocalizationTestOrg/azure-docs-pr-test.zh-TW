---
title: "Azure AD Connect：預覽版功能 | Microsoft Docs"
description: "本主題詳細描述 Azure AD Connect 中位於預覽的功能。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="e4cca-103">有關預覽中之功能的其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="e4cca-103">More details about features in preview</span></span>
<span data-ttu-id="e4cca-104">本主題描述如何使用預覽中目前的功能。</span><span class="sxs-lookup"><span data-stu-id="e4cca-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="e4cca-105">群組回寫</span><span class="sxs-lookup"><span data-stu-id="e4cca-105">Group writeback</span></span>
<span data-ttu-id="e4cca-106">選用功能中的群組回寫選項可讓您將「Office 365 群組」回寫至已安裝 Exchange 的樹系。</span><span class="sxs-lookup"><span data-stu-id="e4cca-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="e4cca-107">這是一律在雲端中控制的群組。</span><span class="sxs-lookup"><span data-stu-id="e4cca-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="e4cca-108">如果您有 Exchange 內部部署，則可以將這些群組回寫到內部部署，讓具有內部部署 Exchange 信箱的使用者可以從這些群組傳送和接收電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e4cca-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="e4cca-109">如需有關 Office 365 群組及其使用方式的詳細資訊，可在 [這裡](http://aka.ms/O365g)找到。</span><span class="sxs-lookup"><span data-stu-id="e4cca-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="e4cca-110">Office 365 群組將會在內部部署 AD DS 中顯示為通訊群組。</span><span class="sxs-lookup"><span data-stu-id="e4cca-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="e4cca-111">您的內部部署 Exchange 伺服器必須是 Exchange 2013 累積更新 8 (2015 年 3 月發行) 或 Exchange 2016，才能辨識這個新的群組類型。</span><span class="sxs-lookup"><span data-stu-id="e4cca-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="e4cca-112">**預覽期間的注意事項**</span><span class="sxs-lookup"><span data-stu-id="e4cca-112">**Notes during the preview**</span></span>

* <span data-ttu-id="e4cca-113">目前在預覽中不會填入通訊錄屬性。</span><span class="sxs-lookup"><span data-stu-id="e4cca-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="e4cca-114">若沒有此屬性，群組就不會顯示在 GAL 中。</span><span class="sxs-lookup"><span data-stu-id="e4cca-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="e4cca-115">若要填入此屬性，最簡單的方法是使用 Exchange PowerShell Cmdlet `update-recipient`。</span><span class="sxs-lookup"><span data-stu-id="e4cca-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="e4cca-116">只有使用 Exchange 結構描述的樹系才是群組的有效目標。</span><span class="sxs-lookup"><span data-stu-id="e4cca-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="e4cca-117">如果沒有偵測到 Exchange，則會無法啟用群組回寫功能。</span><span class="sxs-lookup"><span data-stu-id="e4cca-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="e4cca-118">目前只支援單一樹系 Exchange 組織部署。</span><span class="sxs-lookup"><span data-stu-id="e4cca-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="e4cca-119">如果您的內部部署環境中有多個 Exchange 組織，則需要擁有內部部署 GALSync 解決方案才能讓這些群組出現在其他樹系中。</span><span class="sxs-lookup"><span data-stu-id="e4cca-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="e4cca-120">群組回寫功能無法處理安全性群組或通訊群組。</span><span class="sxs-lookup"><span data-stu-id="e4cca-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="e4cca-121">需要 Azure AD Premium 的訂用帳戶才能使用群組回寫功能。</span><span class="sxs-lookup"><span data-stu-id="e4cca-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="e4cca-122">使用者回寫</span><span class="sxs-lookup"><span data-stu-id="e4cca-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e4cca-123">在 Azure AD Connect 的 2015 年 8 月更新中，已移除使用者的回寫預覽功能。</span><span class="sxs-lookup"><span data-stu-id="e4cca-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="e4cca-124">如果已啟用它，則您應該停用這個功能。</span><span class="sxs-lookup"><span data-stu-id="e4cca-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e4cca-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4cca-125">Next steps</span></span>
<span data-ttu-id="e4cca-126">繼續[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="e4cca-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="e4cca-127">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="e4cca-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
