---
ms.assetid: 
title: "aaaAzure 金鑰保存庫虛刪除 |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a><span data-ttu-id="81de9-102">Azure Key Vault 虛刪除概觀</span><span class="sxs-lookup"><span data-stu-id="81de9-102">Azure Key Vault soft-delete overview</span></span>

<span data-ttu-id="81de9-103">金鑰保存庫虛刪除功能可讓 hello 刪除保存庫與保存庫的物件，稱為 「 虛刪除的復原。</span><span class="sxs-lookup"><span data-stu-id="81de9-103">Key Vault's soft delete feature allows recovery of hello deleted vaults and vault objects, known as soft-delete.</span></span> <span data-ttu-id="81de9-104">具體來說，我們解決 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="81de9-104">Specifically, we address hello following scenarios:</span></span>

- <span data-ttu-id="81de9-105">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="81de9-105">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="81de9-106">可復原的 Key Vault 物件刪除支援 (物件的範例如：</span><span class="sxs-lookup"><span data-stu-id="81de9-106">Support for recoverable deletion of key vault objects (ex.</span></span> <span data-ttu-id="81de9-107">金鑰、密碼和憑證)</span><span class="sxs-lookup"><span data-stu-id="81de9-107">keys, secrets, certificates)</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="81de9-108">支援的介面</span><span class="sxs-lookup"><span data-stu-id="81de9-108">Supporting interfaces</span></span>

<span data-ttu-id="81de9-109">hello 虛刪除功能是一開始可透過 hello 其餘部分，.NET / C# 和 PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="81de9-109">hello soft-delete feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="81de9-110">如需詳細資訊，這些參考 toohello 參考[金鑰保存庫參考](https://docs.microsoft.com/azure/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="81de9-110">Refer toohello references for these for more details, [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>

## <a name="scenarios"></a><span data-ttu-id="81de9-111">案例</span><span class="sxs-lookup"><span data-stu-id="81de9-111">Scenarios</span></span>

<span data-ttu-id="81de9-112">Azure Key Vault 是由 Azure Resource Manager 管理的追蹤資源。</span><span class="sxs-lookup"><span data-stu-id="81de9-112">Azure Key Vaults are tracked resources, managed by Azure Resource Manager.</span></span> <span data-ttu-id="81de9-113">Azure Resource Manager 也會指定妥善定義的刪除行為，而成功的「刪除」作業必須使資源無法再被存取。</span><span class="sxs-lookup"><span data-stu-id="81de9-113">Azure Resource Manager also specifies a well-defined behavior for deletion, which requires that a successful DELETE operation must result in that resource not being accessible anymore.</span></span> <span data-ttu-id="81de9-114">hello 刪除是否意外或故意情況下，hello 虛刪除功能位址 hello 復原刪除的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="81de9-114">hello soft-delete feature addresses hello recovery of hello deleted object, whether hello deletion was accidental or intentional.</span></span>

1. <span data-ttu-id="81de9-115">在 hello 一般案例中，使用者可能不小心刪除金鑰保存庫或金鑰保存庫的物件。如果該金鑰保存庫或金鑰保存庫物件已預先決定的期間內的可復原 toobe，hello 使用者可能會恢復 hello 刪除作業，並復原其資料。</span><span class="sxs-lookup"><span data-stu-id="81de9-115">In hello typical scenario, a user may have inadvertently deleted a key vault or a key vault object; if that key vault or key vault object were toobe recoverable for a predetermined period, hello user may undo hello deletion and recover their data.</span></span>

2. <span data-ttu-id="81de9-116">在不同的案例中，惡意使用者可能會嘗試 toodelete 金鑰保存庫或金鑰保存庫的物件，例如金鑰在保存庫，toocause 業務中斷。</span><span class="sxs-lookup"><span data-stu-id="81de9-116">In a different scenario, a rogue user may attempt toodelete a key vault or a key vault object, such as a key inside a vault, toocause a business disruption.</span></span> <span data-ttu-id="81de9-117">Hello 刪除 hello 金鑰保存庫或金鑰保存庫的物件區隔開 hello 實際刪除基礎資料的 hello 可以做為安全起見，比方說，限制的權限的資料刪除 tooa 不同，信任的角色。</span><span class="sxs-lookup"><span data-stu-id="81de9-117">Separating hello deletion of hello key vault or key vault object from hello actual deletion of hello underlying data can be used as a safety measure by, for instance, restricting permissions on data deletion tooa different, trusted role.</span></span> <span data-ttu-id="81de9-118">實際上，此方法這需要作業仲裁，否則可能導致直接的資料遺失。</span><span class="sxs-lookup"><span data-stu-id="81de9-118">This approach effectively requires quorum for an operation which might otherwise result in an immediate data loss.</span></span>

