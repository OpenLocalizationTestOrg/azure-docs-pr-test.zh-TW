<span data-ttu-id="fc5b6-101">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="fc5b6-102">hello 範本包括區段稱為參數，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="fc5b6-103">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="fc5b6-104">不會定義參數的值，會一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="fc5b6-105">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="fc5b6-106">當定義參數，使用 hello **allowedValues**欄位 toospecify 其中值的使用者可以在部署期間提供。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="fc5b6-107">使用 hello **defaultValue**欄位 tooassign 值 toohello 參數，如果在部署期間未不提供任何值。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="fc5b6-108">我們將說明 hello 範本中的每個參數。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="fc5b6-109">siteName</span><span class="sxs-lookup"><span data-stu-id="fc5b6-109">siteName</span></span>
<span data-ttu-id="fc5b6-110">hello，您會希望 toocreate hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="fc5b6-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="fc5b6-111">hostingPlanName</span></span>
<span data-ttu-id="fc5b6-112">hello 名稱 hello 應用程式服務計劃 toouse 裝載 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="fc5b6-113">sku</span><span class="sxs-lookup"><span data-stu-id="fc5b6-113">sku</span></span>
<span data-ttu-id="fc5b6-114">定價層裝載計劃的 hello。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="fc5b6-115">hello 範本定義此參數，以允許的 hello 值，並指派的預設值 (S1)，如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="fc5b6-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="fc5b6-116">workerSize</span></span>
<span data-ttu-id="fc5b6-117">hello hello 裝載計劃 （小型、 中型或大型） 的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="fc5b6-118">hello 範本可定義 hello （0、 1 或 2），此參數允許的值，並指派的預設值 (0)，如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="fc5b6-119">hello 值相對應 toosmall 中型和大型。</span><span class="sxs-lookup"><span data-stu-id="fc5b6-119">hello values correspond toosmall, medium and large.</span></span>

