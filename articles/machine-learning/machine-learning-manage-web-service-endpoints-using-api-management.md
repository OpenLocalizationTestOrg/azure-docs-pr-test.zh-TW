---
title: "了解如何使用 API 管理來管理 AzureML Web 服務 | Microsoft Docs"
description: "示範如何使用 API 管理來管理 AzureML Web 服務的指南"
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="f5055-104">了解如何使用 API 管理來管理 AzureML Web 服務</span><span class="sxs-lookup"><span data-stu-id="f5055-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f5055-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f5055-105">Overview</span></span>
<span data-ttu-id="f5055-106">本指南示範如何快速開始使用 API 管理，來管理您的 AzureML Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f5055-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="f5055-107">什麼是 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="f5055-107">What is Azure API Management?</span></span>
<span data-ttu-id="f5055-108">Azure API 管理是一項 Azure 服務，可讓您藉由定義使用者存取、使用節流設定和儀表板監視，來管理 REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="f5055-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="f5055-109">如需 Azure API 管理的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/api-management/) 。</span><span class="sxs-lookup"><span data-stu-id="f5055-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="f5055-110">如需如何開始使用 Azure API 管理的指南，請按一下 [這裡](../api-management/api-management-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="f5055-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="f5055-111">這是本指南所依據的另一份指南，涵蓋更多主題，包括通知組態、定價層、回應處理、使用者驗證、建立產品、開發人員訂用帳戶和使用量儀表板。</span><span class="sxs-lookup"><span data-stu-id="f5055-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="f5055-112">什麼是 AzureML？</span><span class="sxs-lookup"><span data-stu-id="f5055-112">What is AzureML?</span></span>
<span data-ttu-id="f5055-113">AzureML 是 Azure Machine Learning 服務，可讓您輕鬆建置、部署及共用進階分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="f5055-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="f5055-114">如需 AzureML 的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/machine-learning/) 。</span><span class="sxs-lookup"><span data-stu-id="f5055-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5055-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="f5055-115">Prerequisites</span></span>
<span data-ttu-id="f5055-116">若要完成本指南，您需要：</span><span class="sxs-lookup"><span data-stu-id="f5055-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="f5055-117">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5055-117">An Azure account.</span></span> <span data-ttu-id="f5055-118">如果您沒有 Azure 帳戶，請按一下 [這裡](https://azure.microsoft.com/pricing/free-trial/) 以取得如何建立免費試用帳戶的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f5055-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="f5055-119">AzureML 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5055-119">An AzureML account.</span></span> <span data-ttu-id="f5055-120">如果您沒有 AzureML 帳戶，請按一下 [這裡](https://studio.azureml.net/) 以取得如何建立免費試用帳戶的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f5055-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="f5055-121">部署為 Web 服務之 AzureML 實驗的工作區、服務和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f5055-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="f5055-122">如需如何建立 AzureML 實驗的詳細資訊，請按一下 [這裡](machine-learning-create-experiment.md) 。</span><span class="sxs-lookup"><span data-stu-id="f5055-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="f5055-123">如需如何將 AzureML 實驗部署為 Web 服務的詳細資訊，請按一下 [這裡](machine-learning-publish-a-machine-learning-web-service.md) 。</span><span class="sxs-lookup"><span data-stu-id="f5055-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="f5055-124">此外，附錄 A 中的指示說明如何建立及測試簡單的 AzureML 實驗，並將其部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f5055-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="f5055-125">建立 API 管理執行個體</span><span class="sxs-lookup"><span data-stu-id="f5055-125">Create an API Management instance</span></span>
<span data-ttu-id="f5055-126">以下是使用 API 管理來管理您的 AzureML Web 服務的步驟。</span><span class="sxs-lookup"><span data-stu-id="f5055-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="f5055-127">首先建立服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f5055-127">First create a service instance.</span></span> <span data-ttu-id="f5055-128">登入[傳統入口網站](https://manage.windowsazure.com/)，然後按一下 [新增] > [應用程式服務] > [API 管理] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="f5055-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![建立執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="f5055-130">指定唯一的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="f5055-130">Specify a unique **URL**.</span></span> <span data-ttu-id="f5055-131">本指南使用 **demoazureml** ，您必須選擇其他不同的值。</span><span class="sxs-lookup"><span data-stu-id="f5055-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="f5055-132">針對您的服務執行個體，選擇需要的 [訂用帳戶] 和 [區域]。</span><span class="sxs-lookup"><span data-stu-id="f5055-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="f5055-133">進行您的選擇之後，請按下一步按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5055-133">After making your selections, click the next button.</span></span>

![建立服務 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="f5055-135">指定 [組織名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="f5055-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="f5055-136">本指南使用 **demoazureml** ，您必須選擇其他不同的值。</span><span class="sxs-lookup"><span data-stu-id="f5055-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="f5055-137">在 [系統管理員電子郵件] 欄位中，輸入您的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="f5055-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="f5055-138">此電子郵件地址將用於自 API 管理系統傳送通知。</span><span class="sxs-lookup"><span data-stu-id="f5055-138">This email address is used for notifications from the API Management system.</span></span>

![建立服務 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="f5055-140">按一下核取方塊來建立您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f5055-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="f5055-141">*建立新服務最多需要 30 分鐘的時間*。</span><span class="sxs-lookup"><span data-stu-id="f5055-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="f5055-142">建立 API</span><span class="sxs-lookup"><span data-stu-id="f5055-142">Create the API</span></span>
<span data-ttu-id="f5055-143">建立服務執行個體之後，下一個步驟是建立 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="f5055-144">API 包含可自用戶端應用程式叫用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="f5055-145">API 作業會代理到現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f5055-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="f5055-146">本指南會建立代理現有 AzureML RRS 和 BES Web 服務的 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="f5055-147">API 是透過您經由 Azure 傳統入口網站存取的 API 發行者入口網站來建立和設定。</span><span class="sxs-lookup"><span data-stu-id="f5055-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="f5055-148">若要連線到發行者入口網站，請選取您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f5055-148">To reach the publisher portal, select your service instance.</span></span>

![選取服務執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="f5055-150">在 Azure 傳統入口網站中，按一下您的 API 管理服務中的 [管理]  。</span><span class="sxs-lookup"><span data-stu-id="f5055-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![管理服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="f5055-152">從左側 [API 管理] 功能表按一下 [API]，然後按一下 [新增 API]。</span><span class="sxs-lookup"><span data-stu-id="f5055-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![API 管理功能表](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="f5055-154">在 [Web API 名稱] 中，輸入 **AzureML 示範 API**。</span><span class="sxs-lookup"><span data-stu-id="f5055-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="f5055-155">在 [Web 服務 URL] 中，輸入 **https://ussouthcentral.services.azureml.net**。</span><span class="sxs-lookup"><span data-stu-id="f5055-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="f5055-156">在 [Web API URL 尾碼] 中，輸入 **azureml-demo**。</span><span class="sxs-lookup"><span data-stu-id="f5055-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="f5055-157">在 [Web API URL 配置] 中，核取 [HTTPS]。</span><span class="sxs-lookup"><span data-stu-id="f5055-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="f5055-158">在 [產品] 中，選取 [Starter]。</span><span class="sxs-lookup"><span data-stu-id="f5055-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="f5055-159">完成後，按一下 [儲存] 以建立 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-159">When finished, click **Save** to create the API.</span></span>

![加入新的 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="f5055-161">加入作業</span><span class="sxs-lookup"><span data-stu-id="f5055-161">Add the operations</span></span>
<span data-ttu-id="f5055-162">按一下 [加入作業]  ，將作業加入這個 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-162">Click **Add operation** to add operations to this API.</span></span>

![加入作業](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="f5055-164">將顯示 [新增作業] 視窗，並且預設會選取 [簽章] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f5055-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="f5055-165">加入 RRS 作業</span><span class="sxs-lookup"><span data-stu-id="f5055-165">Add RRS Operation</span></span>
<span data-ttu-id="f5055-166">首先建立 AzureML RRS 服務的作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="f5055-167">在 [HTTP 指令動詞] 中，選取 [POST]。</span><span class="sxs-lookup"><span data-stu-id="f5055-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="f5055-168">在 [URL 範本] 中，輸入 **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="f5055-169">在 [顯示名稱] 中，輸入 **RRS 執行**。</span><span class="sxs-lookup"><span data-stu-id="f5055-169">Type **RRS Execute** as the **Display name**.</span></span>

![加入 RRS 作業簽章](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="f5055-171">按一下左側的 [回應] > [新增]，然後選取 [200 確定]。</span><span class="sxs-lookup"><span data-stu-id="f5055-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f5055-172">按一下 [儲存]  儲存這個作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-172">Click **Save** to save this operation.</span></span>

![加入 RRS 作業回應](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="f5055-174">加入 BES 作業</span><span class="sxs-lookup"><span data-stu-id="f5055-174">Add BES Operations</span></span>
<span data-ttu-id="f5055-175">由於加入 BES 作業的螢幕擷取畫面與加入 RRS 作業的螢幕擷取畫面很類似，因此不再提供。</span><span class="sxs-lookup"><span data-stu-id="f5055-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="f5055-176">提交 (但不啟動) 批次執行工作</span><span class="sxs-lookup"><span data-stu-id="f5055-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="f5055-177">按一下 [新增作業]，將 AzureML BES 作業新增至 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f5055-178">在 [HTTP 指令動詞] 中，選取 [POST]。</span><span class="sxs-lookup"><span data-stu-id="f5055-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="f5055-179">在 [URL 範本] 中，輸入 **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f5055-180">在 [顯示名稱] 中，輸入 **BES 提交**。</span><span class="sxs-lookup"><span data-stu-id="f5055-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="f5055-181">按一下左側的 [回應] > [新增]，然後選取 [200 確定]。</span><span class="sxs-lookup"><span data-stu-id="f5055-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f5055-182">按一下 [儲存]  儲存這個作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="f5055-183">啟動批次執行工作</span><span class="sxs-lookup"><span data-stu-id="f5055-183">Start a Batch Execution job</span></span>
<span data-ttu-id="f5055-184">按一下 [新增作業]，將 AzureML BES 作業新增至 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f5055-185">在 [HTTP 指令動詞] 中，選取 [POST]。</span><span class="sxs-lookup"><span data-stu-id="f5055-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="f5055-186">在 [URL 範本] 中，輸入 **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f5055-187">在 [顯示名稱] 中，輸入 **BES 啟動**。</span><span class="sxs-lookup"><span data-stu-id="f5055-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="f5055-188">按一下左側的 [回應] > [新增]，然後選取 [200 確定]。</span><span class="sxs-lookup"><span data-stu-id="f5055-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f5055-189">按一下 [儲存]  儲存這個作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="f5055-190">取得批次執行工作的狀態或結果</span><span class="sxs-lookup"><span data-stu-id="f5055-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="f5055-191">按一下 [新增作業]，將 AzureML BES 作業新增至 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f5055-192">在 [HTTP 指令動詞] 中，選取 [GET]。</span><span class="sxs-lookup"><span data-stu-id="f5055-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="f5055-193">在 [URL 範本] 中，輸入 **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f5055-194">在 [顯示名稱] 中，輸入 **BES 狀態**。</span><span class="sxs-lookup"><span data-stu-id="f5055-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="f5055-195">按一下左側的 [回應] > [新增]，然後選取 [200 確定]。</span><span class="sxs-lookup"><span data-stu-id="f5055-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f5055-196">按一下 [儲存]  儲存這個作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="f5055-197">刪除批次執行工作</span><span class="sxs-lookup"><span data-stu-id="f5055-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="f5055-198">按一下 [新增作業]，將 AzureML BES 作業新增至 API。</span><span class="sxs-lookup"><span data-stu-id="f5055-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f5055-199">在 [HTTP 指令動詞] 中，選取 [DELETE]。</span><span class="sxs-lookup"><span data-stu-id="f5055-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="f5055-200">在 [URL 範本] 中，輸入 **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f5055-201">在 [顯示名稱] 中，輸入 **BES 刪除**。</span><span class="sxs-lookup"><span data-stu-id="f5055-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="f5055-202">按一下左側的 [回應] > [新增]，然後選取 [200 確定]。</span><span class="sxs-lookup"><span data-stu-id="f5055-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f5055-203">按一下 [儲存]  儲存這個作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="f5055-204">透過開發人員入口網站呼叫作業</span><span class="sxs-lookup"><span data-stu-id="f5055-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="f5055-205">您可以從開發人員入口網站直接呼叫作業，以便檢視和測試 API 的操作。</span><span class="sxs-lookup"><span data-stu-id="f5055-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="f5055-206">在這個指南步驟中，您會呼叫新增至 [AzureML 示範 API] 的 [RRS 執行] 方法。</span><span class="sxs-lookup"><span data-stu-id="f5055-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="f5055-207">從傳統入口網站右上角的功能表中，按一下 [開發人員入口網站]  。</span><span class="sxs-lookup"><span data-stu-id="f5055-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![開發人員入口網站](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="f5055-209">按一下上層功能表中的 [API]，然後按一下 [AzureML 示範 API] 以查看可用的作業。</span><span class="sxs-lookup"><span data-stu-id="f5055-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml API](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="f5055-211">為作業選取 [RRS 執行]  。</span><span class="sxs-lookup"><span data-stu-id="f5055-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="f5055-212">按一下 [試試看] 。</span><span class="sxs-lookup"><span data-stu-id="f5055-212">Click **Try It**.</span></span>

![試試看](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="f5055-214">在 [要求參數] 中，輸入您的**工作區**和**服務**，在 [API 版本] 中輸入 **2.0**，並在 [詳細資料] 中輸入 **true**。</span><span class="sxs-lookup"><span data-stu-id="f5055-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="f5055-215">您可以在 AzureML Web 服務儀表板中找到您的**工作區**和**服務** (請參閱附錄 A 中的**測試 Web 服務**)。</span><span class="sxs-lookup"><span data-stu-id="f5055-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="f5055-216">在 [要求標頭] 中，按一下 [新增標頭] 並輸入 **Content-Type** 和 **application/json**，然後按一下 [新增標頭] 並輸入 **Authorization** 和 **Bearer <YOUR AZUREML SERVICE API-KEY>**。</span><span class="sxs-lookup"><span data-stu-id="f5055-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="f5055-217">您可以在 AzureML Web 服務儀表板中找到您的 **API 金鑰** (請參閱附錄 A 中的**測試 Web 服務**)。</span><span class="sxs-lookup"><span data-stu-id="f5055-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="f5055-218">在 [要求本文] 中，輸入 **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}**。</span><span class="sxs-lookup"><span data-stu-id="f5055-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![AzureML 示範 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="f5055-220">按一下 [傳送] 。</span><span class="sxs-lookup"><span data-stu-id="f5055-220">Click **Send**.</span></span>

![傳送](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="f5055-222">叫用作業之後，開發人員入口網站會顯示來自後端服務 [要求的 URL]、[回應狀態]、[回應標頭]，以及任何的 [回應內容]。</span><span class="sxs-lookup"><span data-stu-id="f5055-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![回應狀態](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="f5055-224">附錄 A - 建立及測試簡單的 AzureML Web 服務</span><span class="sxs-lookup"><span data-stu-id="f5055-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="f5055-225">建立實驗</span><span class="sxs-lookup"><span data-stu-id="f5055-225">Creating the experiment</span></span>
<span data-ttu-id="f5055-226">以下步驟可讓您建立簡單的 AzureML 實驗並將其部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f5055-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="f5055-227">Web 服務接受任意文字的資料行做為輸入，並傳回一組以整數來表示的特徵。</span><span class="sxs-lookup"><span data-stu-id="f5055-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="f5055-228">例如：</span><span class="sxs-lookup"><span data-stu-id="f5055-228">For example:</span></span>

| <span data-ttu-id="f5055-229">文字</span><span class="sxs-lookup"><span data-stu-id="f5055-229">Text</span></span> | <span data-ttu-id="f5055-230">雜湊的文字</span><span class="sxs-lookup"><span data-stu-id="f5055-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="f5055-231">這是美好的一天</span><span class="sxs-lookup"><span data-stu-id="f5055-231">This is a good day</span></span> |<span data-ttu-id="f5055-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="f5055-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="f5055-233">首先，使用您選擇的瀏覽器巡覽至 [https://studio.azureml.net/](https://studio.azureml.net/) ，並輸入您的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="f5055-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="f5055-234">接下來，建立新的空白實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-234">Next, create a new blank experiment.</span></span>

![搜尋實驗範本](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="f5055-236">重新命名為 **SimpleFeatureHashingExperiment**。</span><span class="sxs-lookup"><span data-stu-id="f5055-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="f5055-237">展開 [儲存的資料集]，將 [來自 Amazon 的書籍評論] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![簡單的特徵雜湊實驗](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="f5055-239">展開 [資料轉換] 和 [操作]，將 [選取資料集中的資料行] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="f5055-240">將 [來自 Amazon 的書籍評論] 連接到 [選取資料集中的資料行]。</span><span class="sxs-lookup"><span data-stu-id="f5055-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="f5055-242">按一下 [選取資料集中的資料行]，然後按一下 [啟動資料行選取器] 並選取 [Col2]。</span><span class="sxs-lookup"><span data-stu-id="f5055-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="f5055-243">按一下核取記號以套用這些變更。</span><span class="sxs-lookup"><span data-stu-id="f5055-243">Click the checkmark to apply these changes.</span></span>

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="f5055-245">展開 [文字分析]，將 [特徵雜湊] 拖曳到實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="f5055-246">將 [選取資料集中的資料行] 連接到 [特徵雜湊]。</span><span class="sxs-lookup"><span data-stu-id="f5055-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![連接專案資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="f5055-248">在 [雜湊位元大小] 中，輸入 **3**。</span><span class="sxs-lookup"><span data-stu-id="f5055-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="f5055-249">這會建立 8 (23) 個資料行。</span><span class="sxs-lookup"><span data-stu-id="f5055-249">This will create 8 (23) columns.</span></span>

![雜湊位元大小](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="f5055-251">此時，您可能想要按一下 [執行]  ，以測試實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![執行](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="f5055-253">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="f5055-253">Create a web service</span></span>
<span data-ttu-id="f5055-254">現在建立 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f5055-254">Now create a web service.</span></span> <span data-ttu-id="f5055-255">展開 [Web 服務]，將 [輸入] 拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="f5055-256">將 [輸入] 連接到 [特徵雜湊]。</span><span class="sxs-lookup"><span data-stu-id="f5055-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="f5055-257">另將 [輸出]  拖曳到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="f5055-258">將 [輸出] 連接到 [特徵雜湊]。</span><span class="sxs-lookup"><span data-stu-id="f5055-258">Connect **Output** to **Feature Hashing**.</span></span>

![輸出至特徵雜湊](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="f5055-260">按一下 [發佈 Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="f5055-260">Click **Publish web service**.</span></span>

![發佈 Web 服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="f5055-262">按一下 [是]  發佈實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-262">Click **Yes** to publish the experiment.</span></span>

![[是] 表示發佈](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="f5055-264">測試 Web 服務</span><span class="sxs-lookup"><span data-stu-id="f5055-264">Test the web service</span></span>
<span data-ttu-id="f5055-265">AzureML Web 服務是由 RSS (要求/回應服務) 和 BES (批次執行服務) 端點所組成。</span><span class="sxs-lookup"><span data-stu-id="f5055-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="f5055-266">RSS 適用於同步執行。</span><span class="sxs-lookup"><span data-stu-id="f5055-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="f5055-267">BES 適用於非同步工作執行。</span><span class="sxs-lookup"><span data-stu-id="f5055-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="f5055-268">若要使用下面的範例 Python 原始碼來測試您的 Web 服務，您可能需要下載並安裝 Azure SDK for Python (請參閱： [如何安裝 Python](../python-how-to-install.md))。</span><span class="sxs-lookup"><span data-stu-id="f5055-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="f5055-269">下面的範例原始碼也需要用到實驗的**工作區**、**服務**和 **API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="f5055-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="f5055-270">若要尋找工作區和服務，請在 Web 服務儀表板中，按一下實驗的 [要求/回應] 或 [批次執行]。</span><span class="sxs-lookup"><span data-stu-id="f5055-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![尋找工作區和服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="f5055-272">若要尋找 [API 金鑰]，請按一下 Web 服務儀表板中的實驗。</span><span class="sxs-lookup"><span data-stu-id="f5055-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![尋找 API 金鑰](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="f5055-274">測試 RRS 端點</span><span class="sxs-lookup"><span data-stu-id="f5055-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="f5055-275">測試按鈕</span><span class="sxs-lookup"><span data-stu-id="f5055-275">Test button</span></span>
<span data-ttu-id="f5055-276">測試 RRS 端點的一個簡單方式，是在 Web 服務儀表板上，按一下 [測試]  。</span><span class="sxs-lookup"><span data-stu-id="f5055-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="f5055-278">在 [col2] 中，輸入**這是美好的一天**。</span><span class="sxs-lookup"><span data-stu-id="f5055-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="f5055-279">按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="f5055-279">Click the checkmark.</span></span>

![輸入資料](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="f5055-281">您會看到類似下列畫面：</span><span class="sxs-lookup"><span data-stu-id="f5055-281">You will see something like</span></span>

![範例輸出](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="f5055-283">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="f5055-283">Sample Code</span></span>
<span data-ttu-id="f5055-284">測試 RRS 的另一個方式，是利用用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5055-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="f5055-285">如果您按一下儀表板上的 [要求/回應] 並捲動至底部，您會看到 C#、Python 和 R 的範例程式碼。您也會看到 RRS 要求的語法，包括要求 URI、標頭和本文。</span><span class="sxs-lookup"><span data-stu-id="f5055-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="f5055-286">本指南顯示一個運作正常的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="f5055-286">This guide shows a working Python example.</span></span> <span data-ttu-id="f5055-287">您必須使用實驗的**工作區**、**服務**和 **API 金鑰**加以修改。</span><span class="sxs-lookup"><span data-stu-id="f5055-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="f5055-288">測試 BES 端點</span><span class="sxs-lookup"><span data-stu-id="f5055-288">Test BES endpoint</span></span>
<span data-ttu-id="f5055-289">按一下儀表板上的 [批次執行] 並捲動至底部。</span><span class="sxs-lookup"><span data-stu-id="f5055-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="f5055-290">您會看到 C#、Python 和 R 的範例程式碼。您也會看到用來提交工作、啟動工作、取得工作狀態或結果，以及刪除工作的 BES 要求語法。</span><span class="sxs-lookup"><span data-stu-id="f5055-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="f5055-291">本指南顯示一個運作正常的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="f5055-291">This guide shows a working Python example.</span></span> <span data-ttu-id="f5055-292">您必須使用實驗的**工作區**、**服務**和 **API 金鑰**加以修改。</span><span class="sxs-lookup"><span data-stu-id="f5055-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="f5055-293">此外，您必須修改**儲存體帳戶名稱**、**儲存體帳戶金鑰**和**儲存體容器名稱**。</span><span class="sxs-lookup"><span data-stu-id="f5055-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="f5055-294">最後，您必須修改**輸入檔**的位置和**輸出檔**的位置。</span><span class="sxs-lookup"><span data-stu-id="f5055-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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
