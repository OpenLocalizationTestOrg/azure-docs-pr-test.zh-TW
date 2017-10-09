---
title: "aaaLearn toomanage AzureML web 服務使用 API 管理 |Microsoft 文件"
description: "顯示如何 toomanage AzureML web 服務以使用 API 管理指南。"
keywords: "機器學習,api 管理"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="66a04-104">了解如何 toomanage AzureML web 服務以使用 API 管理</span><span class="sxs-lookup"><span data-stu-id="66a04-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="66a04-105">概觀</span><span class="sxs-lookup"><span data-stu-id="66a04-105">Overview</span></span>
<span data-ttu-id="66a04-106">本指南也說明如何 tooquickly 開始使用 API 管理 toomanage AzureML web 服務。</span><span class="sxs-lookup"><span data-stu-id="66a04-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="66a04-107">什麼是 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="66a04-107">What is Azure API Management?</span></span>
<span data-ttu-id="66a04-108">Azure API 管理是一項 Azure 服務，可讓您藉由定義使用者存取、使用節流設定和儀表板監視，來管理 REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="66a04-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="66a04-109">如需 Azure API 管理的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/api-management/) 。</span><span class="sxs-lookup"><span data-stu-id="66a04-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="66a04-110">按一下[這裡](../api-management/api-management-get-started.md)上 tooget 如何開始使用 Azure API 管理指南。</span><span class="sxs-lookup"><span data-stu-id="66a04-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="66a04-111">這是本指南所依據的另一份指南，涵蓋更多主題，包括通知組態、定價層、回應處理、使用者驗證、建立產品、開發人員訂用帳戶和使用量儀表板。</span><span class="sxs-lookup"><span data-stu-id="66a04-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="66a04-112">什麼是 AzureML？</span><span class="sxs-lookup"><span data-stu-id="66a04-112">What is AzureML?</span></span>
<span data-ttu-id="66a04-113">AzureML 是一項 Azure 服務的機器學習服務，可讓您 tooeasily 組建、 部署及共用進階的分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="66a04-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="66a04-114">如需 AzureML 的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/machine-learning/) 。</span><span class="sxs-lookup"><span data-stu-id="66a04-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66a04-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="66a04-115">Prerequisites</span></span>
<span data-ttu-id="66a04-116">toocomplete 本指南中，您需要：</span><span class="sxs-lookup"><span data-stu-id="66a04-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="66a04-117">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="66a04-117">An Azure account.</span></span> <span data-ttu-id="66a04-118">如果您沒有 Azure 帳戶，按一下[這裡](https://azure.microsoft.com/pricing/free-trial/)的詳細資料 toocreate 免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66a04-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="66a04-119">AzureML 帳戶。</span><span class="sxs-lookup"><span data-stu-id="66a04-119">An AzureML account.</span></span> <span data-ttu-id="66a04-120">如果您沒有 AzureML 帳戶，按一下[這裡](https://studio.azureml.net/)的詳細資料 toocreate 免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66a04-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="66a04-121">hello 工作區、 服務及部署為 web 服務 AzureML 實驗 api_key。</span><span class="sxs-lookup"><span data-stu-id="66a04-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="66a04-122">按一下[這裡](machine-learning-create-experiment.md)如 toocreate AzureML 的進行實驗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66a04-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="66a04-123">按一下[這裡](machine-learning-publish-a-machine-learning-web-service.md)如 toodeploy AzureML 實驗為 web 服務的方式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66a04-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="66a04-124">或者，附錄 A 中的方式 toocreate 和測試簡單 AzureML 實驗，並將其部署為 web 服務的指示。</span><span class="sxs-lookup"><span data-stu-id="66a04-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="66a04-125">建立 API 管理執行個體</span><span class="sxs-lookup"><span data-stu-id="66a04-125">Create an API Management instance</span></span>
<span data-ttu-id="66a04-126">以下是使用 API 管理 toomanage hello 步驟 AzureML web 服務。</span><span class="sxs-lookup"><span data-stu-id="66a04-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="66a04-127">首先建立服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="66a04-127">First create a service instance.</span></span> <span data-ttu-id="66a04-128">登入 toohello[傳統入口網站](https://manage.windowsazure.com/)按一下**新增** > **應用程式服務** > **API 管理** > **建立**。</span><span class="sxs-lookup"><span data-stu-id="66a04-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![建立執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="66a04-130">指定唯一的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="66a04-130">Specify a unique **URL**.</span></span> <span data-ttu-id="66a04-131">本指南使用**demoazureml** – 您將需要 toochoose 項目不同。</span><span class="sxs-lookup"><span data-stu-id="66a04-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="66a04-132">選擇所需的 hello**訂用帳戶**和**區域**服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="66a04-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="66a04-133">之後您的選擇，請按一下 hello 下一步 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66a04-133">After making your selections, click hello next button.</span></span>

![建立服務 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="66a04-135">指定的值為 hello**組織名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="66a04-136">本指南使用**demoazureml** – 您將需要 toochoose 項目不同。</span><span class="sxs-lookup"><span data-stu-id="66a04-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="66a04-137">輸入您的電子郵件地址中 hello**系統管理員電子郵件**欄位。</span><span class="sxs-lookup"><span data-stu-id="66a04-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="66a04-138">此電子郵件地址用於從 hello API 管理系統的通知。</span><span class="sxs-lookup"><span data-stu-id="66a04-138">This email address is used for notifications from hello API Management system.</span></span>

![建立服務 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="66a04-140">按一下 [hello] 核取方塊 toocreate 您服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="66a04-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="66a04-141">*因此會佔用 toothirty 分鐘的時間，建立新服務 toobe*。</span><span class="sxs-lookup"><span data-stu-id="66a04-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="66a04-142">建立 hello API</span><span class="sxs-lookup"><span data-stu-id="66a04-142">Create hello API</span></span>
<span data-ttu-id="66a04-143">一旦建立 hello 服務執行個體，hello 下一個步驟是 toocreate hello API。</span><span class="sxs-lookup"><span data-stu-id="66a04-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="66a04-144">API 包含可自用戶端應用程式叫用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="66a04-145">應用程式開發介面作業會代理 tooexisting web 服務。</span><span class="sxs-lookup"><span data-stu-id="66a04-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="66a04-146">本指南會建立現有 AzureML RR 和 BES web 服務的 proxy toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="66a04-147">應用程式開發介面建立和設定從 hello API 發行者入口網站，可從 hello Azure 傳統入口網站存取。</span><span class="sxs-lookup"><span data-stu-id="66a04-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="66a04-148">tooreach hello 發行者入口網站中，選取您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="66a04-148">tooreach hello publisher portal, select your service instance.</span></span>

![選取服務執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="66a04-150">按一下**管理**API 管理服務的 hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="66a04-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![管理服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="66a04-152">按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**新增應用程式開發介面**。</span><span class="sxs-lookup"><span data-stu-id="66a04-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![API 管理功能表](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="66a04-154">型別**AzureML 示範 API**為 hello **Web API 名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="66a04-155">型別**https://ussouthcentral.services.azureml.net**為 hello **Web 服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="66a04-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="66a04-156">型別**azureml 示範**為 hello **Web API URL 尾碼**。</span><span class="sxs-lookup"><span data-stu-id="66a04-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="66a04-157">請檢查**HTTPS**為 hello **Web API URL**配置。</span><span class="sxs-lookup"><span data-stu-id="66a04-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="66a04-158">在 [產品] 中，選取 [Starter]。</span><span class="sxs-lookup"><span data-stu-id="66a04-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="66a04-159">完成後，請按一下**儲存**toocreate hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-159">When finished, click **Save** toocreate hello API.</span></span>

![加入新的 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="66a04-161">新增 hello 作業</span><span class="sxs-lookup"><span data-stu-id="66a04-161">Add hello operations</span></span>
<span data-ttu-id="66a04-162">按一下**加入作業**tooadd 作業 toothis 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-162">Click **Add operation** tooadd operations toothis API.</span></span>

![加入作業](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="66a04-164">hello**新作業**視窗會顯示與 hello**簽章**預設會選取索引標籤。</span><span class="sxs-lookup"><span data-stu-id="66a04-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="66a04-165">加入 RRS 作業</span><span class="sxs-lookup"><span data-stu-id="66a04-165">Add RRS Operation</span></span>
<span data-ttu-id="66a04-166">先建立 hello AzureML RR 服務的作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="66a04-167">選取**POST**為 hello **HTTP 指令動詞**。</span><span class="sxs-lookup"><span data-stu-id="66a04-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="66a04-168">型別**/workspaces/ {工作區} /services/ {服務} / 執行？ api 版本 = {microsoft.authorization} （& s) 詳細資料 = {詳細資料}**為 hello **URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="66a04-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="66a04-169">型別**RR 執行**為 hello**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-169">Type **RRS Execute** as hello **Display name**.</span></span>

![加入 RRS 作業簽章](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="66a04-171">按一下**回應** > **新增**上 hello，然後選取**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="66a04-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="66a04-172">按一下**儲存**toosave 這項作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-172">Click **Save** toosave this operation.</span></span>

![加入 RRS 作業回應](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="66a04-174">加入 BES 作業</span><span class="sxs-lookup"><span data-stu-id="66a04-174">Add BES Operations</span></span>
<span data-ttu-id="66a04-175">螢幕擷取畫面的不包括 hello BES 作業，因為它們是非常類似 toothose 新增 hello RR 作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="66a04-176">提交 (但不啟動) 批次執行工作</span><span class="sxs-lookup"><span data-stu-id="66a04-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="66a04-177">按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="66a04-178">選取**POST** hello **HTTP 指令動詞**。</span><span class="sxs-lookup"><span data-stu-id="66a04-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="66a04-179">型別**/workspaces/ {工作區} /services/ {服務} / 作業？ api 版本 = {microsoft.authorization}** hello **URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="66a04-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="66a04-180">型別**BES 提交**hello**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="66a04-181">按一下**回應** > **新增**上 hello，然後選取**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="66a04-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="66a04-182">按一下**儲存**toosave 這項作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="66a04-183">啟動批次執行工作</span><span class="sxs-lookup"><span data-stu-id="66a04-183">Start a Batch Execution job</span></span>
<span data-ttu-id="66a04-184">按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="66a04-185">選取**POST** hello **HTTP 指令動詞**。</span><span class="sxs-lookup"><span data-stu-id="66a04-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="66a04-186">型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}] / [開始嗎？ 如果 api 版本 = {microsoft.authorization}** hello **URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="66a04-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="66a04-187">型別**BES 啟動**hello**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="66a04-188">按一下**回應** > **新增**上 hello，然後選取**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="66a04-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="66a04-189">按一下**儲存**toosave 這項作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="66a04-190">收到 hello 狀態或批次執行作業的結果</span><span class="sxs-lookup"><span data-stu-id="66a04-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="66a04-191">按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="66a04-192">選取**取得**hello **HTTP 指令動詞**。</span><span class="sxs-lookup"><span data-stu-id="66a04-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="66a04-193">型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}？ api 版本 = {microsoft.authorization}** hello **URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="66a04-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="66a04-194">型別**BES 狀態**hello**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="66a04-195">按一下**回應** > **新增**上 hello，然後選取**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="66a04-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="66a04-196">按一下**儲存**toosave 這項作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="66a04-197">刪除批次執行工作</span><span class="sxs-lookup"><span data-stu-id="66a04-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="66a04-198">按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="66a04-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="66a04-199">選取**刪除**hello **HTTP 指令動詞**。</span><span class="sxs-lookup"><span data-stu-id="66a04-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="66a04-200">型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}？ api 版本 = {microsoft.authorization}** hello **URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="66a04-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="66a04-201">型別**BES 刪除**hello**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="66a04-202">按一下**回應** > **新增**上 hello，然後選取**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="66a04-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="66a04-203">按一下**儲存**toosave 這項作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="66a04-204">從 hello 開發人員入口網站呼叫作業</span><span class="sxs-lookup"><span data-stu-id="66a04-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="66a04-205">作業可以直接從 hello 開發人員入口網站，可提供便利的方式 tooview 呼叫，並測試應用程式開發介面的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="66a04-206">在此快速入門步驟中您會呼叫 hello **RR 執行**方法已加入 toohello **AzureML 示範 API**。</span><span class="sxs-lookup"><span data-stu-id="66a04-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="66a04-207">按一下**開發人員入口網站**功能表在 hello hello hello 傳統入口網站的右上方。</span><span class="sxs-lookup"><span data-stu-id="66a04-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![開發人員入口網站](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="66a04-209">按一下**Api**從 hello 最上層功能表，然後再按一下**AzureML 示範 API** toosee hello 可用的作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml API](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="66a04-211">選取**RR 執行**hello 作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="66a04-212">按一下 [試試看] 。</span><span class="sxs-lookup"><span data-stu-id="66a04-212">Click **Try It**.</span></span>

![試試看](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="66a04-214">要求參數，輸入您**工作區**，**服務**， **2.0** hello **microsoft.authorization**，和**true**hello**詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="66a04-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="66a04-215">您可以找到您**工作區**和**服務**hello AzureML web 服務儀表板中 (請參閱**測試 hello web 服務**附錄 A 中)。</span><span class="sxs-lookup"><span data-stu-id="66a04-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="66a04-216">在 [要求標頭] 中，按一下 [新增標頭] 並輸入 **Content-Type** 和 **application/json**，然後按一下 [新增標頭] 並輸入 **Authorization** 和 **Bearer <YOUR AZUREML SERVICE API-KEY>**。</span><span class="sxs-lookup"><span data-stu-id="66a04-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="66a04-217">您可以找到您**api 金鑰**hello AzureML web 服務儀表板中 (請參閱**測試 hello web 服務**附錄 A 中)。</span><span class="sxs-lookup"><span data-stu-id="66a04-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="66a04-218">型別**{[輸入] 5d: {"input1": {"ColumnNames": ["Col2"]"值 」: [["This is 你好"]]}}，"GlobalParameters": {}}** hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="66a04-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![AzureML 示範 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="66a04-220">按一下 [傳送] 。</span><span class="sxs-lookup"><span data-stu-id="66a04-220">Click **Send**.</span></span>

![傳送](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="66a04-222">叫用作業之後，hello 開發人員入口網站會顯示 hello**要求 URL** hello 後端服務，從 hello**回應狀態**，hello**回應標頭**，和任何**回應內容**。</span><span class="sxs-lookup"><span data-stu-id="66a04-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![回應狀態](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="66a04-224">附錄 A - 建立及測試簡單的 AzureML Web 服務</span><span class="sxs-lookup"><span data-stu-id="66a04-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="66a04-225">建立 hello 實驗</span><span class="sxs-lookup"><span data-stu-id="66a04-225">Creating hello experiment</span></span>
<span data-ttu-id="66a04-226">以下是建立簡單的 AzureML 實驗，並將它部署為 web 服務的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="66a04-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="66a04-227">web 服務會接受 hello 做為輸入任意文字資料行，並傳回一組以整數表示的功能。</span><span class="sxs-lookup"><span data-stu-id="66a04-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="66a04-228">例如：</span><span class="sxs-lookup"><span data-stu-id="66a04-228">For example:</span></span>

| <span data-ttu-id="66a04-229">文字</span><span class="sxs-lookup"><span data-stu-id="66a04-229">Text</span></span> | <span data-ttu-id="66a04-230">雜湊的文字</span><span class="sxs-lookup"><span data-stu-id="66a04-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="66a04-231">這是美好的一天</span><span class="sxs-lookup"><span data-stu-id="66a04-231">This is a good day</span></span> |<span data-ttu-id="66a04-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="66a04-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="66a04-233">首先，使用您選擇的瀏覽器瀏覽至： [https://studio.azureml.net/](https://studio.azureml.net/)並輸入您的認證 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="66a04-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="66a04-234">接下來，建立新的空白實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-234">Next, create a new blank experiment.</span></span>

![搜尋實驗範本](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="66a04-236">將它重新命名過**SimpleFeatureHashingExperiment**。</span><span class="sxs-lookup"><span data-stu-id="66a04-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="66a04-237">展開 [儲存的資料集]，將 [來自 Amazon 的書籍評論] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![簡單的特徵雜湊實驗](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="66a04-239">展開 [資料轉換] 和 [操作]，將 [選取資料集中的資料行] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="66a04-240">連接**書籍檢閱從 Amazon**太**資料集中選取的資料行**。</span><span class="sxs-lookup"><span data-stu-id="66a04-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="66a04-242">按一下 選取資料集中的資料行，然後按一下啟動資料行選取器 並選取 Col2。</span><span class="sxs-lookup"><span data-stu-id="66a04-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="66a04-243">按一下 hello 核取記號 tooapply 這些變更。</span><span class="sxs-lookup"><span data-stu-id="66a04-243">Click hello checkmark tooapply these changes.</span></span>

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="66a04-245">展開**文字分析**拖曳**特徵雜湊**到 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="66a04-246">連接**資料集中選取的資料行**太**特徵雜湊**。</span><span class="sxs-lookup"><span data-stu-id="66a04-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![連接專案資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="66a04-248">型別**3** hello**雜湊位元大小**。</span><span class="sxs-lookup"><span data-stu-id="66a04-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="66a04-249">這會建立 8 (23) 個資料行。</span><span class="sxs-lookup"><span data-stu-id="66a04-249">This will create 8 (23) columns.</span></span>

![雜湊位元大小](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="66a04-251">此時，您可能會想 tooclick**執行**tootest hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![執行](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="66a04-253">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="66a04-253">Create a web service</span></span>
<span data-ttu-id="66a04-254">現在建立 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="66a04-254">Now create a web service.</span></span> <span data-ttu-id="66a04-255">展開 [Web 服務]，將 [輸入] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="66a04-256">連接**輸入**太**特徵雜湊**。</span><span class="sxs-lookup"><span data-stu-id="66a04-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="66a04-257">另將 [輸出]  拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="66a04-258">連接**輸出**太**特徵雜湊**。</span><span class="sxs-lookup"><span data-stu-id="66a04-258">Connect **Output** too**Feature Hashing**.</span></span>

![輸出至特徵雜湊](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="66a04-260">按一下 [發佈 Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="66a04-260">Click **Publish web service**.</span></span>

![發佈 Web 服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="66a04-262">按一下**是**toopublish hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-262">Click **Yes** toopublish hello experiment.</span></span>

![[是] 表示發佈](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="66a04-264">測試 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="66a04-264">Test hello web service</span></span>
<span data-ttu-id="66a04-265">AzureML Web 服務是由 RSS (要求/回應服務) 和 BES (批次執行服務) 端點所組成。</span><span class="sxs-lookup"><span data-stu-id="66a04-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="66a04-266">RSS 適用於同步執行。</span><span class="sxs-lookup"><span data-stu-id="66a04-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="66a04-267">BES 適用於非同步工作執行。</span><span class="sxs-lookup"><span data-stu-id="66a04-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="66a04-268">您的 web 服務與 hello 以下的範例 Python 來源 tootest，您可能需要 toodownload 和安裝 hello Azure SDK for Python (請參閱：[如何 tooinstall Python](../python-how-to-install.md))。</span><span class="sxs-lookup"><span data-stu-id="66a04-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="66a04-269">您也需要 hello**工作區**，**服務**，和**api_key**的 hello 範例來源的下列實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="66a04-270">您可以按一下找到 hello 工作區和服務**要求/回應**或**批次執行**hello web 服務儀表板在您實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![尋找工作區和服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="66a04-272">您可以找到 hello **api_key**按一下實驗 hello web 服務儀表板中的。</span><span class="sxs-lookup"><span data-stu-id="66a04-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![尋找 API 金鑰](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="66a04-274">測試 RRS 端點</span><span class="sxs-lookup"><span data-stu-id="66a04-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="66a04-275">測試按鈕</span><span class="sxs-lookup"><span data-stu-id="66a04-275">Test button</span></span>
<span data-ttu-id="66a04-276">輕鬆 tootest hello RR 端點是 tooclick**測試**hello web 服務儀表板上。</span><span class="sxs-lookup"><span data-stu-id="66a04-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="66a04-278">在 [col2] 中，輸入**這是美好的一天**。</span><span class="sxs-lookup"><span data-stu-id="66a04-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="66a04-279">按一下 hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="66a04-279">Click hello checkmark.</span></span>

![輸入資料](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="66a04-281">您會看到類似下列畫面：</span><span class="sxs-lookup"><span data-stu-id="66a04-281">You will see something like</span></span>

![範例輸出](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="66a04-283">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="66a04-283">Sample Code</span></span>
<span data-ttu-id="66a04-284">另一個方式 tootest RR 您是從用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="66a04-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="66a04-285">如果您按一下**要求/回應**在 hello 儀表板和捲動 toohello 底部，您會看到範例程式碼的 C#、 Python 和。您也會看到 hello 語法的 hello RR 要求，包括 hello 要求 URI、 標頭和主體。</span><span class="sxs-lookup"><span data-stu-id="66a04-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="66a04-286">本指南顯示一個運作正常的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="66a04-286">This guide shows a working Python example.</span></span> <span data-ttu-id="66a04-287">您將需要 toomodify 它以 hello**工作區**，**服務**，和**api_key**的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="66a04-288">測試 BES 端點</span><span class="sxs-lookup"><span data-stu-id="66a04-288">Test BES endpoint</span></span>
<span data-ttu-id="66a04-289">按一下**批次執行**hello 儀表板和捲動 toohello 下方。</span><span class="sxs-lookup"><span data-stu-id="66a04-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="66a04-290">您會看到的範例程式碼的 C#、 Python 和。您也會看到 hello 語法的 hello BES 要求 toosubmit 作業、 啟動工作、 取得 hello 狀態或作業的結果和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="66a04-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="66a04-291">本指南顯示一個運作正常的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="66a04-291">This guide shows a working Python example.</span></span> <span data-ttu-id="66a04-292">您需要 toomodify 它以 hello**工作區**，**服務**，和**api_key**的實驗。</span><span class="sxs-lookup"><span data-stu-id="66a04-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="66a04-293">此外，您需要 toomodify hello**儲存體帳戶名稱**，**儲存體帳戶金鑰**，和**儲存體容器名稱**。</span><span class="sxs-lookup"><span data-stu-id="66a04-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="66a04-294">最後，您將需要 hello toomodify hello 位置**輸入的檔**和 hello hello 位置**輸出檔**。</span><span class="sxs-lookup"><span data-stu-id="66a04-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
