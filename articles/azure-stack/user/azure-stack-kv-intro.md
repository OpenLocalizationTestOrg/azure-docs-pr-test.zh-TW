---
title: "Azure Stack Key Vault 簡介 | Microsoft Docs"
description: "了解 Azure Stack Key Vault 如何管理金鑰和祕密"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: ecb542e967669fc4e4465ae59b3e9c37e4a5c332
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="c4535-103">Azure Stack 中的 Key Vault 簡介</span><span class="sxs-lookup"><span data-stu-id="c4535-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c4535-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="c4535-104">Before you start</span></span>
<span data-ttu-id="c4535-105">本文假設下列項目：</span><span class="sxs-lookup"><span data-stu-id="c4535-105">This article assumes the following:</span></span>

* <span data-ttu-id="c4535-106">您必須訂閱包含 Key Vault 服務的供應項目。</span><span class="sxs-lookup"><span data-stu-id="c4535-106">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="c4535-107">PowerShell 設定為搭配 Azure Stack 使用</span><span class="sxs-lookup"><span data-stu-id="c4535-107">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="c4535-108">Key Vault 的基本概念</span><span class="sxs-lookup"><span data-stu-id="c4535-108">Key Vault basics</span></span>
<span data-ttu-id="c4535-109">Azure Stack 中的 Key Vault 可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="c4535-109">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="c4535-110">您可以使用 Key Vault 來加密金鑰和祕密 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.pfx 檔案和密碼)。</span><span class="sxs-lookup"><span data-stu-id="c4535-110">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="c4535-111">金鑰保存庫簡化了金鑰管理程序，並可讓您控管存取和加密資料的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-111">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="c4535-112">開發人員可以在幾分鐘內建立開發和測試的金鑰，然後順利地將他們移轉至生產金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-112">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="c4535-113">安全性系統管理員可以視需要授與 (和撤銷) 存取金鑰的權限。</span><span class="sxs-lookup"><span data-stu-id="c4535-113">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="c4535-114">只要擁有 Azure Stack 訂用帳戶，任何人都可以建立和使用金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c4535-114">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="c4535-115">雖然 Key Vault 有助於開發人員和安全性系統管理員，但管理組織其他 Azure Stack 服務的操作員也可以實作並管理 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="c4535-115">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the operator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="c4535-116">例如，Azure Stack 操作員可以使用 Azure Stack 訂用帳戶登入、建立組織要用來儲存金鑰的保存庫，然後負責執行以下操作作業：</span><span class="sxs-lookup"><span data-stu-id="c4535-116">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="c4535-117">建立或匯入金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="c4535-117">Create or import a key or secret</span></span>
* <span data-ttu-id="c4535-118">撤銷或刪除金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="c4535-118">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="c4535-119">授權使用者或應用程式存取金鑰保存庫，以便管理或使用其金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="c4535-119">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="c4535-120">設定金鑰使用方法 (例如，簽署或加密)</span><span class="sxs-lookup"><span data-stu-id="c4535-120">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="c4535-121">操作員接著可以為開發人員提供可從其應用程式進行呼叫的 URI，並為安全性系統管理員提供金鑰使用記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="c4535-121">The operator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="c4535-122">開發人員也可透過使用 API 直接管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-122">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="c4535-123">如需詳細資訊，請參閱《Key Vault 開發人員指南》。</span><span class="sxs-lookup"><span data-stu-id="c4535-123">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="c4535-124">案例</span><span class="sxs-lookup"><span data-stu-id="c4535-124">Scenarios</span></span>
<span data-ttu-id="c4535-125">下表說明 Key Vault 協助滿足開發人員和安全性系統管理員需求的一些案例：</span><span class="sxs-lookup"><span data-stu-id="c4535-125">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="c4535-126">Azure Stack 應用程式的開發人員</span><span class="sxs-lookup"><span data-stu-id="c4535-126">Developer for an Azure Stack application</span></span>
<span data-ttu-id="c4535-127">**問題**：我想要撰寫使用金鑰進行簽署和加密的 Azure Stack 應用程式，但我希望這些金鑰會與我的應用程式分開，如此一來此解決方案便適用於位於不同地點的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4535-127">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="c4535-128">**說明**：金鑰會儲存在保存庫中，並且視需要由 URI 叫用。</span><span class="sxs-lookup"><span data-stu-id="c4535-128">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="c4535-129">軟體即服務 (SaaS) 的開發人員</span><span class="sxs-lookup"><span data-stu-id="c4535-129">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="c4535-130">**問題**：對於客戶的金鑰和祕密，我不想承擔任何實際或潛在法律責任。</span><span class="sxs-lookup"><span data-stu-id="c4535-130">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="c4535-131">**說明**：客戶可以將他們自己的金鑰匯入 Azure Stack 並加以管理。</span><span class="sxs-lookup"><span data-stu-id="c4535-131">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="c4535-132">我希望客戶擁有並自行管理金鑰，所以我可以將全部精力集中在我的專長上，也就是提供核心軟體功能。</span><span class="sxs-lookup"><span data-stu-id="c4535-132">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="c4535-133">資訊安全長 (CSO)</span><span class="sxs-lookup"><span data-stu-id="c4535-133">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="c4535-134">**問題**：我想要確定我的組織掌控著金鑰生命週期，並可監視金鑰使用狀況。</span><span class="sxs-lookup"><span data-stu-id="c4535-134">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="c4535-135">**說明**：Key Vault 的設計，便是讓 Microsoft 無法看見或擷取您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-135">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="c4535-136">當應用程式必須使用客戶的金鑰來執行加密編譯密碼作業時，Key Vault 會代表應用程式來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="c4535-136">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="c4535-137">應用程式不會看到客戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-137">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="c4535-138">即使我們使用多個 Azure Stack 服務和資源，我仍想要從 Azure Stack 中的單一位置管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="c4535-138">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="c4535-139">不論您在 Azure Stack 中有幾個保存庫、保存庫支援哪些區域，以及哪些應用程式使用這些保存庫，保存庫都可以提供單一介面。</span><span class="sxs-lookup"><span data-stu-id="c4535-139">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4535-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4535-140">Next Steps</span></span>

* [<span data-ttu-id="c4535-141">使用入口網站管理 Azure Stack 中的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="c4535-141">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="c4535-142">使用 PowerShell 管理 Azure Stack 中的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="c4535-142">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
