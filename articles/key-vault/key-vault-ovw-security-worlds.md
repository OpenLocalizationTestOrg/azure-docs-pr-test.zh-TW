---
ms.assetid: 
title: "Azure Key Vault 安全世界 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="f610f-102">Azure Key Vault 安全世界和地理界限</span><span class="sxs-lookup"><span data-stu-id="f610f-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="f610f-103">Azure Key Vault 是多租用戶服務，並且在每個 Azure 位置使用硬體安全模組 (HSM) 的集區。</span><span class="sxs-lookup"><span data-stu-id="f610f-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="f610f-104">同一個地理區域之 Azure 位置上的所有 HSM 都共用相同的密碼編譯界限 (Thales 安全世界)。</span><span class="sxs-lookup"><span data-stu-id="f610f-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="f610f-105">例如，美國東部和美國西部共用相同的安全世界，因為它們隸屬於美國地理位置。</span><span class="sxs-lookup"><span data-stu-id="f610f-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="f610f-106">同樣地，日本的所有 Azure 位置共用相同的安全世界，而位於澳洲、印度等國的所有 Azure 位置以此類推。</span><span class="sxs-lookup"><span data-stu-id="f610f-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="f610f-107">備份與還原行為</span><span class="sxs-lookup"><span data-stu-id="f610f-107">Backup and restore behavior</span></span>

<span data-ttu-id="f610f-108">在一個 Azure 位置的 Key Vault 建立的金鑰備份可還原至另一個 Azure 位置的 Key Vault，前提是這兩個條件都成立︰</span><span class="sxs-lookup"><span data-stu-id="f610f-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="f610f-109">兩個 Azure 位置都隸屬於相同的地理位置</span><span class="sxs-lookup"><span data-stu-id="f610f-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="f610f-110">兩個 Key Vault 都隸屬於相同的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f610f-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="f610f-111">例如，以指定的訂用帳戶在印度西部的 Key Vault 建立的金鑰備份，只能還原至同一個訂用帳戶和地理位置 (印度西部、印度中部或印度南部) 的另一個 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="f610f-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="f610f-112">區域和產品</span><span class="sxs-lookup"><span data-stu-id="f610f-112">Regions and products</span></span>

- [<span data-ttu-id="f610f-113">Azure 區域</span><span class="sxs-lookup"><span data-stu-id="f610f-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="f610f-114">依區域的 Microsoft 產品</span><span class="sxs-lookup"><span data-stu-id="f610f-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="f610f-115">區域會對應至安全世界，在資料表中顯示為主要標題：</span><span class="sxs-lookup"><span data-stu-id="f610f-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="f610f-116">在依區域的產品文章中，例如，[美國] 索引標籤包含都會對應至美國區域的美國東部、美國中部、美國西部。</span><span class="sxs-lookup"><span data-stu-id="f610f-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="f610f-117">例外狀況是美國 DOD 東部和美國 DOD 中部有自己的安全世界。</span><span class="sxs-lookup"><span data-stu-id="f610f-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="f610f-118">同樣地，在 [歐洲] 索引標籤上，北歐和西歐都會對應到歐洲區域。</span><span class="sxs-lookup"><span data-stu-id="f610f-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="f610f-119">在 [亞太地區] 索引標籤上也是如此。</span><span class="sxs-lookup"><span data-stu-id="f610f-119">The same is also true on the **Asia Pacific** tab.</span></span>



