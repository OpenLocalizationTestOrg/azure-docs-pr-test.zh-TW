---
title: "aaaNo 訂用帳戶中找到的錯誤時再試一次 toosign tooAzure 入口網站或 Azure 帳戶中心 |Microsoft 文件"
description: "提供 hello 方案中沒有訂用帳戶會找到錯誤，就會發生問題時登入 tooAzure 入口網站或 Azure 帳戶中心。"
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
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="1df33-103">在 Azure 入口網站或 Azure 帳戶中心內，未於訂用帳戶中找到任何錯誤</span><span class="sxs-lookup"><span data-stu-id="1df33-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="1df33-104">您可能會收到 「 找不到訂閱 」 錯誤訊息，當您嘗試在 toohello toosign [Azure 入口網站](https://portal.azure.com/)或 hello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="1df33-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="1df33-105">本文會提供此問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1df33-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="1df33-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="1df33-106">Symptom</span></span>

<span data-ttu-id="1df33-107">當您嘗試在 toohello toosign [Azure 入口網站](https://portal.azure.com/)或 hello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)，您會收到下列錯誤訊息的 hello: 「 找不到訂閱 」。</span><span class="sxs-lookup"><span data-stu-id="1df33-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="1df33-108">原因</span><span class="sxs-lookup"><span data-stu-id="1df33-108">Cause</span></span>

<span data-ttu-id="1df33-109">如果您的帳戶沒有足夠的權限，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="1df33-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="1df33-110">方案</span><span class="sxs-lookup"><span data-stu-id="1df33-110">Solution</span></span>

<span data-ttu-id="1df33-111">請確定您在 hello 正確的系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="1df33-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="1df33-112">帳戶系統管理員可以存取 hello 帳戶中心。</span><span class="sxs-lookup"><span data-stu-id="1df33-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="1df33-113">服務系統管理員 (SA) 和共同管理員 (CA) 的存取權限只有 toohello Azure 入口網站或 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="1df33-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="1df33-114">案例 1: Hello 中收到錯誤訊息[Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1df33-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="1df33-115">toofix 此問題：</span><span class="sxs-lookup"><span data-stu-id="1df33-115">toofix this issue:</span></span>

* <span data-ttu-id="1df33-116">請確定該 hello 正確依序按一下您的帳戶在 hello 右上方選取 Azure 目錄。</span><span class="sxs-lookup"><span data-stu-id="1df33-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![選取 hello 目錄 hello hello Azure 入口網站的右上方](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="1df33-118">如果 hello 右 Azure 選取目錄，但是您仍然收到 hello 錯誤訊息，[將您的帳戶作為擁有者加入](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="1df33-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="1df33-119">案例 2: Hello 中收到錯誤訊息[Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="1df33-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="1df33-120">檢查您所使用的 hello 帳戶是否 hello 帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="1df33-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="1df33-121">tooverify 人員 hello 帳戶系統管理員，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1df33-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="1df33-122">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1df33-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1df33-123">在 hello 中樞功能表中，選取 **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1df33-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="1df33-124">選取您想 toocheck，，然後選取 hello 訂閱**設定**。</span><span class="sxs-lookup"><span data-stu-id="1df33-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="1df33-125">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="1df33-125">Select **Properties**.</span></span> <span data-ttu-id="1df33-126">hello hello 訂用帳戶的帳戶管理員會顯示在 hello**帳戶管理員**方塊。</span><span class="sxs-lookup"><span data-stu-id="1df33-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="1df33-127">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="1df33-127">Need help?</span></span> <span data-ttu-id="1df33-128">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="1df33-128">Contact support.</span></span>
<span data-ttu-id="1df33-129">如果您仍需要協助，[連絡支援人員](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="1df33-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
