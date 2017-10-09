## <a name="overview-of-azure-resource-manager-templates"></a>Azure 資源管理員範本概觀
Azure 資源管理員範本可讓您 toodeclaratively hello Azure IaaS 基礎結構中指定 Json 語言定義 hello 資源之間的相依性。 Azure 資源管理員範本的詳細概觀，請參閱下列文件 toohello:

[資源群組概觀](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>VM 擴充功能的範例範本程式碼片段
Toodeclaratively 部署 VM 擴充功能的 Azure Resource Manager 範本部份需要您在 hello 範本中指定 hello 延伸模組組態。
以下是指定 hello 延伸模組組態 hello 格式。

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

您可以看到從上述 hello，hello 擴充範本包含兩個主要部分：

1. 擴充功能名稱、發行者和版本
2. 延伸模組組態。

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>識別 hello 發行者、 類型和 typeHandlerVersion 的任何擴充功能
Microsoft 所發行的 azure VM 擴充功能而且要信任由其發行者、 類型和 hello typeHandlerVersion 唯一識別第 3 個合作對象發行者和每個擴充功能。 其判斷方式如下：  

