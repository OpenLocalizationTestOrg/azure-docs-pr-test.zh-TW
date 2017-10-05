---
title: "在 Azure API 管理中使用備份和還原實作災害復原 | Microsoft Docs"
description: "了解如何在 Azure API 管理中使用備份和還原來執行災難復原。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="33049-103">如何在 Azure API 管理中使用服務備份和還原實作災害復原</span><span class="sxs-lookup"><span data-stu-id="33049-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="33049-104">選擇透過 Azure API 管理來發佈及管理 API，您將能夠利用許多非 Azure API 管理使用者須另行設計、實作及管理的容錯和基礎結構功能。</span><span class="sxs-lookup"><span data-stu-id="33049-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="33049-105">Azure 平台可緩和絕大部分可能的失敗後果，且成本低廉。</span><span class="sxs-lookup"><span data-stu-id="33049-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="33049-106">若要從影響範圍涵蓋 API 管理服務託管所在之區域的可用性問題復原，您應該要做好準備能隨時在其他區域重新建構服務。</span><span class="sxs-lookup"><span data-stu-id="33049-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="33049-107">由於可用性目標和復原時間目標不盡相同，您也許會想要在一或多個區域預留備份服務，並嘗試與作用中的服務維持組態和內容同步。</span><span class="sxs-lookup"><span data-stu-id="33049-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="33049-108">服務備份和還原功能可提供實作災害復原策略時所不可或缺的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="33049-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="33049-109">本指南說明如何驗證 Azure Resource Manager 的要求，以及如何備份和還原您的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="33049-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="33049-110">備份與還原嚴重損壞修復的 API 管理服務執行個體的程序，也可用於預備等案例，以複寫 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="33049-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="33049-111">請注意，每個備份在 30 天後到期。</span><span class="sxs-lookup"><span data-stu-id="33049-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="33049-112">如果您在過了 30 天的到期時間後嘗試還原備份，還原會失敗並傳回 `Cannot restore: backup expired` 訊息。</span><span class="sxs-lookup"><span data-stu-id="33049-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="33049-113">驗證 Azure 資源管理員要求</span><span class="sxs-lookup"><span data-stu-id="33049-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="33049-114">備份和還原的 REST API 會使用 Azure 資源管理員，並有不同的驗證機制的 REST API 來管理您的 API 管理實體。</span><span class="sxs-lookup"><span data-stu-id="33049-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="33049-115">本節中的步驟描述如何驗證 Azure 資源管理員的要求。</span><span class="sxs-lookup"><span data-stu-id="33049-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="33049-116">如需詳細資訊，請參閱 [驗證 Azure Resource Manager 要求](http://msdn.microsoft.com/library/azure/dn790557.aspx)。</span><span class="sxs-lookup"><span data-stu-id="33049-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="33049-117">所有您使用 Azure 資源管理員對資源所做的工作，必須透過 Azure Active Directory 使用以下步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="33049-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="33049-118">新增應用程式到 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="33049-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="33049-119">設定您所新增之應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="33049-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="33049-120">取得向 Azure 資源管理員驗證要求的權杖。</span><span class="sxs-lookup"><span data-stu-id="33049-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="33049-121">第一個步驟是建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33049-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="33049-122">使用含 API 管理服務執行個體的訂用帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com/)，並瀏覽至預設 Azure Active Directory 的 [應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="33049-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="33049-123">如果您的帳戶看不到 Azure Active Directory 預設目錄，請連絡 Azure 訂用帳戶的系統管理員，以授與您的帳戶必要權限。</span><span class="sxs-lookup"><span data-stu-id="33049-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![建立 Azure Active Directory 應用程式][api-management-add-aad-application]

<span data-ttu-id="33049-125">按一下 [新增]，[新增我的組織正在開發的應用程式]，然後選擇 [原生用戶端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="33049-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="33049-126">輸入描述性名稱，然後按一下下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="33049-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="33049-127">輸入 [重新導向 URI] 的預留位置 URL，例如 `http://resources`，因為它是必要的欄位，但稍後不會使用這個值。</span><span class="sxs-lookup"><span data-stu-id="33049-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="33049-128">按一下核取方塊以儲存應用程式。</span><span class="sxs-lookup"><span data-stu-id="33049-128">Click the check box to save the application.</span></span>

<span data-ttu-id="33049-129">儲存應用程式之後，按一下 [組態]，向下捲動至 [其他應用程式的權限] 區段，然後按一下 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="33049-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![新增權限][api-management-aad-permissions-add]

<span data-ttu-id="33049-131">選取 [Windows Azure 服務管理 API]，然後按一下核取方塊以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="33049-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![新增權限][api-management-aad-permissions]

<span data-ttu-id="33049-133">按一下新增的 [Windows Azure 服務管理 API] 應用程式旁邊的 [委派權限]，核取 [存取 Azure 服務管理 (預覽)]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="33049-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![新增權限][api-management-aad-delegated-permissions]

<span data-ttu-id="33049-135">在叫用產生備份並將其還原的 API 之前，必須先取得權杖。</span><span class="sxs-lookup"><span data-stu-id="33049-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="33049-136">以下範例會使用 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet 封裝來擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="33049-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="33049-137">使用下列指示取代 `{tentand id}`、`{application id}` 和 `{redirect uri}`。</span><span class="sxs-lookup"><span data-stu-id="33049-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="33049-138">使用剛才建立的 Azure Active Directory 應用程式的租用戶識別碼取代 `{tenant id}` 。</span><span class="sxs-lookup"><span data-stu-id="33049-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="33049-139">您可以按一下 [檢視端點] 來存取識別碼。</span><span class="sxs-lookup"><span data-stu-id="33049-139">You can access the id by clicking **View endpoints**.</span></span>

![端點][api-management-aad-default-directory]

![端點][api-management-endpoint]

<span data-ttu-id="33049-142">使用 Azure Active Directory 應用程式的 [設定] 索引標籤中的 [用戶端識別碼] 和 [重新導向 URI] 區段中的 URL，取代 `{application id}` 和 `{redirect uri}`。</span><span class="sxs-lookup"><span data-stu-id="33049-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![資源][api-management-aad-resources]

<span data-ttu-id="33049-144">一旦指定了值，程式碼範例將傳回類似以下範例的權杖。</span><span class="sxs-lookup"><span data-stu-id="33049-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![權杖][api-management-arm-token]

<span data-ttu-id="33049-146">呼叫下節描述的備份和還原作業之前，請先設定您 REST 呼叫的授權要求標頭。</span><span class="sxs-lookup"><span data-stu-id="33049-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="33049-147"><a name="step1"> </a>備份 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="33049-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="33049-148">若要備份 API 管理服務，請發出以下 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="33049-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="33049-149">其中：</span><span class="sxs-lookup"><span data-stu-id="33049-149">where:</span></span>

* <span data-ttu-id="33049-150">`subscriptionId` -  訂用帳戶的識別碼，此訂用帳戶含有您嘗試備份的 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="33049-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="33049-151">`resourceGroupName` - 'Api-Default-{service-region}' 形式的字串；其中，`service-region` 可識別在其中裝載您嘗試備份之 API 管理服務的 Azure 區域 (例如 `North-Central-US`)</span><span class="sxs-lookup"><span data-stu-id="33049-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="33049-152">`serviceName` - 要備份之 API 管理服務的名稱，該名稱是在服務建立時所指定</span><span class="sxs-lookup"><span data-stu-id="33049-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="33049-153">`api-version` - 取代為 `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="33049-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="33049-154">在要求的本文中指定目標 Azure 儲存體帳戶名稱、存取金鑰、Blob 容器名稱和備份名稱：</span><span class="sxs-lookup"><span data-stu-id="33049-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="33049-155">將 `Content-Type` 要求標頭的值設定為 `application/json`。</span><span class="sxs-lookup"><span data-stu-id="33049-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="33049-156">備份作業的執行時間較長，因此可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="33049-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="33049-157">如果要求成功並已起始備份程序，則會收到含有 `Location` 標頭的 `202 Accepted` 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="33049-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="33049-158">請向 `Location` 標頭中的 URL 發出 'GET' 要求，以查明作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="33049-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="33049-159">當備份進行時，您會持續收到「202 已接受」狀態碼。</span><span class="sxs-lookup"><span data-stu-id="33049-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="33049-160">回應碼 `200 OK` 代表備份作業已成功完成。</span><span class="sxs-lookup"><span data-stu-id="33049-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="33049-161">進行備份的要求時，請注意下列條件約束。</span><span class="sxs-lookup"><span data-stu-id="33049-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="33049-162">在要求本文中指定的**容器****必須存在**。</span><span class="sxs-lookup"><span data-stu-id="33049-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="33049-163">備份進行時，請「避免嘗試任何服務管理作業」  ，如提升或降低 SKU、變更網域名稱等。</span><span class="sxs-lookup"><span data-stu-id="33049-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="33049-164">備份還原的**保證僅限建立後的 30 天內**。</span><span class="sxs-lookup"><span data-stu-id="33049-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="33049-165">備份**不包含**用來建立分析報告的**使用量資料**。</span><span class="sxs-lookup"><span data-stu-id="33049-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="33049-166">請使用 [Azure API 管理 REST API][Azure API Management REST API] 來定期擷取分析報告，以利妥善保存。</span><span class="sxs-lookup"><span data-stu-id="33049-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="33049-167">執行服務備份的頻率會影響您的復原點目標。</span><span class="sxs-lookup"><span data-stu-id="33049-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="33049-168">為了盡可能縮小，建議您實施定期備份，以及在針對 API 管理服務做出重要變更後執行隨選備份。</span><span class="sxs-lookup"><span data-stu-id="33049-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="33049-169">在備份作業進行時針對服務組態 (如 API、原則、開發人員入口網站外觀) 所做的**變更****可能不會納入備份中，因此可能會遺失**。</span><span class="sxs-lookup"><span data-stu-id="33049-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="33049-170"><a name="step2"> </a>還原 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="33049-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="33049-171">若要從先前建立的備份還原 API 管理服務，請發出以下 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="33049-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="33049-172">其中：</span><span class="sxs-lookup"><span data-stu-id="33049-172">where:</span></span>

* <span data-ttu-id="33049-173">`subscriptionId` - 訂用帳戶的識別碼，此訂用帳戶含有您要還原備份的目標 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="33049-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="33049-174">`resourceGroupName` - 'Api-Default-{service-region}' 形式的字串；其中，`service-region` 可識別在其中裝載您要還原備份之目標 API 管理服務的 Azure 區域 (例如 `North-Central-US`)</span><span class="sxs-lookup"><span data-stu-id="33049-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="33049-175">`serviceName` - 要還原之目標 API 管理服務的名稱，該名稱是在服務建立時所指定</span><span class="sxs-lookup"><span data-stu-id="33049-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="33049-176">`api-version` - 取代為 `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="33049-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="33049-177">在要求的本文中指定備份檔案位置，即 Azure 儲存體帳戶名稱、存取金鑰、Blob 容器名稱和備份名稱：</span><span class="sxs-lookup"><span data-stu-id="33049-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="33049-178">將 `Content-Type` 要求標頭的值設定為 `application/json`。</span><span class="sxs-lookup"><span data-stu-id="33049-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="33049-179">還原作業的執行時間較長，因此可能需要 30 分鐘以上的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="33049-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="33049-180">如果要求成功並已起始還原程序，則會收到含有 `Location` 標頭的 `202 Accepted` 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="33049-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="33049-181">請向 `Location` 標頭中的 URL 發出 'GET' 要求，以查明作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="33049-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="33049-182">當還原進行時，您會持續收到「202 已接受」狀態碼。</span><span class="sxs-lookup"><span data-stu-id="33049-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="33049-183">回應碼 `200 OK` 代表還原作業已成功完成。</span><span class="sxs-lookup"><span data-stu-id="33049-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33049-184">用於還原之目標服務的 **SKU****必須符合**即將還原之已備份服務的 SKU。</span><span class="sxs-lookup"><span data-stu-id="33049-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="33049-185">在還原作業進行時針對服務組態 (如 API、原則、開發人員入口網站外觀) 所做的**變更****可能會遭到覆寫**。</span><span class="sxs-lookup"><span data-stu-id="33049-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="33049-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33049-186">Next steps</span></span>
<span data-ttu-id="33049-187">請參閱下列 Microsoft 部落格中，兩個不同的備份/還原程序逐步解說。</span><span class="sxs-lookup"><span data-stu-id="33049-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="33049-188">複寫 Azure API 管理帳戶 (英文)</span><span class="sxs-lookup"><span data-stu-id="33049-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="33049-189">感謝 Gisela 提供此文章。</span><span class="sxs-lookup"><span data-stu-id="33049-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="33049-190">Azure API 管理：備份和還原組態 (英文)</span><span class="sxs-lookup"><span data-stu-id="33049-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="33049-191">Stuart 詳細說明的方法與正式指南不同，但非常有意思。</span><span class="sxs-lookup"><span data-stu-id="33049-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
