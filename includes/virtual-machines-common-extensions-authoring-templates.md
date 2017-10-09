## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="b31ce-101">Azure 資源管理員範本概觀</span><span class="sxs-lookup"><span data-stu-id="b31ce-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="b31ce-102">Azure 資源管理員範本可讓您 toodeclaratively hello Azure IaaS 基礎結構中指定 Json 語言定義 hello 資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="b31ce-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="b31ce-103">Azure 資源管理員範本的詳細概觀，請參閱下列文件 toohello:</span><span class="sxs-lookup"><span data-stu-id="b31ce-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="b31ce-104">資源群組概觀</span><span class="sxs-lookup"><span data-stu-id="b31ce-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="b31ce-105">VM 擴充功能的範例範本程式碼片段</span><span class="sxs-lookup"><span data-stu-id="b31ce-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="b31ce-106">Toodeclaratively 部署 VM 擴充功能的 Azure Resource Manager 範本部份需要您在 hello 範本中指定 hello 延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="b31ce-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="b31ce-107">以下是指定 hello 延伸模組組態 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="b31ce-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="b31ce-108">您可以看到從上述 hello，hello 擴充範本包含兩個主要部分：</span><span class="sxs-lookup"><span data-stu-id="b31ce-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="b31ce-109">擴充功能名稱、發行者和版本</span><span class="sxs-lookup"><span data-stu-id="b31ce-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="b31ce-110">延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="b31ce-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="b31ce-111">識別 hello 發行者、 類型和 typeHandlerVersion 的任何擴充功能</span><span class="sxs-lookup"><span data-stu-id="b31ce-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="b31ce-112">Microsoft 所發行的 azure VM 擴充功能而且要信任由其發行者、 類型和 hello typeHandlerVersion 唯一識別第 3 個合作對象發行者和每個擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b31ce-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="b31ce-113">其判斷方式如下：</span><span class="sxs-lookup"><span data-stu-id="b31ce-113">These can be determined as following:</span></span>  