### <a name="soft-delete-behavior"></a><span data-ttu-id="81de9-119">虛刪除行為</span><span class="sxs-lookup"><span data-stu-id="81de9-119">Soft-delete behavior</span></span>

<span data-ttu-id="81de9-120">利用此功能，hello 金鑰保存庫上的刪除作業，或金鑰保存庫的物件是虛刪除，有效地保留 hello 資源為指定的保留期限，讓該 hello 物件 hello 外觀刪除時。</span><span class="sxs-lookup"><span data-stu-id="81de9-120">With this feature, hello DELETE operation on a key vault or key vault object is a soft-delete, effectively holding hello resources for a given retention period, while giving hello appearance that hello object is deleted.</span></span> <span data-ttu-id="81de9-121">進一步 hello 服務會提供一個機制，來復原刪除的 hello 物件，基本上復原 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="81de9-121">hello service further provides a mechanism for recovering hello deleted object, essentially undoing hello deletion.</span></span> 

<span data-ttu-id="81de9-122">虛刪除是選擇性的 Key Vault 行為，在此版本中**預設未啟用**。</span><span class="sxs-lookup"><span data-stu-id="81de9-122">Soft-delete is an optional Key Vault behavior and is **not enabled by default** in this release.</span></span> <span data-ttu-id="81de9-123">如需啟用虛刪除金鑰保存庫的詳細資訊，請參閱 hello hello 參考您的選擇，hello 介面中的特定指導方針[金鑰保存庫參考](https://docs.microsoft.com/azure/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="81de9-123">For details on enabling soft-delete for your key vault, see hello specific guidance in hello reference for hello interface of your choice, [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>

### <a name="key-vault-recovery"></a><span data-ttu-id="81de9-124">Key Vault 復原</span><span class="sxs-lookup"><span data-stu-id="81de9-124">Key vault recovery</span></span>

<span data-ttu-id="81de9-125">一旦刪除金鑰保存庫，hello 服務會建立下 hello 訂用帳戶，加入足夠的中繼資料進行復原的 proxy 資源。</span><span class="sxs-lookup"><span data-stu-id="81de9-125">Upon deleting a key vault, hello service creates a proxy resource under hello subscription, adding sufficient metadata for recovery.</span></span> <span data-ttu-id="81de9-126">hello proxy 資源是預存的物件，用於 hello 與 hello 刪除金鑰保存庫相同的位置。</span><span class="sxs-lookup"><span data-stu-id="81de9-126">hello proxy resource is a stored object, available in hello same location as hello deleted key vault.</span></span> 

### <a name="key-vault-object-recovery"></a><span data-ttu-id="81de9-127">Key Vault 物件復原</span><span class="sxs-lookup"><span data-stu-id="81de9-127">Key vault object recovery</span></span>

<span data-ttu-id="81de9-128">一旦刪除金鑰保存庫物件，例如機碼，hello 服務會將 hello 物件處於已刪除狀態，使它無法存取 tooany 擷取作業。</span><span class="sxs-lookup"><span data-stu-id="81de9-128">Upon deleting a key vault object, such as a key, hello service will place hello object in a deleted state, thus making it inaccessible tooany retrieval operations.</span></span> <span data-ttu-id="81de9-129">處於此狀態時，hello 金鑰保存庫的物件只能列出，復原，或強制/永久刪除。</span><span class="sxs-lookup"><span data-stu-id="81de9-129">While in this state, hello key vault object can only be listed, recovered, or forcefully/permanently deleted.</span></span> 

<span data-ttu-id="81de9-130">在 hello 相同時間、 金鑰保存庫會排程的基礎資料的對應 toohello 刪除 hello hello 刪除金鑰保存庫或預先決定的保留間隔之後執行的金鑰保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="81de9-130">At hello same time, Key Vault will schedule hello deletion of hello underlying data corresponding toohello deleted key vault or key vault object for execution after a predetermined retention interval.</span></span> <span data-ttu-id="81de9-131">hello DNS 記錄對應 toohello 的保存庫也會保留 hello hello 保留間隔持續時間。</span><span class="sxs-lookup"><span data-stu-id="81de9-131">hello DNS record corresponding toohello vault is also retained for hello duration of hello retention interval.</span></span>

### <a name="soft-delete-retention-period"></a><span data-ttu-id="81de9-132">虛刪除保留期限</span><span class="sxs-lookup"><span data-stu-id="81de9-132">Soft-delete retention period</span></span>

<span data-ttu-id="81de9-133">虛刪除的資源預設會保留 90 天的時間。</span><span class="sxs-lookup"><span data-stu-id="81de9-133">Soft deleted resources are retained for a set period of time, 90 days.</span></span> <span data-ttu-id="81de9-134">在 hello 虛刪除保留間隔內，hello 下列適用於：</span><span class="sxs-lookup"><span data-stu-id="81de9-134">During hello soft-delete retention interval, hello following apply:</span></span>

- <span data-ttu-id="81de9-135">您可能會列出所有的 hello 金鑰保存庫和金鑰保存庫中的物件，您的訂用帳戶以及存取其相關的刪除和復原資訊 hello 虛刪除狀態。</span><span class="sxs-lookup"><span data-stu-id="81de9-135">You may list all of hello key vaults and key vault objects in hello soft-delete state for your subscription as well as access deletion and recovery information about them.</span></span>
    - <span data-ttu-id="81de9-136">只有具備特殊權限的使用者可以列出已刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="81de9-136">Only users with special permissions can list deleted vaults.</span></span> <span data-ttu-id="81de9-137">我們建議使用者建立具有這些特殊權限的自訂角色，以處理刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="81de9-137">We recommend that our users create a custom role with these special permissions for handling deleted vaults.</span></span>
- <span data-ttu-id="81de9-138">無法在 hello 建立相同名稱的 hello 與金鑰保存庫相同的位置。相對的只要該金鑰的保存庫包含 hello 的物件，金鑰保存庫物件就無法建立在指定的保存庫中相同名稱和哪個是處於已刪除的狀態</span><span class="sxs-lookup"><span data-stu-id="81de9-138">A key vault with hello same name cannot be created in hello same location; correspondingly, a key vault object cannot be created in a given vault if that key vault contains an object with hello same name and which is in a deleted state</span></span> 
- <span data-ttu-id="81de9-139">只有特別特殊權限的使用者可能會藉由發出 hello 對應 proxy 資源上的復原命令還原金鑰保存庫或金鑰保存庫的物件。</span><span class="sxs-lookup"><span data-stu-id="81de9-139">Only a specifically privileged user may restore a key vault or key vault object by issuing a recover command on hello corresponding proxy resource.</span></span>
    - <span data-ttu-id="81de9-140">hello 使用者角色的成員 hello 自訂，擁有 hello 權限 toocreate hello 資源群組下的金鑰保存庫可以還原 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="81de9-140">hello user, member of hello custom role, who has hello privilege toocreate a key vault under hello resource group can restore hello vault.</span></span>
- <span data-ttu-id="81de9-141">只有特別特殊權限的使用者強制可能刪除金鑰保存庫或金鑰保存庫的物件發出刪除命令 hello 對應 proxy 資源上。</span><span class="sxs-lookup"><span data-stu-id="81de9-141">Only a specifically privileged user may forcibly delete a key vault or key vault object by issuing a delete command on hello corresponding proxy resource.</span></span>

<span data-ttu-id="81de9-142">復原金鑰保存庫或金鑰保存庫物件，除非在 hello 結束 hello 保留間隔 hello 服務會執行清除虛刪除的 hello 金鑰保存庫或金鑰保存庫的物件和其內容。</span><span class="sxs-lookup"><span data-stu-id="81de9-142">Unless a key vault or key vault object is recovered, at hello end of hello retention interval hello service performs a purge of hello soft-deleted key vault or key vault object and its content.</span></span> <span data-ttu-id="81de9-143">資源刪除作業無法重新排程。</span><span class="sxs-lookup"><span data-stu-id="81de9-143">Resource deletion may not be rescheduled.</span></span>

### <a name="permitted-purge"></a><span data-ttu-id="81de9-144">允許的清除作業</span><span class="sxs-lookup"><span data-stu-id="81de9-144">Permitted purge</span></span>

<span data-ttu-id="81de9-145">永久刪除、 清除、 金鑰保存庫可透過 hello proxy 資源的 POST 作業，而需要特殊權限。</span><span class="sxs-lookup"><span data-stu-id="81de9-145">Permanently deleting, purging, a key vault is possible via a POST operation on hello proxy resource and requires special privileges.</span></span> <span data-ttu-id="81de9-146">一般而言，只有 hello 訂用帳戶擁有者將能夠 toopurge 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="81de9-146">Generally, only hello subscription owner will be able toopurge a key vault.</span></span> <span data-ttu-id="81de9-147">hello POST 作業觸發程序 hello 立即且無法復原刪除該保存庫。</span><span class="sxs-lookup"><span data-stu-id="81de9-147">hello POST operation triggers hello immediate and irrecoverable deletion of that vault.</span></span> 

<span data-ttu-id="81de9-148">例外狀況 toothis 是 hello 情況 hello Azure 訂用帳戶已被標示為*undeletable*。</span><span class="sxs-lookup"><span data-stu-id="81de9-148">An exception toothis is hello case when hello Azure subscription has been marked as *undeletable*.</span></span> <span data-ttu-id="81de9-149">在此情況下，只有 hello 服務然後可能會執行 hello 實際刪除，而且也這麼做為排程的處理序。</span><span class="sxs-lookup"><span data-stu-id="81de9-149">In this case, only hello service may then perform hello actual deletion, and does so as a scheduled process.</span></span> 



