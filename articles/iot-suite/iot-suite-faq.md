---
title: "Azure IoT Suite 常見問題集 | Microsoft Docs"
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="f7b08-103">IoT 套件的常見問題集</span><span class="sxs-lookup"><span data-stu-id="f7b08-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="f7b08-104">另請參閱，連線處理站專用的[常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="f7b08-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="f7b08-105">哪裡可以找到預先設定之解決方案的原始程式碼？</span><span class="sxs-lookup"><span data-stu-id="f7b08-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="f7b08-106">原始程式碼儲存在下列 GitHub 儲存機制中︰</span><span class="sxs-lookup"><span data-stu-id="f7b08-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="f7b08-107">[遠端監視預先設定的解決方案][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="f7b08-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="f7b08-108">[預先設定的預防性維護的解決方案][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="f7b08-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="f7b08-109">連線處理站預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="f7b08-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="f7b08-110">如何更新為最新版預先設定的遠端監視解決方案，其使用 IoT 中樞裝置管理功能？</span><span class="sxs-lookup"><span data-stu-id="f7b08-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="f7b08-111">如果您從 https://www.azureiotsuite.com/ 網站部署預先設定的解決方案，一律會部署最新版解決方案的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7b08-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="f7b08-112">如果您使用命令列來部署預先設定的解決方案，您可以使用新的程式碼來更新現有的部署。</span><span class="sxs-lookup"><span data-stu-id="f7b08-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="f7b08-113">請參閱 GitHub [儲存機制][lnk-remote-monitoring-github]中的[雲端部署][lnk-cloud-deployment]。</span><span class="sxs-lookup"><span data-stu-id="f7b08-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f7b08-114">如何將新裝置方法的支援新增至預先設定的遠端監視解決方案？</span><span class="sxs-lookup"><span data-stu-id="f7b08-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="f7b08-115">請參閱[自訂預先設定的解決方案][lnk-customize]一文中的[將新方法的支援新增至模擬器][lnk-add-method]一節。</span><span class="sxs-lookup"><span data-stu-id="f7b08-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="f7b08-116">模擬裝置會忽略我的所需屬性變更，為什麼？</span><span class="sxs-lookup"><span data-stu-id="f7b08-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="f7b08-117">在預先設定的遠端監視解決方案中，模擬裝置程式碼只會使用 **Desired.Config.TemperatureMeanValue** 和 **Desired.Config.TelemetryInterval** 所需屬性來更新報告屬性。</span><span class="sxs-lookup"><span data-stu-id="f7b08-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="f7b08-118">所有其他所需屬性變更要求都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="f7b08-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="f7b08-119">我的裝置未顯示於解決方案儀表板的裝置清單中，為什麼？</span><span class="sxs-lookup"><span data-stu-id="f7b08-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="f7b08-120">解決方案儀表板中的裝置清單會使用查詢來傳回裝置清單。</span><span class="sxs-lookup"><span data-stu-id="f7b08-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="f7b08-121">目前，查詢無法傳回超過 10,000 個裝置。</span><span class="sxs-lookup"><span data-stu-id="f7b08-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="f7b08-122">試著讓查詢的搜尋準則更具限制性。</span><span class="sxs-lookup"><span data-stu-id="f7b08-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="f7b08-123">在 Azure 入口網站中刪除資源群組，與在 azureiotsuite.com 中對預先設定解決方案按一下 [刪除] 之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="f7b08-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="f7b08-124">如果您在 [azureiotsuite.com][lnk-azureiotsuite] 中刪除預先設定的解決方案，將會刪除您在建立該預先設定解決方案時所佈建的一切資源。</span><span class="sxs-lookup"><span data-stu-id="f7b08-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="f7b08-125">將額外資源新增到資源群組時，也會一併刪除這些資源。</span><span class="sxs-lookup"><span data-stu-id="f7b08-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="f7b08-126">如果您在 [Azure 入口網站][lnk-azure-portal]中刪除資源群組，則只會刪除該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="f7b08-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="f7b08-127">您還必須在 [Azure 傳統入口網站][lnk-classic-portal]中刪除與預先設定的解決方案關聯的 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b08-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="f7b08-128">我可以在一個訂用帳戶中佈建多少個 IoT 中樞執行個體？</span><span class="sxs-lookup"><span data-stu-id="f7b08-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="f7b08-129">根據預設，您的佈建方式可以是[每個訂用帳戶 10 個 IoT 中樞][link-azuresublimits]。</span><span class="sxs-lookup"><span data-stu-id="f7b08-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="f7b08-130">您可以建立 [Azure 支援票證][link-azuresupportticket]來提高此限制。</span><span class="sxs-lookup"><span data-stu-id="f7b08-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="f7b08-131">結果就是，由於每個預先設定的解決方案會佈建一個新的「IoT 中樞」，因此在一個指定的訂用帳戶中，您最多只能佈建 10 個預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="f7b08-132">我可以在一個訂用帳戶中佈建多少個 Azure Cosmos DB 執行個體？</span><span class="sxs-lookup"><span data-stu-id="f7b08-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="f7b08-133">50 個。</span><span class="sxs-lookup"><span data-stu-id="f7b08-133">Fifty.</span></span> <span data-ttu-id="f7b08-134">您可以建立 [Azure 支援票證][link-azuresupportticket]來提高此限制，但每一個訂用帳戶預設只能佈建 50 個 Cosmos DB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7b08-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="f7b08-135">我可以在一個訂用帳戶中佈建多少個免費 Bing 地圖服務 API？</span><span class="sxs-lookup"><span data-stu-id="f7b08-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="f7b08-136">2 個。</span><span class="sxs-lookup"><span data-stu-id="f7b08-136">Two.</span></span> <span data-ttu-id="f7b08-137">您只可以在 Azure 訂用帳戶中針對 Enterprise 方案建立兩個內部交易層級 1 Bing 地圖。</span><span class="sxs-lookup"><span data-stu-id="f7b08-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="f7b08-138">根據預設，遠端監視方案會隨著內部交易層級 1 方案一起佈建。</span><span class="sxs-lookup"><span data-stu-id="f7b08-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="f7b08-139">因此，您只可以在一個訂用帳戶中最多佈建 2 個遠端監視方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="f7b08-140">我有使用靜態地圖的遠端監視解決方案部署，如何加入互動式 Bing 地圖？</span><span class="sxs-lookup"><span data-stu-id="f7b08-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="f7b08-141">從 [Azure 入口網站][lnk-azure-portal]取得 Bing Maps API for Enterprise QueryKey：</span><span class="sxs-lookup"><span data-stu-id="f7b08-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="f7b08-142">在 [Azure 入口網站][lnk-azure-portal]中瀏覽至 Bing Maps API for Enterprise 所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f7b08-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="f7b08-143">依序按一下 [所有設定] 和 [金鑰管理]。</span><span class="sxs-lookup"><span data-stu-id="f7b08-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="f7b08-144">您可以看到兩個金鑰︰**MasterKey** 和 **QueryKey**。</span><span class="sxs-lookup"><span data-stu-id="f7b08-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="f7b08-145">請複製 **QueryKey** 的值。</span><span class="sxs-lookup"><span data-stu-id="f7b08-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f7b08-146">沒有 Bing Maps API for Enterprise 帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="f7b08-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="f7b08-147">請在 [Azure 入口網站][lnk-azure-portal]中按一下 [+ 新增]、搜尋 Bing Maps API for Enterprise，然後依照提示來建立一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7b08-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="f7b08-148">從 [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github] 下拉最新的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f7b08-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="f7b08-149">依照儲存機制的 /docs/ 資料夾中的命令列部署指引，執行本機或雲端部署。</span><span class="sxs-lookup"><span data-stu-id="f7b08-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="f7b08-150">執行本機或雲端部署之後，在您的根資料夾中尋找部署期間所建立的 *.user.config。</span><span class="sxs-lookup"><span data-stu-id="f7b08-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="f7b08-151">在文字編輯器中開啟這個檔案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="f7b08-152">變更下列這一行，使其包含從 **QueryKey** 複製的值︰</span><span class="sxs-lookup"><span data-stu-id="f7b08-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="f7b08-153">如果我有 Microsoft Azure for DreamSpark，是否可以建立預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="f7b08-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="f7b08-154">目前，您無法使用 [Microsoft Azure for DreamSpark][lnk-dreamspark] 帳戶來建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="f7b08-155">不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="f7b08-156">如果我有雲端方案提供者 (CSP) 訂用帳戶，是否可以建立預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="f7b08-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="f7b08-157">目前您無法透過雲端方案提供者 (CSP) 訂用帳戶建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="f7b08-158">不過，您只需花幾分鐘即可建立 [Azure 免費試用帳戶][lnk-30daytrial]，此帳戶可讓您建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7b08-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="f7b08-159">如何刪除 AAD 租用戶？</span><span class="sxs-lookup"><span data-stu-id="f7b08-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="f7b08-160">請參閱 Eric Golpe 的部落格文章：[刪除 Azure AD 租用戶的逐步解說 (英文)][lnk-delete-aad-tennant]。</span><span class="sxs-lookup"><span data-stu-id="f7b08-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="f7b08-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7b08-161">Next steps</span></span>

<span data-ttu-id="f7b08-162">您也可以瀏覽一些其他功能和預先設定的 IoT 套件解決方案的功能︰</span><span class="sxs-lookup"><span data-stu-id="f7b08-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="f7b08-163">[預先設定的預防性維護解決方案概觀][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="f7b08-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="f7b08-164">連線處理站預先設定的解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="f7b08-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="f7b08-165">[從頭建立 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="f7b08-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
