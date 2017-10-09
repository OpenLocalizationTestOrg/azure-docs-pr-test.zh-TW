### <a name="app-service-plan"></a><span data-ttu-id="bf412-101">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="bf412-101">App Service plan</span></span>
<span data-ttu-id="bf412-102">建立 hello 裝載 hello web 應用程式的服務方案。</span><span class="sxs-lookup"><span data-stu-id="bf412-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="bf412-103">提供透過 hello hello 計劃 hello 名稱**hostingPlanName**參數。</span><span class="sxs-lookup"><span data-stu-id="bf412-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="bf412-104">hello 計劃 hello 位置是的 hello hello 資源群組使用相同的位置。</span><span class="sxs-lookup"><span data-stu-id="bf412-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="bf412-105">hello 定價層和背景工作大小指定在 hello **sku**和**workerSize**參數</span><span class="sxs-lookup"><span data-stu-id="bf412-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

