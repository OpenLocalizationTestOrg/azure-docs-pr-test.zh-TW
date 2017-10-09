
### <a name="cacheskuname"></a><span data-ttu-id="67a23-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="67a23-101">cacheSKUName</span></span>
<span data-ttu-id="67a23-102">hello 定價層的 hello 新的 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="67a23-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="67a23-103">hello 範本定義 hello 值，允許這個參數 （基本或標準），並指派的預設值 （基本），如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="67a23-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="67a23-104">Basic 提供具有向上 too53 GB 可用的多個大小的單一節點。</span><span class="sxs-lookup"><span data-stu-id="67a23-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="67a23-105">標準提供兩個節點主要/複本可用總 too53 GB 和 99.9 %sla 的多個大小。</span><span class="sxs-lookup"><span data-stu-id="67a23-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="67a23-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="67a23-106">cacheSKUFamily</span></span>
<span data-ttu-id="67a23-107">hello hello sku 系列。</span><span class="sxs-lookup"><span data-stu-id="67a23-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="67a23-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="67a23-108">cacheSKUCapacity</span></span>
<span data-ttu-id="67a23-109">hello hello 新 Azure Redis 快取執行個體的大小。</span><span class="sxs-lookup"><span data-stu-id="67a23-109">hello size of hello new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="67a23-110">hello 範本可定義 hello （0、 1、 2、 3、 4、 5 或 6），此參數允許的值，並指派的預設值 (1)，如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="67a23-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="67a23-111">這些數字對應 toofollowing 快取大小： 0 = 250 MB，1 = 1 GB，2 = 2.5 GB，3 = 6 GB，4 = 13 GB，5 = 26 GB，6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="67a23-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

