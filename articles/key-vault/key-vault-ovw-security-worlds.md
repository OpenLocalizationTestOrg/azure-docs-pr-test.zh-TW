---
ms.assetid: 
title: "aaaAzure 金鑰保存庫安全園地 |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="d458b-102">Azure Key Vault 安全世界和地理界限</span><span class="sxs-lookup"><span data-stu-id="d458b-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="d458b-103">Azure Key Vault 是多租用戶服務，並且在每個 Azure 位置使用硬體安全模組 (HSM) 的集區。</span><span class="sxs-lookup"><span data-stu-id="d458b-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="d458b-104">所有的 Hsm 在 hello 的 Azure 位置上相同的地理區域共用 hello 相同的密碼編譯界限 （Thales 安全園地）。</span><span class="sxs-lookup"><span data-stu-id="d458b-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="d458b-105">例如，美國東部和共用美國西部 hello 相同的安全園地，因為它們隸屬 toohello 美國地理位置。</span><span class="sxs-lookup"><span data-stu-id="d458b-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="d458b-106">同樣地，所有的 Azure 位置，在日本共用 hello 相同的安全園地和所有的 Azure 位置，澳洲、 印度、 等等。</span><span class="sxs-lookup"><span data-stu-id="d458b-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="d458b-107">備份與還原行為</span><span class="sxs-lookup"><span data-stu-id="d458b-107">Backup and restore behavior</span></span>

<span data-ttu-id="d458b-108">其中一個 Azure 位置可以是金鑰保存庫的金鑰建立的備份還原 tooa 金鑰保存庫中其他的 Azure 位置，只要這些條件都成立：</span><span class="sxs-lookup"><span data-stu-id="d458b-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="d458b-109">這兩個 hello Azure 位置所屬 toohello 相同的地理位置</span><span class="sxs-lookup"><span data-stu-id="d458b-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="d458b-110">這兩個金鑰保存庫 hello 隸屬 toohello 相同的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d458b-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="d458b-111">比方說，印度西部金鑰保存庫中的索引鍵中的指定訂用帳戶所建立的備份只能還原的 tooanother hello 在金鑰保存庫相同的訂用帳戶和地理位置。印度西部、 印度中部或印度南部及印度。</span><span class="sxs-lookup"><span data-stu-id="d458b-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="d458b-112">區域和產品</span><span class="sxs-lookup"><span data-stu-id="d458b-112">Regions and products</span></span>

- [<span data-ttu-id="d458b-113">Azure 區域</span><span class="sxs-lookup"><span data-stu-id="d458b-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="d458b-114">依區域的 Microsoft 產品</span><span class="sxs-lookup"><span data-stu-id="d458b-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="d458b-115">區域是對應的 toosecurity 領域，顯示為在 hello 資料表中的主要標頭：</span><span class="sxs-lookup"><span data-stu-id="d458b-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="d458b-116">在 hello 產品中由區域發行項，例如 hello**美洲** 索引標籤包含東部 US，美國中部、 美國西部所有對應 toohello 美洲區域。</span><span class="sxs-lookup"><span data-stu-id="d458b-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="d458b-117">例外狀況是美國 DOD 東部和美國 DOD 中部有自己的安全世界。</span><span class="sxs-lookup"><span data-stu-id="d458b-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="d458b-118">同樣地，在 hello**歐洲**索引標籤，北歐和西歐都對應 toohello 歐洲地區。</span><span class="sxs-lookup"><span data-stu-id="d458b-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="d458b-119">hello 相同也是如此上 hello**亞太地區** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d458b-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



