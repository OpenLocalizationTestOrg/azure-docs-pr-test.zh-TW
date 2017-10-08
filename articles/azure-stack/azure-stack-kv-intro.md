---
title: "aaaAzure 堆疊金鑰保存庫簡介 |Microsoft 文件"
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
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a><span data-ttu-id="72ef0-103">簡介 tooKey Azure 堆疊中的保存庫</span><span class="sxs-lookup"><span data-stu-id="72ef0-103">Introduction tooKey Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="72ef0-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="72ef0-104">Before you start</span></span>
<span data-ttu-id="72ef0-105">本文章假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="72ef0-105">This article assumes hello following:</span></span>

* <span data-ttu-id="72ef0-106">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="72ef0-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="72ef0-107">使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="72ef0-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="72ef0-108">PowerShell 設定為搭配 Azure Stack 使用</span><span class="sxs-lookup"><span data-stu-id="72ef0-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="72ef0-109">Key Vault 的基本概念</span><span class="sxs-lookup"><span data-stu-id="72ef0-109">Key Vault basics</span></span>
<span data-ttu-id="72ef0-110">Azure Stack 中的 Key Vault 可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="72ef0-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="72ef0-111">您可以使用 Key Vault 來加密金鑰和祕密 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.pfx 檔案和密碼)。</span><span class="sxs-lookup"><span data-stu-id="72ef0-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="72ef0-112">金鑰保存庫可簡化 hello 金鑰管理程序，並讓您 toomaintain 控制項的索引鍵，以存取並加密資料。</span><span class="sxs-lookup"><span data-stu-id="72ef0-112">Key Vault streamlines hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="72ef0-113">開發人員可以建立開發和測試以分鐘為單位的索引鍵，並再順暢地移轉 tooproduction 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="72ef0-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them tooproduction keys.</span></span> <span data-ttu-id="72ef0-114">安全性系統管理員可以授與，並撤銷權限 tookeys，視需要。</span><span class="sxs-lookup"><span data-stu-id="72ef0-114">Security administrators can grant (and revoke) permission tookeys, as needed.</span></span>

