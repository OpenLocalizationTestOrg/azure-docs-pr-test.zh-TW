---
ms.assetid: 
title: "Azure Key Vault 虛刪除 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: c873b153ef9c7d5f55672a5918c9dc4fb7256701
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a><span data-ttu-id="5d057-102">Azure Key Vault 虛刪除概觀</span><span class="sxs-lookup"><span data-stu-id="5d057-102">Azure Key Vault soft-delete overview</span></span>

<span data-ttu-id="5d057-103">Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件，也稱為「虛刪除」。</span><span class="sxs-lookup"><span data-stu-id="5d057-103">Key Vault's soft delete feature allows recovery of the deleted vaults and vault objects, known as soft-delete.</span></span> <span data-ttu-id="5d057-104">具體而言，我們會說明下列案例：</span><span class="sxs-lookup"><span data-stu-id="5d057-104">Specifically, we address the following scenarios:</span></span>

- <span data-ttu-id="5d057-105">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="5d057-105">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="5d057-106">可復原的 Key Vault 物件刪除支援 (物件的範例如：</span><span class="sxs-lookup"><span data-stu-id="5d057-106">Support for recoverable deletion of key vault objects (ex.</span></span> <span data-ttu-id="5d057-107">金鑰、密碼和憑證)</span><span class="sxs-lookup"><span data-stu-id="5d057-107">keys, secrets, certificates)</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="5d057-108">支援的介面</span><span class="sxs-lookup"><span data-stu-id="5d057-108">Supporting interfaces</span></span>

<span data-ttu-id="5d057-109">虛刪除功能最初是透過 REST、.NET/C# 和 PowerShell 介面提供。</span><span class="sxs-lookup"><span data-stu-id="5d057-109">The soft-delete feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="5d057-110">如需詳細資訊，請參閱這些介面的參考資料：[Key Vault 參考](https://docs.microsoft.com/azure/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="5d057-110">Refer to the references for these for more details, [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>

## <a name="scenarios"></a><span data-ttu-id="5d057-111">案例</span><span class="sxs-lookup"><span data-stu-id="5d057-111">Scenarios</span></span>

<span data-ttu-id="5d057-112">Azure Key Vault 是由 Azure Resource Manager 管理的追蹤資源。</span><span class="sxs-lookup"><span data-stu-id="5d057-112">Azure Key Vaults are tracked resources, managed by Azure Resource Manager.</span></span> <span data-ttu-id="5d057-113">Azure Resource Manager 也會指定妥善定義的刪除行為，而成功的「刪除」作業必須使資源無法再被存取。</span><span class="sxs-lookup"><span data-stu-id="5d057-113">Azure Resource Manager also specifies a well-defined behavior for deletion, which requires that a successful DELETE operation must result in that resource not being accessible anymore.</span></span> <span data-ttu-id="5d057-114">虛刪除功能可復原已刪除的物件，無論是無意或有意刪除的。</span><span class="sxs-lookup"><span data-stu-id="5d057-114">The soft-delete feature addresses the recovery of the deleted object, whether the deletion was accidental or intentional.</span></span>

1. <span data-ttu-id="5d057-115">在常見的案例中，使用者可能不小心刪除 Key Vault 或 Key Vault 物件；如果該 Key Vault 或 Key Vault 物件在預定期限內是可復原的，使用者可以還原刪除作業並復原其資料。</span><span class="sxs-lookup"><span data-stu-id="5d057-115">In the typical scenario, a user may have inadvertently deleted a key vault or a key vault object; if that key vault or key vault object were to be recoverable for a predetermined period, the user may undo the deletion and recover their data.</span></span>

2. <span data-ttu-id="5d057-116">而在其他案例中，惡意使用者可能會嘗試刪除 Key Vault 或 Key Vault 物件 (例如保存庫內的金鑰) 而使業務中斷。</span><span class="sxs-lookup"><span data-stu-id="5d057-116">In a different scenario, a rogue user may attempt to delete a key vault or a key vault object, such as a key inside a vault, to cause a business disruption.</span></span> <span data-ttu-id="5d057-117">將 Key Vault 或 Key Vault 物件的刪除與基礎資料的實際刪除做區隔，可做為一種安全措施，例如，將刪除資料的權限限制為其他信任的角色。</span><span class="sxs-lookup"><span data-stu-id="5d057-117">Separating the deletion of the key vault or key vault object from the actual deletion of the underlying data can be used as a safety measure by, for instance, restricting permissions on data deletion to a different, trusted role.</span></span> <span data-ttu-id="5d057-118">實際上，此方法這需要作業仲裁，否則可能導致直接的資料遺失。</span><span class="sxs-lookup"><span data-stu-id="5d057-118">This approach effectively requires quorum for an operation which might otherwise result in an immediate data loss.</span></span>

