---
title: "建立 Azure 應用程式閘道 - 範本 | Microsoft Docs"
description: "本頁面提供使用 Azure 資源管理員範本，建立 Azure 應用程式閘道的指示。"
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="02d71-103">使用 Azure 資源管理員範本建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="02d71-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02d71-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="02d71-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="02d71-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="02d71-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="02d71-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="02d71-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="02d71-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="02d71-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="02d71-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02d71-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="02d71-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="02d71-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="02d71-110">不論是在雲端或內部部署環境中，此閘道均提供在不同伺服器之間進行容錯移轉及效能路由傳送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="02d71-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="02d71-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="02d71-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="02d71-112">若要尋找完整的支援功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="02d71-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="02d71-113">本文會逐步引導您從 GitHub 下載和修改現有 Azure Resource Manager 範本，以及從 GitHub、PowerShell 和 Azure CLI 部署範本。</span><span class="sxs-lookup"><span data-stu-id="02d71-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="02d71-114">如果您只需直接從 GitHub 部署 Azure 資源管理員範本而不做任何變更，請跳至＜從 GitHub 部署範本＞。</span><span class="sxs-lookup"><span data-stu-id="02d71-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="02d71-115">案例</span><span class="sxs-lookup"><span data-stu-id="02d71-115">Scenario</span></span>

<span data-ttu-id="02d71-116">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="02d71-116">In this scenario you will:</span></span>

