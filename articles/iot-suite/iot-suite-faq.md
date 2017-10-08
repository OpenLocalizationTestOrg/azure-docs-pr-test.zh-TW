---
title: "aaaAzure IoT 套件常見問題集 |Microsoft 文件"
description: "IoT 套件的常見問題集"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>IoT 套件的常見問題集

此外，請參閱 hello 連接的工廠特定[常見問題集](iot-suite-faq-cf.md)。

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>可以在哪裡找到 hello 原始程式碼 hello 預先設定的解決方案？

hello 原始程式碼儲存在 hello 遵循 GitHub 儲存機制：
* [遠端監視預先設定的解決方案][lnk-remote-monitoring-github]
* [預先設定的預防性維護的解決方案][lnk-predictive-maintenance-github]
* [連線處理站預先設定的解決方案](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>如何更新 toohello 最新版本的 hello 遠端監視預先設定解決方案會使用 hello IoT 中心裝置管理功能？

* 如果您部署的 hello https://www.azureiotsuite.com/ 站台從預先設定的解決方案，它一定會將部署 hello hello 方案最新版本的新執行的個體。
* 如果您部署使用 hello 命令列的預先設定的方案，您可以使用新的程式碼更新現有的部署。 請參閱[雲端部署][ lnk-cloud-deployment] hello GitHub 中[儲存機制][lnk-remote-monitoring-github]。

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>如何新增支援遠端監視預先設定的解決方案新裝置方法 toohello？

參閱 hello[加入新的方法 toohello 模擬器支援][ lnk-add-method]在 hello[來自訂預先設定的解決方案][ lnk-customize]發行項。

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>hello 模擬的裝置會忽略我想要的屬性的變更，為何？
在 hello 遠端監視預先設定的解決方案、 hello 模擬裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**所需屬性tooupdate hello 所報告的屬性。 所有其他所需屬性變更要求都會被忽略。

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>我的裝置未在 hello hello 方案儀表板中的裝置清單中顯示為何？

裝置 hello 方案儀表板中的 hello 清單會使用查詢 tooreturn hello 的裝置清單。 目前，查詢無法傳回超過 10,000 個裝置。 請嘗試進行查詢的搜尋準則 hello 更具限制性。

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>刪除資源群組 hello Azure 入口網站並按一下刪除 azureiotsuite.com 中預先設定的解決方案中的 hello 差異為何？

* 如果您刪除中預先設定的 hello 方案[azureiotsuite.com][lnk-azureiotsuite]，刪除所有已佈建，當您建立預先設定的 hello 方案的 hello 資源。 如果您新增其他資源 toohello 資源群組，也會一併刪除這些資源。 
* 如果您刪除 hello 資源群組中 hello [Azure 入口網站][lnk-azure-portal]，您只能刪除該資源群組中的 hello 資源。 您也需要 toodelete hello Azure Active Directory 應用程式與 hello 中預先設定的 hello 方案相關聯[Azure 傳統入口網站][lnk-classic-portal]。

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>我可以在一個訂用帳戶中佈建多少個 IoT 中樞執行個體？

根據預設，您的佈建方式可以是[每個訂用帳戶 10 個 IoT 中樞][link-azuresublimits]。 您可以建立[Azure 支援票證][ link-azuresupportticket] tooraise 這項限制。 如此一來，因為每個預先設定的解決方案佈建一個新的 IoT 中樞，您僅能佈建向上 too10 預先設定中指定的訂用帳戶的方案。 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>我可以在一個訂用帳戶中佈建多少個 Azure Cosmos DB 執行個體？

50 個。 您可以建立[Azure 支援票證][ link-azuresupportticket] tooraise 此限制，但根據預設，您可以只佈建 50 Cosmos 資料庫執行個體，每個訂閱。 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>我可以在一個訂用帳戶中佈建多少個免費 Bing 地圖服務 API？

2 個。 您只可以在 Azure 訂用帳戶中針對 Enterprise 方案建立兩個內部交易層級 1 Bing 地圖。 hello 遠端監視解決方案的佈建與 hello 內部交易層級 1 計劃的預設值。 如此一來，您可以只佈建 tootwo 遠端監視解決方案，不需要修改的訂用帳戶中註冊。

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>我有使用靜態地圖的遠端監視解決方案部署，如何加入互動式 Bing 地圖？

1. 從 [Azure 入口網站][lnk-azure-portal]取得 Bing Maps API for Enterprise QueryKey： 
   
   1. 瀏覽 toohello 資源群組，其中您企業的 Bing Maps API 是以 hello [Azure 入口網站][lnk-azure-portal]。
   2. 依序按一下 [所有設定] 和 [金鑰管理]。 
   3. 您可以看到兩個金鑰︰**MasterKey** 和 **QueryKey**。 複製 hello 值**QueryKey**。
      
      > [!NOTE]
      > 沒有 Bing Maps API for Enterprise 帳戶嗎？ 在 hello 中建立一個[Azure 入口網站][ lnk-azure-portal]按一下 + 新、 Enterprise 和後續的 Bing Maps API 搜尋提示 toocreate。
      > 
      > 
2. 提取從 hello hello 最新的程式碼[Azure IoT-遠端-監視][lnk-remote-monitoring-github]。
3. 執行本機或雲端部署下列 hello hello 儲存機制中的 hello /docs/ 資料夾中的命令列部署指南。 
4. 您已執行本機或雲端部署中，查看 hello 根資料夾中之後 *。 在部署期間建立的 user.config 檔案。 在文字編輯器中開啟這個檔案。 
5. 變更 hello 下列行 tooinclude hello 值從您複製您**QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>如果我有 Microsoft Azure for DreamSpark，是否可以建立預先設定的解決方案？

目前，您無法使用 [Microsoft Azure for DreamSpark][lnk-dreamspark] 帳戶來建立預先設定的解決方案。 不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>如果我有雲端方案提供者 (CSP) 訂用帳戶，是否可以建立預先設定的解決方案？

目前您無法透過雲端方案提供者 (CSP) 訂用帳戶建立預先設定的解決方案。 不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。

### <a name="how-do-i-delete-an-aad-tenant"></a>如何刪除 AAD 租用戶？

請參閱 Eric Golpe 的部落格文章：[刪除 Azure AD 租用戶的逐步解說 (英文)][lnk-delete-aad-tennant]。

### <a name="next-steps"></a>後續步驟

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [連線處理站預先設定的解決方案概觀](iot-suite-connected-factory-overview.md)
* [從 hello 接地 IoT 安全性][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
