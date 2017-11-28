---
title: "aaaCreate Azure 應用程式閘道-範本 |Microsoft 文件"
description: "本頁面提供的指示 toocreate Azure 應用程式閘道使用 hello Azure Resource Manager 範本"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="18684-103">使用 hello Azure Resource Manager 範本來建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="18684-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18684-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="18684-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="18684-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="18684-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="18684-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="18684-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="18684-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="18684-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="18684-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18684-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="18684-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="18684-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="18684-110">它提供容錯移轉和效能路由不同的伺服器之間的 HTTP 要求是否位於 hello 雲端或內部部署。</span><span class="sxs-lookup"><span data-stu-id="18684-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="18684-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="18684-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="18684-112">toofind 完整支援的功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="18684-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="18684-113">這篇文章會逐步引導您下載並修改現有的 Azure Resource Manager 範本從 GitHub 及部署從 GitHub、 PowerShell 和 hello Azure CLI hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18684-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="18684-114">如果您只需部署 hello Azure Resource Manager 範本，直接從 GitHub 不進行任何變更，請從 GitHub 略過 toodeploy 範本。</span><span class="sxs-lookup"><span data-stu-id="18684-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="18684-115">案例</span><span class="sxs-lookup"><span data-stu-id="18684-115">Scenario</span></span>

<span data-ttu-id="18684-116">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="18684-116">In this scenario you will:</span></span>

