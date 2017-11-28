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
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="5a7d7-103">IoT 套件的常見問題集</span><span class="sxs-lookup"><span data-stu-id="5a7d7-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="5a7d7-104">此外，請參閱 hello 連接的工廠特定[常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="5a7d7-105">可以在哪裡找到 hello 原始程式碼 hello 預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="5a7d7-106">hello 原始程式碼儲存在 hello 遵循 GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="5a7d7-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="5a7d7-107">[遠端監視預先設定的解決方案][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="5a7d7-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="5a7d7-108">[預先設定的預防性維護的解決方案][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="5a7d7-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="5a7d7-109">連線處理站預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="5a7d7-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="5a7d7-110">如何更新 toohello 最新版本的 hello 遠端監視預先設定解決方案會使用 hello IoT 中心裝置管理功能？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="5a7d7-111">如果您部署的 hello https://www.azureiotsuite.com/ 站台從預先設定的解決方案，它一定會將部署 hello hello 方案最新版本的新執行的個體。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="5a7d7-112">如果您部署使用 hello 命令列的預先設定的方案，您可以使用新的程式碼更新現有的部署。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="5a7d7-113">請參閱[雲端部署][ lnk-cloud-deployment] hello GitHub 中[儲存機制][lnk-remote-monitoring-github]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="5a7d7-114">如何新增支援遠端監視預先設定的解決方案新裝置方法 toohello？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="5a7d7-115">參閱 hello[加入新的方法 toohello 模擬器支援][ lnk-add-method]在 hello[來自訂預先設定的解決方案][ lnk-customize]發行項。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="5a7d7-116">hello 模擬的裝置會忽略我想要的屬性的變更，為何？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="5a7d7-117">在 hello 遠端監視預先設定的解決方案、 hello 模擬裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**所需屬性tooupdate hello 所報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="5a7d7-118">所有其他所需屬性變更要求都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="5a7d7-119">我的裝置未在 hello hello 方案儀表板中的裝置清單中顯示為何？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="5a7d7-120">裝置 hello 方案儀表板中的 hello 清單會使用查詢 tooreturn hello 的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="5a7d7-121">目前，查詢無法傳回超過 10,000 個裝置。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="5a7d7-122">請嘗試進行查詢的搜尋準則 hello 更具限制性。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="5a7d7-123">刪除資源群組 hello Azure 入口網站並按一下刪除 azureiotsuite.com 中預先設定的解決方案中的 hello 差異為何？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="5a7d7-124">如果您刪除中預先設定的 hello 方案[azureiotsuite.com][lnk-azureiotsuite]，刪除所有已佈建，當您建立預先設定的 hello 方案的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="5a7d7-125">如果您新增其他資源 toohello 資源群組，也會一併刪除這些資源。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="5a7d7-126">如果您刪除 hello 資源群組中 hello [Azure 入口網站][lnk-azure-portal]，您只能刪除該資源群組中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="5a7d7-127">您也需要 toodelete hello Azure Active Directory 應用程式與 hello 中預先設定的 hello 方案相關聯[Azure 傳統入口網站][lnk-classic-portal]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="5a7d7-128">我可以在一個訂用帳戶中佈建多少個 IoT 中樞執行個體？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="5a7d7-129">根據預設，您的佈建方式可以是[每個訂用帳戶 10 個 IoT 中樞][link-azuresublimits]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="5a7d7-130">您可以建立[Azure 支援票證][ link-azuresupportticket] tooraise 這項限制。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="5a7d7-131">如此一來，因為每個預先設定的解決方案佈建一個新的 IoT 中樞，您僅能佈建向上 too10 預先設定中指定的訂用帳戶的方案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="5a7d7-132">我可以在一個訂用帳戶中佈建多少個 Azure Cosmos DB 執行個體？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="5a7d7-133">50 個。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-133">Fifty.</span></span> <span data-ttu-id="5a7d7-134">您可以建立[Azure 支援票證][ link-azuresupportticket] tooraise 此限制，但根據預設，您可以只佈建 50 Cosmos 資料庫執行個體，每個訂閱。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="5a7d7-135">我可以在一個訂用帳戶中佈建多少個免費 Bing 地圖服務 API？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="5a7d7-136">2 個。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-136">Two.</span></span> <span data-ttu-id="5a7d7-137">您只可以在 Azure 訂用帳戶中針對 Enterprise 方案建立兩個內部交易層級 1 Bing 地圖。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="5a7d7-138">hello 遠端監視解決方案的佈建與 hello 內部交易層級 1 計劃的預設值。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="5a7d7-139">如此一來，您可以只佈建 tootwo 遠端監視解決方案，不需要修改的訂用帳戶中註冊。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="5a7d7-140">我有使用靜態地圖的遠端監視解決方案部署，如何加入互動式 Bing 地圖？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="5a7d7-141">從 [Azure 入口網站][lnk-azure-portal]取得 Bing Maps API for Enterprise QueryKey：</span><span class="sxs-lookup"><span data-stu-id="5a7d7-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="5a7d7-142">瀏覽 toohello 資源群組，其中您企業的 Bing Maps API 是以 hello [Azure 入口網站][lnk-azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="5a7d7-143">依序按一下 [所有設定] 和 [金鑰管理]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="5a7d7-144">您可以看到兩個金鑰︰**MasterKey** 和 **QueryKey**。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="5a7d7-145">複製 hello 值**QueryKey**。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="5a7d7-146">沒有 Bing Maps API for Enterprise 帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="5a7d7-147">在 hello 中建立一個[Azure 入口網站][ lnk-azure-portal]按一下 + 新、 Enterprise 和後續的 Bing Maps API 搜尋提示 toocreate。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="5a7d7-148">提取從 hello hello 最新的程式碼[Azure IoT-遠端-監視][lnk-remote-monitoring-github]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="5a7d7-149">執行本機或雲端部署下列 hello hello 儲存機制中的 hello /docs/ 資料夾中的命令列部署指南。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="5a7d7-150">您已執行本機或雲端部署中，查看 hello 根資料夾中之後 *。 在部署期間建立的 user.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="5a7d7-151">在文字編輯器中開啟這個檔案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="5a7d7-152">變更 hello 下列行 tooinclude hello 值從您複製您**QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="5a7d7-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="5a7d7-153">如果我有 Microsoft Azure for DreamSpark，是否可以建立預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="5a7d7-154">目前，您無法使用 [Microsoft Azure for DreamSpark][lnk-dreamspark] 帳戶來建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="5a7d7-155">不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="5a7d7-156">如果我有雲端方案提供者 (CSP) 訂用帳戶，是否可以建立預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="5a7d7-157">目前您無法透過雲端方案提供者 (CSP) 訂用帳戶建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="5a7d7-158">不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="5a7d7-159">如何刪除 AAD 租用戶？</span><span class="sxs-lookup"><span data-stu-id="5a7d7-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="5a7d7-160">請參閱 Eric Golpe 的部落格文章：[刪除 Azure AD 租用戶的逐步解說 (英文)][lnk-delete-aad-tennant]。</span><span class="sxs-lookup"><span data-stu-id="5a7d7-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="5a7d7-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a7d7-161">Next steps</span></span>

<span data-ttu-id="5a7d7-162">您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="5a7d7-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="5a7d7-163">[預先設定的預防性維護解決方案概觀][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="5a7d7-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="5a7d7-164">連線處理站預先設定的解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="5a7d7-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="5a7d7-165">[從 hello 接地 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="5a7d7-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