* <span data-ttu-id="02d71-117">建立具有 Web 應用程式防火牆的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="02d71-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="02d71-118">建立名為 VirtualNetwork1 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="02d71-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="02d71-119">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="02d71-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="02d71-120">針對想要用來為流量進行負載平衡的 Web 伺服器，設定兩個先前所設定的後端 IP。</span><span class="sxs-lookup"><span data-stu-id="02d71-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="02d71-121">在此範本範例中，後端 IP 是 10.0.1.10 和 10.0.1.11。</span><span class="sxs-lookup"><span data-stu-id="02d71-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="02d71-122">這些設定都是適用於此範本的參數。</span><span class="sxs-lookup"><span data-stu-id="02d71-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="02d71-123">若要自訂範本，您可以在 azuredeploy.json 檔案中變更規則、接聽程式、SSL 和其他選項。</span><span class="sxs-lookup"><span data-stu-id="02d71-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![案例](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="02d71-125">下載並了解 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="02d71-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="02d71-126">您可以下載現有 Azure 資源管理員範本，以透過 Github 建立虛擬網路和兩個子網路，然後進行任何需要的變更，並重複使用該範本。</span><span class="sxs-lookup"><span data-stu-id="02d71-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="02d71-127">若要這樣做，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="02d71-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="02d71-128">瀏覽至[建立已啟用 Web 應用程式防火牆的應用程式閘道](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)</span><span class="sxs-lookup"><span data-stu-id="02d71-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="02d71-129">依序按一下 [azuredeploy.json] 和 [RAW]。</span><span class="sxs-lookup"><span data-stu-id="02d71-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="02d71-130">將檔案儲存至您電腦上的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="02d71-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="02d71-131">如果您熟悉 Azure 資源管理員範本的使用方式，請跳至步驟 7。</span><span class="sxs-lookup"><span data-stu-id="02d71-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="02d71-132">開啟您儲存的檔案，查看 **parameters** 這行下方的內容。</span><span class="sxs-lookup"><span data-stu-id="02d71-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="02d71-133">Azure 資源管理員範本的參數提供值的預留位置，可以在部署期間填寫。</span><span class="sxs-lookup"><span data-stu-id="02d71-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="02d71-134">參數</span><span class="sxs-lookup"><span data-stu-id="02d71-134">Parameter</span></span> | <span data-ttu-id="02d71-135">說明</span><span class="sxs-lookup"><span data-stu-id="02d71-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="02d71-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="02d71-136">**subnetPrefix**</span></span> |<span data-ttu-id="02d71-137">應用程式閘道子網路的 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="02d71-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="02d71-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="02d71-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="02d71-139">應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="02d71-139">Size of the application gateway.</span></span>  <span data-ttu-id="02d71-140">WAF 只允許中型和大型。</span><span class="sxs-lookup"><span data-stu-id="02d71-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="02d71-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="02d71-141">**backendIpaddress1**</span></span> |<span data-ttu-id="02d71-142">第一部 Web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02d71-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="02d71-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="02d71-143">**backendIpaddress2**</span></span> |<span data-ttu-id="02d71-144">第二部 Web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02d71-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="02d71-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="02d71-145">**wafEnabled**</span></span> | <span data-ttu-id="02d71-146">用於判斷 WAF 是否已啟用的設定。</span><span class="sxs-lookup"><span data-stu-id="02d71-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="02d71-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="02d71-147">**wafMode**</span></span> | <span data-ttu-id="02d71-148">Web 應用程式防火牆的模式。</span><span class="sxs-lookup"><span data-stu-id="02d71-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="02d71-149">可用的選項為 **prevention** 或 **detection**。</span><span class="sxs-lookup"><span data-stu-id="02d71-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="02d71-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="02d71-150">**wafRuleSetType**</span></span> | <span data-ttu-id="02d71-151">WAF 的規則集類型。</span><span class="sxs-lookup"><span data-stu-id="02d71-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="02d71-152">目前，OWASP 是唯一支援的選項。</span><span class="sxs-lookup"><span data-stu-id="02d71-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="02d71-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="02d71-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="02d71-154">規則集版本。</span><span class="sxs-lookup"><span data-stu-id="02d71-154">Ruleset version.</span></span> <span data-ttu-id="02d71-155">OWASP CRS 2.2.9 和 3.0 是目前支援的選項。</span><span class="sxs-lookup"><span data-stu-id="02d71-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="02d71-156">檢查 **resources** 下方的內容，並注意下列屬性：</span><span class="sxs-lookup"><span data-stu-id="02d71-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="02d71-157">**type**。</span><span class="sxs-lookup"><span data-stu-id="02d71-157">**type**.</span></span> <span data-ttu-id="02d71-158">範本所建立的資源類型。</span><span class="sxs-lookup"><span data-stu-id="02d71-158">Type of resource being created by the template.</span></span> <span data-ttu-id="02d71-159">在此案例中，類型是 `Microsoft.Network/applicationGateways`，代表應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="02d71-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="02d71-160">**名稱**。</span><span class="sxs-lookup"><span data-stu-id="02d71-160">**name**.</span></span> <span data-ttu-id="02d71-161">資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="02d71-161">Name for the resource.</span></span> <span data-ttu-id="02d71-162">請注意 `[parameters('applicationGatewayName')]` 的用法，這表示此名稱是在部署期間由您輸入的內容，或是由參數檔案所提供。</span><span class="sxs-lookup"><span data-stu-id="02d71-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="02d71-163">**屬性**。</span><span class="sxs-lookup"><span data-stu-id="02d71-163">**properties**.</span></span> <span data-ttu-id="02d71-164">資源屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="02d71-164">List of properties for the resource.</span></span> <span data-ttu-id="02d71-165">此範本會在應用程式閘道建立期間，使用虛擬網路與公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02d71-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02d71-166">如需範本的詳細資訊，請造訪︰[Resource Manager 範本參考](/templates/)</span><span class="sxs-lookup"><span data-stu-id="02d71-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="02d71-167">瀏覽回 [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="02d71-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="02d71-168">按一下 [azuredeploy-parameters.json]，然後按一下 [RAW]。</span><span class="sxs-lookup"><span data-stu-id="02d71-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="02d71-169">將檔案儲存至您電腦上的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="02d71-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="02d71-170">開啟您儲存的檔案，以編輯參數的值。</span><span class="sxs-lookup"><span data-stu-id="02d71-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="02d71-171">使用下列值來部署本文案例所述的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="02d71-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="02d71-172">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="02d71-172">Save the file.</span></span> <span data-ttu-id="02d71-173">您可以使用線上 JSON 驗證工具 (例如 [JSlint.com](http://www.jslint.com/))，來測試 JSON 範本和參數範本。</span><span class="sxs-lookup"><span data-stu-id="02d71-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="02d71-174">使用 PowerShell 來部署 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="02d71-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="02d71-175">如果您從未用過 Azure PowerShell，請造訪：[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)，並遵循指示登入 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="02d71-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="02d71-176">登入 PowerShell</span><span class="sxs-lookup"><span data-stu-id="02d71-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="02d71-177">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="02d71-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="02d71-178">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="02d71-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="02d71-179">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="02d71-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="02d71-180">如有需要，請使用 **New-AzureResourceGroup** Cmdlet 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="02d71-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="02d71-181">在下列範例中，您會在美國東部位置建立名為 AppgatewayRG 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="02d71-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="02d71-182">執行 **New-AzureRmResourceGroupDeployment** Cmdlet，使用先前下載並修改的範本和參數檔案來部署新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="02d71-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="02d71-183">使用 Azure CLI 來部署 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="02d71-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="02d71-184">若要使用 Azure CLI 部署您下載的 Azure Resource Manager 範本，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="02d71-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="02d71-185">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](/cli/azure/install-azure-cli) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="02d71-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="02d71-186">如有必要，請執行 `az group create` 命令建立新的資源群組，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="02d71-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="02d71-187">請查看命令的輸出內容。</span><span class="sxs-lookup"><span data-stu-id="02d71-187">Notice the output of the command.</span></span> <span data-ttu-id="02d71-188">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="02d71-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="02d71-189">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="02d71-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="02d71-190">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="02d71-190">**-n (or --name)**.</span></span> <span data-ttu-id="02d71-191">新資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="02d71-191">Name for the new resource group.</span></span> <span data-ttu-id="02d71-192">在本文案例中為「appgatewayRG」 。</span><span class="sxs-lookup"><span data-stu-id="02d71-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="02d71-193">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="02d71-193">**-l (or --location)**.</span></span> <span data-ttu-id="02d71-194">建立新資源群組的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="02d71-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="02d71-195">在我們的案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="02d71-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="02d71-196">執行 `az group deployment create` Cmdlet，使用在上一個步驟中下載並修改的範本和參數檔案來部署新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="02d71-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="02d71-197">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="02d71-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="02d71-198">使用「按一下即部署」來部署 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="02d71-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="02d71-199">「按一下即部署」是另一種使用 Azure 資源管理員範本的方式。</span><span class="sxs-lookup"><span data-stu-id="02d71-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="02d71-200">這是將範本與 Azure 入口網站搭配使用的簡便方法。</span><span class="sxs-lookup"><span data-stu-id="02d71-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="02d71-201">移至[建立具有 Web 應用程式防火牆的應用程式閘道](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)。</span><span class="sxs-lookup"><span data-stu-id="02d71-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="02d71-202">按一下 [ **部署至 Azure**]。</span><span class="sxs-lookup"><span data-stu-id="02d71-202">Click **Deploy to Azure**.</span></span>

    ![部署至 Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="02d71-204">在入口網站上填寫適用於部署範本的參數，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="02d71-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![參數](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="02d71-206">選取 [我同意上方所述的條款及條件]，按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="02d71-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="02d71-207">在 [自訂部署] 刀鋒視窗上，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="02d71-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="02d71-208">提供 Resource Manager 範本的憑證資料</span><span class="sxs-lookup"><span data-stu-id="02d71-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="02d71-209">使用 SSL 搭配範本時，必須以 base64 字串形式提供憑證，而不是上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="02d71-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="02d71-210">若要將 .pfx 或 .cer 轉換為 Base64 字串，請使用下列其中一個命令。</span><span class="sxs-lookup"><span data-stu-id="02d71-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="02d71-211">下列命令會將憑證轉換為可以提供給範本的 Base64 字串。</span><span class="sxs-lookup"><span data-stu-id="02d71-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="02d71-212">預期的輸出是可以儲存在變數並貼在範本中的字串。</span><span class="sxs-lookup"><span data-stu-id="02d71-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="02d71-213">macOS</span><span class="sxs-lookup"><span data-stu-id="02d71-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="02d71-214">Windows</span><span class="sxs-lookup"><span data-stu-id="02d71-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="02d71-215">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="02d71-215">Delete all resources</span></span>

<span data-ttu-id="02d71-216">若要刪除這篇文章中建立的所有資源，請完成下列其中一個步驟：</span><span class="sxs-lookup"><span data-stu-id="02d71-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="02d71-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02d71-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="02d71-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02d71-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="02d71-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02d71-219">Next steps</span></span>

<span data-ttu-id="02d71-220">如果您想要設定 SSL 卸載，請造訪：[設定應用程式閘道以進行 SSL 卸載](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="02d71-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="02d71-221">如果您想要將應用程式閘道設為與內部負載平衡器搭配使用，請造訪：[建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="02d71-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="02d71-222">如果您想進一步了解一般負載平衡選項，請造訪：</span><span class="sxs-lookup"><span data-stu-id="02d71-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="02d71-223">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="02d71-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="02d71-224">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="02d71-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

