---
title: "疑難排解: 'Active Directory' 項目已遺失或無法使用 |Microsoft 文件"
description: "若 Active Directory 功能表項目未出現在 Azure 管理入口網站中，該怎麼做。"
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="2579d-103">疑難排解：'Active Directory' 項目遺失或無法使用</span><span class="sxs-lookup"><span data-stu-id="2579d-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="2579d-104">許多使用 Azure Active Directory 功能和服務的相關指示都是以「前往 Azure 管理入口網站並按一下 **Active Directory**」為開頭。</span><span class="sxs-lookup"><span data-stu-id="2579d-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="2579d-105">但是，如果 Active Directory 擴充功能或功能表項目未出現，或者標示為 [無法使用]，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="2579d-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="2579d-106">本主題旨在提供協助。</span><span class="sxs-lookup"><span data-stu-id="2579d-106">This topic is designed to help.</span></span> <span data-ttu-id="2579d-107">它將說明 **Active Directory** 未出現或無法使用的情況，並說明如何繼續執行。</span><span class="sxs-lookup"><span data-stu-id="2579d-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="2579d-108">Active Directory 遺失</span><span class="sxs-lookup"><span data-stu-id="2579d-108">Active Directory is missing</span></span>
<span data-ttu-id="2579d-109">一般而言， **Active Directory** 項目會出現在左側導覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2579d-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="2579d-110">Azure Active Directory 程序中的指示假設此項目是在您的檢視中。</span><span class="sxs-lookup"><span data-stu-id="2579d-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![螢幕擷取畫面：Azure 中的 Active Directory](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="2579d-112">當下列任一條件成立時，Active Directory 項目就會出現在左側導覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2579d-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="2579d-113">否則，該項目便不會出現。</span><span class="sxs-lookup"><span data-stu-id="2579d-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="2579d-114">目前的使用者是使用 Microsoft 帳戶 (之前稱為 Windows Live ID) 登入。</span><span class="sxs-lookup"><span data-stu-id="2579d-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="2579d-115">或</span><span class="sxs-lookup"><span data-stu-id="2579d-115">OR</span></span>
* <span data-ttu-id="2579d-116">Azure 租用戶都擁有一個目錄，且目前的帳戶為目錄系統管理員。</span><span class="sxs-lookup"><span data-stu-id="2579d-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="2579d-117">或</span><span class="sxs-lookup"><span data-stu-id="2579d-117">OR</span></span>
* <span data-ttu-id="2579d-118">Azure 租用戶至少具有一個 Azure AD 存取控制 (ACS) 命名空間。</span><span class="sxs-lookup"><span data-stu-id="2579d-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="2579d-119">如需詳細資訊，請參閱 [存取控制命名空間](https://msdn.microsoft.com/library/azure/gg185908.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2579d-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="2579d-120">或</span><span class="sxs-lookup"><span data-stu-id="2579d-120">OR</span></span>
* <span data-ttu-id="2579d-121">Azure 租用戶至少具有一個 Azure Multi-Factor Authentication 提供者。</span><span class="sxs-lookup"><span data-stu-id="2579d-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="2579d-122">如需詳細資訊，請參閱 [管理 Azure Multi-Factor Authentication 提供者](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="2579d-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="2579d-123">若要建立存取控制命名空間或 Multi-Factor Authentication 提供者，請按一下 [+新增]  >  [應用程式服務]  >  [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="2579d-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="2579d-124">若要取得目錄的系統管理權限，必須要求系統管理員將系統管理員角色指派給您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2579d-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="2579d-125">如需詳細資訊，請參閱 [指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="2579d-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="2579d-126">Active Directory 無法使用</span><span class="sxs-lookup"><span data-stu-id="2579d-126">Active Directory is not available</span></span>
<span data-ttu-id="2579d-127">當您按一下 [+新增]  >  [應用程式服務] 時，[Active Directory] 項目即會出現。</span><span class="sxs-lookup"><span data-stu-id="2579d-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="2579d-128">具體而言，當任何 Active Directory 功能 (例如，目錄、存取控制或 Multi-Factor Auth 提供者) 可供目前使用者使用時，Active Directory 項目即會出現。</span><span class="sxs-lookup"><span data-stu-id="2579d-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="2579d-129">不過，當網頁正在載入時，該項目會呈暗灰色且標示為 [無法使用] 。</span><span class="sxs-lookup"><span data-stu-id="2579d-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="2579d-130">這是暫時性狀態。</span><span class="sxs-lookup"><span data-stu-id="2579d-130">This is a temporary state.</span></span> <span data-ttu-id="2579d-131">如果您稍待片刻，該項目將變成可用狀態。</span><span class="sxs-lookup"><span data-stu-id="2579d-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="2579d-132">如果延遲太久，重新整理網頁通常就能解決問題。</span><span class="sxs-lookup"><span data-stu-id="2579d-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![螢幕擷取畫面：Active Directory 無法使用](./media/active-directory-troubleshooting/not-available.png)

