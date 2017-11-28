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
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="f3a25-103">有關預覽中之功能的其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="f3a25-103">More details about features in preview</span></span>
<span data-ttu-id="f3a25-104">本主題描述如何 toouse 功能目前在預覽中。</span><span class="sxs-lookup"><span data-stu-id="f3a25-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="f3a25-105">群組回寫</span><span class="sxs-lookup"><span data-stu-id="f3a25-105">Group writeback</span></span>
<span data-ttu-id="f3a25-106">hello 選項用於群組回寫中的選擇性功能可讓您 toowriteback **Office 365 群組**tooa 樹系安裝 exchange。</span><span class="sxs-lookup"><span data-stu-id="f3a25-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="f3a25-107">這是永遠 hello 雲端中受控制的群組。</span><span class="sxs-lookup"><span data-stu-id="f3a25-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="f3a25-108">如果您有 Exchange 內部部署，然後您可以撰寫回這些群組 tooon 單位以便與在內部部署 Exchange 信箱的使用者可以傳送和接收電子郵件從這些群組。</span><span class="sxs-lookup"><span data-stu-id="f3a25-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="f3a25-109">Office 365 群組和如何 toouse 它們可以找到詳細資訊[這裡](http://aka.ms/O365g)。</span><span class="sxs-lookup"><span data-stu-id="f3a25-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="f3a25-110">Office 365 群組將會在內部部署 AD DS 中顯示為通訊群組。</span><span class="sxs-lookup"><span data-stu-id="f3a25-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="f3a25-111">在內部部署 Exchange 伺服器必須在 Exchange 2013 累積更新 8 （2015 年 3 月發行） 或 Exchange 2016 toorecognize 這個新的群組類型。</span><span class="sxs-lookup"><span data-stu-id="f3a25-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="f3a25-112">**Hello 預覽期間的附註**</span><span class="sxs-lookup"><span data-stu-id="f3a25-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="f3a25-113">目前不在 hello 預覽中才會填入 hello 地址通訊錄屬性。</span><span class="sxs-lookup"><span data-stu-id="f3a25-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="f3a25-114">沒有這個屬性，hello 群組不是顯示在 hello GAL。</span><span class="sxs-lookup"><span data-stu-id="f3a25-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="f3a25-115">hello 最簡單的方式 toopopulate 這個屬性是 toouse hello Exchange PowerShell cmdlet `update-recipient`。</span><span class="sxs-lookup"><span data-stu-id="f3a25-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="f3a25-116">只有 hello Exchange 結構描述的樹系是有效的目標群組。</span><span class="sxs-lookup"><span data-stu-id="f3a25-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="f3a25-117">如果不偵測到任何 Exchange，然後群組回寫是不可能 tooenable。</span><span class="sxs-lookup"><span data-stu-id="f3a25-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="f3a25-118">目前只支援單一樹系 Exchange 組織部署。</span><span class="sxs-lookup"><span data-stu-id="f3a25-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="f3a25-119">如果您有一個以上的 Exchange 組織內部，然後您需要在內部部署 GALSync 解決方案的這些群組 tooappear 其他樹系中。</span><span class="sxs-lookup"><span data-stu-id="f3a25-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="f3a25-120">安全性群組或通訊群組，並不會處理 hello 群組回寫功能。</span><span class="sxs-lookup"><span data-stu-id="f3a25-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="f3a25-121">用於群組回寫需要訂用帳戶 tooAzure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="f3a25-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="f3a25-122">使用者回寫</span><span class="sxs-lookup"><span data-stu-id="f3a25-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f3a25-123">hello 使用者回寫預覽功能已移除 hello 2015 年 8 月更新 tooAzure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="f3a25-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="f3a25-124">如果已啟用它，則您應該停用這個功能。</span><span class="sxs-lookup"><span data-stu-id="f3a25-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f3a25-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3a25-125">Next steps</span></span>
<span data-ttu-id="f3a25-126">繼續[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="f3a25-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="f3a25-127">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="f3a25-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