<span data-ttu-id="72ef0-115">只要擁有 Azure Stack 訂用帳戶，任何人都可以建立和使用金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="72ef0-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="72ef0-116">雖然開發人員和安全性系統管理員，將有益於金鑰保存庫，它可以實作並管理組織的其他 Azure 堆疊服務 hello 雲端系統管理員所管理。</span><span class="sxs-lookup"><span data-stu-id="72ef0-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by hello cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="72ef0-117">比方說，hello 雲端系統管理員可以使用 Azure 堆疊訂用帳戶登入、 哪些 toostore 機碼中，建立 hello 組織保存庫，就負責處理這些作業的工作：</span><span class="sxs-lookup"><span data-stu-id="72ef0-117">For example, hello cloud administrator can sign in with an Azure Stack subscription, create a vault for hello organization in which toostore keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="72ef0-118">建立或匯入金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="72ef0-118">Create or import a key or secret</span></span>
* <span data-ttu-id="72ef0-119">撤銷或刪除金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="72ef0-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="72ef0-120">授權使用者或應用程式 tooaccess hello 金鑰保存庫，讓他們可以管理或使用其索引鍵和機密資料</span><span class="sxs-lookup"><span data-stu-id="72ef0-120">Authorize users or applications tooaccess hello key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="72ef0-121">設定金鑰使用方法 (例如，簽署或加密)</span><span class="sxs-lookup"><span data-stu-id="72ef0-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="72ef0-122">hello 雲端系統管理員可以從他們的應用程式的 Uri toocall 提供開發人員並提供金鑰的使用情況記錄資訊的安全性系統管理員。</span><span class="sxs-lookup"><span data-stu-id="72ef0-122">hello cloud administrator can then provide developers with URIs toocall from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="72ef0-123">開發人員也可以管理 hello 機碼直接使用 Api。</span><span class="sxs-lookup"><span data-stu-id="72ef0-123">Developers can also manage hello keys directly, by using APIs.</span></span> <span data-ttu-id="72ef0-124">如需詳細資訊，請參閱 hello 金鑰保存庫開發人員手冊 》。</span><span class="sxs-lookup"><span data-stu-id="72ef0-124">For more information, see hello Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="72ef0-125">案例</span><span class="sxs-lookup"><span data-stu-id="72ef0-125">Scenarios</span></span>
<span data-ttu-id="72ef0-126">hello 下表描述的金鑰保存庫可協助開發人員和安全性系統管理員需求 hello hello 案例：</span><span class="sxs-lookup"><span data-stu-id="72ef0-126">hello following table depicts some of hello scenarios where Key Vault can help meet hello needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="72ef0-127">Azure Stack 應用程式的開發人員</span><span class="sxs-lookup"><span data-stu-id="72ef0-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="72ef0-128">**問題**： 我想要用於簽署及加密，會使用金鑰的 Azure 堆疊 toowrite 應用程式，但我想要這些 toobe 外部我的應用程式從如此 hello 方案適合地理位置分散的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72ef0-128">**Problem**: I want toowrite an application for Azure Stack that uses keys for signing and encryption, but I want these toobe external from my application so that hello solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="72ef0-129">**說明**：金鑰會儲存在保存庫中，並且視需要由 URI 叫用。</span><span class="sxs-lookup"><span data-stu-id="72ef0-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="72ef0-130">軟體即服務 (SaaS) 的開發人員</span><span class="sxs-lookup"><span data-stu-id="72ef0-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="72ef0-131">**問題：**我不想要顯示 hello 責任或潛在責任我的客戶金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="72ef0-131">**Problem:** I don’t want hello responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="72ef0-132">**說明**：客戶可以將他們自己的金鑰匯入 Azure Stack 並加以管理。</span><span class="sxs-lookup"><span data-stu-id="72ef0-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="72ef0-133">我想客戶 tooown 並管理其索引鍵，讓我可以專注於我要怎麼最佳，這提供 hello 核心軟體功能。</span><span class="sxs-lookup"><span data-stu-id="72ef0-133">I want customers tooown and manage their keys so that I can concentrate on doing what I do best, which is providing hello core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="72ef0-134">資訊安全長 (CSO)</span><span class="sxs-lookup"><span data-stu-id="72ef0-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="72ef0-135">**問題：**我想 toomake 確定我的組織在 hello 金鑰生命週期的控制權，而且可以監視金鑰使用方式。</span><span class="sxs-lookup"><span data-stu-id="72ef0-135">**Problem:** I want toomake sure that my organization is in control of hello key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="72ef0-136">**說明**：Key Vault 的設計，便是讓 Microsoft 無法看見或擷取您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="72ef0-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="72ef0-137">當應用程式需要 tooperform 密碼編譯作業時使用客戶的金鑰時，金鑰保存庫會代表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72ef0-137">When an application needs tooperform cryptographic operations by using customers’ keys, Key Vault does this on behalf of hello application.</span></span> <span data-ttu-id="72ef0-138">hello 應用程式不會看到 hello 客戶索引鍵。</span><span class="sxs-lookup"><span data-stu-id="72ef0-138">hello application does not see hello customers’ keys.</span></span>  <span data-ttu-id="72ef0-139">雖然我們會使用多個 Azure 堆疊服務和資源，但我想 toomanage hello 索引鍵，從 Azure 堆疊中的單一位置。</span><span class="sxs-lookup"><span data-stu-id="72ef0-139">Although we use multiple Azure Stack services and resources, I want toomanage hello keys from a single location in Azure Stack.</span></span> <span data-ttu-id="72ef0-140">hello 保存庫會提供單一介面，不論多少的保存庫中有 Azure 堆疊，哪些區域它們支援，以及哪些應用程式使用它們。</span><span class="sxs-lookup"><span data-stu-id="72ef0-140">hello vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72ef0-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72ef0-141">Next Steps</span></span>

* [<span data-ttu-id="72ef0-142">管理 Azure 堆疊使用 hello 入口網站中的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="72ef0-142">Manage Key Vault in Azure Stack using hello portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="72ef0-143">使用 PowerShell 管理 Azure Stack 中的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="72ef0-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
