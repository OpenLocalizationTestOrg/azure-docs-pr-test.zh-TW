---
title: "嘗試登入 Azure 入口網站或 Azure 帳戶中心時，未在訂用帳戶中找到任何錯誤 | Microsoft Docs"
description: "針對登入 Azure 入口網站或 Azure 帳戶中心時，未在訂用帳戶中找到任何錯誤這個問題，提供解決方案。"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="918f5-103">在 Azure 入口網站或 Azure 帳戶中心內，未於訂用帳戶中找到任何錯誤</span><span class="sxs-lookup"><span data-stu-id="918f5-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="918f5-104">當您嘗試登入 [Azure 入口網站](https://portal.azure.com/)或 [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)時，可能會收到「找不到訂用帳戶」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="918f5-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="918f5-105">本文會提供此問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="918f5-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="918f5-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="918f5-106">Symptom</span></span>

<span data-ttu-id="918f5-107">當您嘗試登入 [Azure 入口網站](https://portal.azure.com/)或 [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)時，會收到下列錯誤訊息：「找不到訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="918f5-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="918f5-108">原因</span><span class="sxs-lookup"><span data-stu-id="918f5-108">Cause</span></span>

<span data-ttu-id="918f5-109">如果您的帳戶沒有足夠的權限，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="918f5-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="918f5-110">方案</span><span class="sxs-lookup"><span data-stu-id="918f5-110">Solution</span></span>

<span data-ttu-id="918f5-111">請確定您是以正確的系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="918f5-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="918f5-112">帳戶管理員只能存取帳戶中心。</span><span class="sxs-lookup"><span data-stu-id="918f5-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="918f5-113">服務管理員 (SA) 和共同管理員 (CA) 只有存取 Azure 入口網站或 Azure 傳統入口網站的權限。</span><span class="sxs-lookup"><span data-stu-id="918f5-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="918f5-114">情節 1：在 [Azure 入口網站](https://portal.azure.com)收到錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="918f5-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="918f5-115">若要修正此問題：</span><span class="sxs-lookup"><span data-stu-id="918f5-115">To fix this issue:</span></span>

* <span data-ttu-id="918f5-116">確定您已選取正確的 Azure 目錄，方法是按一下右上角的帳戶。</span><span class="sxs-lookup"><span data-stu-id="918f5-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![選取 Azure 入口網站右上角的目錄](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="918f5-118">若已選取正確的 Azure 目錄，但您仍收到錯誤訊息，請[將您的帳戶新增為擁有者](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="918f5-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="918f5-119">情節 2：在 [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)收到錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="918f5-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="918f5-120">請檢查您所使用的帳戶是否為帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="918f5-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="918f5-121">若要確認誰是帳戶管理員，請依照下列步驟操作︰</span><span class="sxs-lookup"><span data-stu-id="918f5-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="918f5-122">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="918f5-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="918f5-123">在 [中樞] 功能表中，選取 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="918f5-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="918f5-124">選取您想要檢查的訂用帳戶，然後選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="918f5-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="918f5-125">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="918f5-125">Select **Properties**.</span></span> <span data-ttu-id="918f5-126">該訂用帳戶的帳戶管理員會顯示在 [帳戶管理員]  方塊中。</span><span class="sxs-lookup"><span data-stu-id="918f5-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="918f5-127">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="918f5-127">Need help?</span></span> <span data-ttu-id="918f5-128">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="918f5-128">Contact support.</span></span>
<span data-ttu-id="918f5-129">如果仍需要協助，請[連絡支援人員](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="918f5-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
