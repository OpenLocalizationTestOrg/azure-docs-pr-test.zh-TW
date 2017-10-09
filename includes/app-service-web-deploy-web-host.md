### <a name="app-service-plan"></a>App Service 方案
建立 hello 裝載 hello web 應用程式的服務方案。 提供透過 hello hello 計劃 hello 名稱**hostingPlanName**參數。 hello 計劃 hello 位置是的 hello hello 資源群組使用相同的位置。 hello 定價層和背景工作大小指定在 hello **sku**和**workerSize**參數

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

