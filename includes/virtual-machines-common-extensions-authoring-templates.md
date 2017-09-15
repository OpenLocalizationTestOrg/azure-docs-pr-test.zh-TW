## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="ad971-101">Azure 資源管理員範本概觀</span><span class="sxs-lookup"><span data-stu-id="ad971-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="ad971-102">Azure Resource Manager 範本可讓您藉由定義資源之間的相依性，以宣告方式指定 JSON 語言中的 Azure IaaS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ad971-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="ad971-103">如需 Azure Resource Manager 範本的詳細概觀，請參閱下文：</span><span class="sxs-lookup"><span data-stu-id="ad971-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="ad971-104">資源群組概觀</span><span class="sxs-lookup"><span data-stu-id="ad971-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="ad971-105">VM 擴充功能的範例範本程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ad971-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="ad971-106">若要將 VM 擴充功能部署到 Azure Resource Manager 範本中，您必須以宣告方式在範本中指定擴充功能組態。</span><span class="sxs-lookup"><span data-stu-id="ad971-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="ad971-107">以下是用來指定延伸模組組態的格式。</span><span class="sxs-lookup"><span data-stu-id="ad971-107">Here is the format for specifying the extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="ad971-108">您可以在以上程式碼中看到，延伸模組範本包含兩個主要部分：</span><span class="sxs-lookup"><span data-stu-id="ad971-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="ad971-109">擴充功能名稱、發行者和版本</span><span class="sxs-lookup"><span data-stu-id="ad971-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="ad971-110">延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="ad971-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="ad971-111">識別任何擴充功能的發行者、類型和 typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ad971-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="ad971-112">Azure VM 擴充功能是由 Microsoft 和受信任的第 3 方發行者所發佈，每個擴充功能會依其發行者、類型和 typeHandlerVersion 進行唯一識別。</span><span class="sxs-lookup"><span data-stu-id="ad971-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="ad971-113">其判斷方式如下：</span><span class="sxs-lookup"><span data-stu-id="ad971-113">These can be determined as following:</span></span>  