* <span data-ttu-id="18684-117">建立具有 Web 應用程式防火牆的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="18684-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="18684-118">建立名為 VirtualNetwork1 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="18684-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="18684-119">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="18684-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="18684-120">您想讓 tooload 平衡 hello 流量 hello 網頁伺服器先前已設定兩個後端 Ip 設定。</span><span class="sxs-lookup"><span data-stu-id="18684-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="18684-121">在此範本範例，hello 後端 Ip 是 10.0.1.10 和 10.0.1.11。</span><span class="sxs-lookup"><span data-stu-id="18684-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="18684-122">這些設定是 hello 參數，此範本。</span><span class="sxs-lookup"><span data-stu-id="18684-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="18684-123">toocustomize hello 範本，您可以變更規則、 hello 接聽程式、 SSL 及 hello azuredeploy.json 檔案中的其他選項。</span><span class="sxs-lookup"><span data-stu-id="18684-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![案例](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="18684-125">下載並了解 hello Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="18684-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="18684-126">您可以從 GitHub 下載現有 Azure Resource Manager 範本 toocreate hello 虛擬網路和兩個子網路，進行任何變更，您可能會想要並重複使用它。</span><span class="sxs-lookup"><span data-stu-id="18684-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="18684-127">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18684-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="18684-128">瀏覽過[啟用 web 應用程式防火牆的 建立應用程式閘道](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)。</span><span class="sxs-lookup"><span data-stu-id="18684-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="18684-129">依序按一下 [azuredeploy.json] 和 [RAW]。</span><span class="sxs-lookup"><span data-stu-id="18684-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="18684-130">在電腦上儲存 hello 檔案 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="18684-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="18684-131">如果您已熟悉 Azure 資源管理員範本，請略過 toostep 7。</span><span class="sxs-lookup"><span data-stu-id="18684-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="18684-132">開啟您儲存的 hello 檔案，並查看下 hello 內容**參數**一行</span><span class="sxs-lookup"><span data-stu-id="18684-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="18684-133">Azure 資源管理員範本的參數提供值的預留位置，可以在部署期間填寫。</span><span class="sxs-lookup"><span data-stu-id="18684-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="18684-134">參數</span><span class="sxs-lookup"><span data-stu-id="18684-134">Parameter</span></span> | <span data-ttu-id="18684-135">說明</span><span class="sxs-lookup"><span data-stu-id="18684-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="18684-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="18684-136">**subnetPrefix**</span></span> |<span data-ttu-id="18684-137">Hello 應用程式閘道子網路的 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="18684-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="18684-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="18684-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="18684-139">Hello 應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="18684-139">Size of hello application gateway.</span></span>  <span data-ttu-id="18684-140">WAF 只允許中型和大型。</span><span class="sxs-lookup"><span data-stu-id="18684-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="18684-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="18684-141">**backendIpaddress1**</span></span> |<span data-ttu-id="18684-142">Hello 第一部 web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18684-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="18684-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="18684-143">**backendIpaddress2**</span></span> |<span data-ttu-id="18684-144">Hello 第二部 web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18684-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="18684-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="18684-145">**wafEnabled**</span></span> | <span data-ttu-id="18684-146">如果已啟用 WAF，設定 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="18684-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="18684-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="18684-147">**wafMode**</span></span> | <span data-ttu-id="18684-148">Hello web 應用程式防火牆模式。</span><span class="sxs-lookup"><span data-stu-id="18684-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="18684-149">可用的選項為 **prevention** 或 **detection**。</span><span class="sxs-lookup"><span data-stu-id="18684-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="18684-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="18684-150">**wafRuleSetType**</span></span> | <span data-ttu-id="18684-151">WAF 的規則集類型。</span><span class="sxs-lookup"><span data-stu-id="18684-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="18684-152">目前 OWASP 是 hello 只支援的選項。</span><span class="sxs-lookup"><span data-stu-id="18684-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="18684-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="18684-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="18684-154">規則集版本。</span><span class="sxs-lookup"><span data-stu-id="18684-154">Ruleset version.</span></span> <span data-ttu-id="18684-155">OWASP CRS 2.2.9 和 3.0 目前正在 hello 支援選項。</span><span class="sxs-lookup"><span data-stu-id="18684-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="18684-156">檢查下的 hello 內容**資源**和注意事項 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="18684-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="18684-157">**type**。</span><span class="sxs-lookup"><span data-stu-id="18684-157">**type**.</span></span> <span data-ttu-id="18684-158">Hello 範本所建立的資源類型。</span><span class="sxs-lookup"><span data-stu-id="18684-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="18684-159">在此情況下，hello 類型是`Microsoft.Network/applicationGateways`，用來表示應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="18684-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="18684-160">**名稱**。</span><span class="sxs-lookup"><span data-stu-id="18684-160">**name**.</span></span> <span data-ttu-id="18684-161">Hello 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="18684-161">Name for hello resource.</span></span> <span data-ttu-id="18684-162">請注意 hello 使用`[parameters('applicationGatewayName')]`，這表示該 hello 名稱做為輸入您或參數檔期間所部署。</span><span class="sxs-lookup"><span data-stu-id="18684-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="18684-163">**屬性**。</span><span class="sxs-lookup"><span data-stu-id="18684-163">**properties**.</span></span> <span data-ttu-id="18684-164">Hello 資源屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="18684-164">List of properties for hello resource.</span></span> <span data-ttu-id="18684-165">此範本建立應用程式閘道期間將使用 hello 虛擬網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18684-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="18684-166">如需範本的詳細資訊，請造訪︰[Resource Manager 範本參考](/templates/)</span><span class="sxs-lookup"><span data-stu-id="18684-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="18684-167">瀏覽回太[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf)。</span><span class="sxs-lookup"><span data-stu-id="18684-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="18684-168">按一下 azuredeploy-parameters.json，然後按一下RAW。</span><span class="sxs-lookup"><span data-stu-id="18684-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="18684-169">在電腦上儲存 hello 檔案 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="18684-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="18684-170">開啟您儲存的 hello 檔案並編輯 hello hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="18684-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="18684-171">使用下列值 toodeploy hello 應用程式閘道我們的案例中所述的 hello。</span><span class="sxs-lookup"><span data-stu-id="18684-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="18684-172">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="18684-172">Save hello file.</span></span> <span data-ttu-id="18684-173">您可以使用線上 JSON 驗證工具，像是測試 hello JSON 範本和參數範本[JSlint.com](http://www.jslint.com/)。</span><span class="sxs-lookup"><span data-stu-id="18684-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="18684-174">使用 PowerShell 來部署 hello Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="18684-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="18684-175">如果您從未使用過 Azure PowerShell，請瀏覽：[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示 toosign 至 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18684-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="18684-176">登入 tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="18684-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="18684-177">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18684-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="18684-178">您必須提示的 tooauthenticate 和您的認證。</span><span class="sxs-lookup"><span data-stu-id="18684-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="18684-179">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="18684-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="18684-180">如有需要建立資源群組使用 hello**新增 AzureResourceGroup** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="18684-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="18684-181">在下列範例的 hello，您可以建立呼叫 AppgatewayRG 美國東部位置中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="18684-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="18684-182">執行 hello**新增 AzureRmResourceGroupDeployment** cmdlet toodeploy hello 新的虛擬網路使用 hello 前下載，並修改範本和參數檔案。</span><span class="sxs-lookup"><span data-stu-id="18684-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="18684-183">使用 Azure CLI hello 部署 hello Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="18684-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="18684-184">您使用 Azure CLI 下載 toodeploy hello Azure Resource Manager 範本，請依照下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18684-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="18684-185">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="18684-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="18684-186">如果有必要，請執行的 hello`az group create`命令 toocreate 資源群組，如下列程式碼片段的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="18684-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="18684-187">請注意 hello hello 命令輸出。</span><span class="sxs-lookup"><span data-stu-id="18684-187">Notice hello output of hello command.</span></span> <span data-ttu-id="18684-188">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="18684-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="18684-189">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="18684-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="18684-190">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="18684-190">**-n (or --name)**.</span></span> <span data-ttu-id="18684-191">Hello 新資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="18684-191">Name for hello new resource group.</span></span> <span data-ttu-id="18684-192">在本文案例中為「appgatewayRG」 。</span><span class="sxs-lookup"><span data-stu-id="18684-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="18684-193">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="18684-193">**-l (or --location)**.</span></span> <span data-ttu-id="18684-194">Hello 新資源群組建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="18684-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="18684-195">在我們的案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="18684-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="18684-196">執行 hello `az group deployment create` cmdlet toodeploy hello 新的虛擬網路使用 hello 範本和參數檔案，您可以下載並在 hello 前面步驟中修改。</span><span class="sxs-lookup"><span data-stu-id="18684-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="18684-197">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="18684-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="18684-198">使用部署按一下部署 hello Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="18684-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="18684-199">按一下 部署是另一個方式 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="18684-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="18684-200">它是以 hello Azure 入口網站輕鬆 toouse 範本。</span><span class="sxs-lookup"><span data-stu-id="18684-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="18684-201">跳過[建立 web 應用程式防火牆應用程式閘道](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)。</span><span class="sxs-lookup"><span data-stu-id="18684-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="18684-202">按一下**部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="18684-202">Click **Deploy tooAzure**.</span></span>

    ![部署 tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="18684-204">Hello hello 入口網站上的部署範本的 hello 參數，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="18684-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![參數](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="18684-206">選取**toohello 條款和條件前面所述，即表示我同意**按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="18684-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="18684-207">在 hello 自訂部署刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="18684-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="18684-208">提供憑證資料 tooResource 管理員範本</span><span class="sxs-lookup"><span data-stu-id="18684-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="18684-209">當使用範本中的 SSL，hello 憑證需要 toobe 而不是正在上傳的 base64 字串中提供。</span><span class="sxs-lookup"><span data-stu-id="18684-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="18684-210">tooconvert.pfx 或.cer tooa base64 字串可使用其中一個 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="18684-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="18684-211">hello 下列命令會將轉換 hello 憑證 tooa base64 字串，它可以提供 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="18684-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="18684-212">hello 預期輸出，則可以儲存在變數中，且在 hello 範本中貼上的字串。</span><span class="sxs-lookup"><span data-stu-id="18684-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="18684-213">macOS</span><span class="sxs-lookup"><span data-stu-id="18684-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="18684-214">Windows</span><span class="sxs-lookup"><span data-stu-id="18684-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="18684-215">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="18684-215">Delete all resources</span></span>

<span data-ttu-id="18684-216">toodelete 本文完成其中一個 hello 步驟中建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="18684-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="18684-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18684-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="18684-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18684-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="18684-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18684-219">Next steps</span></span>

<span data-ttu-id="18684-220">如果您想的 tooconfigure SSL 卸載，請造訪：[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="18684-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="18684-221">如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請造訪：[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="18684-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="18684-222">如果您想進一步了解一般負載平衡選項，請造訪：</span><span class="sxs-lookup"><span data-stu-id="18684-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="18684-223">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="18684-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="18684-224">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="18684-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