### <a name="soft-delete-behavior"></a><span data-ttu-id="5d057-119">虛刪除行為</span><span class="sxs-lookup"><span data-stu-id="5d057-119">Soft-delete behavior</span></span>

<span data-ttu-id="5d057-120">使用此功能，針對 Key Vault 或 Key Vault 物件的刪除作業是虛刪除，實際上在指定的保留期限內會保留資源，然而看起來物件卻為已刪除。</span><span class="sxs-lookup"><span data-stu-id="5d057-120">With this feature, the DELETE operation on a key vault or key vault object is a soft-delete, effectively holding the resources for a given retention period, while giving the appearance that the object is deleted.</span></span> <span data-ttu-id="5d057-121">此服務進一步提供復原已刪除物件的機制 (基本上是復原刪除作業)。</span><span class="sxs-lookup"><span data-stu-id="5d057-121">The service further provides a mechanism for recovering the deleted object, essentially undoing the deletion.</span></span> 

<span data-ttu-id="5d057-122">虛刪除是選擇性的 Key Vault 行為，在此版本中**預設未啟用**。</span><span class="sxs-lookup"><span data-stu-id="5d057-122">Soft-delete is an optional Key Vault behavior and is **not enabled by default** in this release.</span></span> <span data-ttu-id="5d057-123">如需為 Key Vault 啟用虛刪除的詳細資訊，請參閱參考資料中適用於您所選介面的具體指引：[Key Vault 參考](https://docs.microsoft.com/azure/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="5d057-123">For details on enabling soft-delete for your key vault, see the specific guidance in the reference for the interface of your choice, [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>

### <a name="key-vault-recovery"></a><span data-ttu-id="5d057-124">Key Vault 復原</span><span class="sxs-lookup"><span data-stu-id="5d057-124">Key vault recovery</span></span>

<span data-ttu-id="5d057-125">一旦刪除 Key Vault，此服務會在訂用帳戶下建立 Proxy 資源，以新增足夠使用於復原的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5d057-125">Upon deleting a key vault, the service creates a proxy resource under the subscription, adding sufficient metadata for recovery.</span></span> <span data-ttu-id="5d057-126">Proxy 資源是預存物件，和刪除的 Key Vault 位於相同位置。</span><span class="sxs-lookup"><span data-stu-id="5d057-126">The proxy resource is a stored object, available in the same location as the deleted key vault.</span></span> 

### <a name="key-vault-object-recovery"></a><span data-ttu-id="5d057-127">Key Vault 物件復原</span><span class="sxs-lookup"><span data-stu-id="5d057-127">Key vault object recovery</span></span>

<span data-ttu-id="5d057-128">一旦刪除 Key Vault 物件 (例如金鑰)，此服務會將物件設為已刪除狀態，任何擷取作業將無法再存取它。</span><span class="sxs-lookup"><span data-stu-id="5d057-128">Upon deleting a key vault object, such as a key, the service will place the object in a deleted state, thus making it inaccessible to any retrieval operations.</span></span> <span data-ttu-id="5d057-129">此狀態下的 Key Vault 物件只能列出、復原或強制/永久刪除。</span><span class="sxs-lookup"><span data-stu-id="5d057-129">While in this state, the key vault object can only be listed, recovered, or forcefully/permanently deleted.</span></span> 

<span data-ttu-id="5d057-130">同時，Key Vault 會根據刪除的 Key Vault 或 Key Vault 物件來排程基礎資料的刪除，並在預定的保留間隔後執行。</span><span class="sxs-lookup"><span data-stu-id="5d057-130">At the same time, Key Vault will schedule the deletion of the underlying data corresponding to the deleted key vault or key vault object for execution after a predetermined retention interval.</span></span> <span data-ttu-id="5d057-131">在保留間隔期間，也會保留與保存庫相對應的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="5d057-131">The DNS record corresponding to the vault is also retained for the duration of the retention interval.</span></span>

### <a name="soft-delete-retention-period"></a><span data-ttu-id="5d057-132">虛刪除保留期限</span><span class="sxs-lookup"><span data-stu-id="5d057-132">Soft-delete retention period</span></span>

<span data-ttu-id="5d057-133">虛刪除的資源預設會保留 90 天的時間。</span><span class="sxs-lookup"><span data-stu-id="5d057-133">Soft deleted resources are retained for a set period of time, 90 days.</span></span> <span data-ttu-id="5d057-134">在虛刪除保留間隔期限內，下列說明是成立的：</span><span class="sxs-lookup"><span data-stu-id="5d057-134">During the soft-delete retention interval, the following apply:</span></span>

- <span data-ttu-id="5d057-135">您可以列出您的訂用帳戶下狀態是虛刪除的所有 Key Vault 和 Key Vault 物件，也能存取與它們相關的刪除和復原資訊。</span><span class="sxs-lookup"><span data-stu-id="5d057-135">You may list all of the key vaults and key vault objects in the soft-delete state for your subscription as well as access deletion and recovery information about them.</span></span>
    - <span data-ttu-id="5d057-136">只有具備特殊權限的使用者可以列出已刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d057-136">Only users with special permissions can list deleted vaults.</span></span> <span data-ttu-id="5d057-137">我們建議使用者建立具有這些特殊權限的自訂角色，以處理刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d057-137">We recommend that our users create a custom role with these special permissions for handling deleted vaults.</span></span>
- <span data-ttu-id="5d057-138">不能在同一個位置建立同名的 Key Vault；同樣地，若指定的 Key Vault 中含有同名且是已刪除狀態的物件，就無法在其中建立該 Key Vault 物件。</span><span class="sxs-lookup"><span data-stu-id="5d057-138">A key vault with the same name cannot be created in the same location; correspondingly, a key vault object cannot be created in a given vault if that key vault contains an object with the same name and which is in a deleted state</span></span> 
- <span data-ttu-id="5d057-139">只有具備特殊權限的使用者，可以在對應的 Proxy 資源上發出復原命令來還原 Key Vault 或 Key Vault 物件。</span><span class="sxs-lookup"><span data-stu-id="5d057-139">Only a specifically privileged user may restore a key vault or key vault object by issuing a recover command on the corresponding proxy resource.</span></span>
    - <span data-ttu-id="5d057-140">身為自訂角色成員 (這個角色有權在資源群組下建立 Key Vault) 的使用者，可以還原保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d057-140">The user, member of the custom role, who has the privilege to create a key vault under the resource group can restore the vault.</span></span>
- <span data-ttu-id="5d057-141">只有具備特殊權限的使用者，可以在對應的 Proxy 資源上發出刪除命令來強制刪除 Key Vault 或 Key Vault 物件。</span><span class="sxs-lookup"><span data-stu-id="5d057-141">Only a specifically privileged user may forcibly delete a key vault or key vault object by issuing a delete command on the corresponding proxy resource.</span></span>

<span data-ttu-id="5d057-142">除非 Key Vault 或 Key Vault 物件已復原，否則在保留間隔結束時，此服務會對虛刪除的 Key Vault 或 Key Vault 物件及其內容執行清除作業。</span><span class="sxs-lookup"><span data-stu-id="5d057-142">Unless a key vault or key vault object is recovered, at the end of the retention interval the service performs a purge of the soft-deleted key vault or key vault object and its content.</span></span> <span data-ttu-id="5d057-143">資源刪除作業無法重新排程。</span><span class="sxs-lookup"><span data-stu-id="5d057-143">Resource deletion may not be rescheduled.</span></span>

### <a name="permitted-purge"></a><span data-ttu-id="5d057-144">允許的清除作業</span><span class="sxs-lookup"><span data-stu-id="5d057-144">Permitted purge</span></span>

<span data-ttu-id="5d057-145">在 Proxy 資源上可透過 POST 作業永久刪除、清除 Key Vault，而這需要特殊權限。</span><span class="sxs-lookup"><span data-stu-id="5d057-145">Permanently deleting, purging, a key vault is possible via a POST operation on the proxy resource and requires special privileges.</span></span> <span data-ttu-id="5d057-146">一般而言，只有訂用帳戶擁有者可以清除 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="5d057-146">Generally, only the subscription owner will be able to purge a key vault.</span></span> <span data-ttu-id="5d057-147">POST 作業會對該保存庫觸發立即性且無法復原的刪除作業。</span><span class="sxs-lookup"><span data-stu-id="5d057-147">The POST operation triggers the immediate and irrecoverable deletion of that vault.</span></span> 

<span data-ttu-id="5d057-148">唯一的例外是當 Azure 訂用帳戶已標示為「無法刪除」時。</span><span class="sxs-lookup"><span data-stu-id="5d057-148">An exception to this is the case when the Azure subscription has been marked as *undeletable*.</span></span> <span data-ttu-id="5d057-149">在此情況下，只有此服務可接著執行實際的刪除作業，而且會以排程的程序執行。</span><span class="sxs-lookup"><span data-stu-id="5d057-149">In this case, only the service may then perform the actual deletion, and does so as a scheduled process.</span></span> 



