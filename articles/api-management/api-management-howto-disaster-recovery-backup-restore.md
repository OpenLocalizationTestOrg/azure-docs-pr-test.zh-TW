---
title: "aaaImplement 災害復原使用備份與還原在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 toouse 備份和還原 tooperform 嚴重損壞修復，在 Azure API 管理。"
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
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="18392-103">如何 tooimplement 災害復原使用服務備份和還原在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="18392-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="18392-104">藉由選擇 toopublish 和管理您的應用程式開發介面透過 Azure API 管理，您就可以運用許多錯誤容錯和基礎結構功能，您原本必須另外 toodesign 實作和管理。</span><span class="sxs-lookup"><span data-stu-id="18392-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="18392-105">hello Azure 平台可降低在 hello 成本可能發生失敗的較大的分數。</span><span class="sxs-lookup"><span data-stu-id="18392-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="18392-106">從可用性問題在影響其中是您的 API 管理服務的 hello 區域 toorecover 裝載您應該準備好 tooreconstitute 隨時都是您在不同的區域中的服務。</span><span class="sxs-lookup"><span data-stu-id="18392-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="18392-107">視您的可用性目標和復原時間目標，您可能會想 tooreserve 中一或多個區域的備份服務並再試一次 toomaintain 其設定及內容與 hello active service 不同步。</span><span class="sxs-lookup"><span data-stu-id="18392-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="18392-108">hello 服務備份和還原功能提供 hello 所需的建置組塊，實作嚴重損壞修復策略。</span><span class="sxs-lookup"><span data-stu-id="18392-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="18392-109">本指南也說明如何 tooauthenticate Azure 資源管理員要求，以及如何 toobackup 和還原您的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="18392-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="18392-110">備份與還原 API 管理服務執行個體的災害復原的 hello 程序也可用來複寫案例，例如臨時的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="18392-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="18392-111">請注意，每個備份在 30 天後到期。</span><span class="sxs-lookup"><span data-stu-id="18392-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="18392-112">如果您嘗試 toorestore 備份 hello 30 天的逾期期限過期之後，hello 還原會失敗並`Cannot restore: backup expired`訊息。</span><span class="sxs-lookup"><span data-stu-id="18392-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="18392-113">驗證 Azure 資源管理員要求</span><span class="sxs-lookup"><span data-stu-id="18392-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="18392-114">hello 備份和還原的 REST API 使用 Azure 資源管理員並具有不同的驗證機制比 hello REST Api 來管理您 API 管理的實體。</span><span class="sxs-lookup"><span data-stu-id="18392-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="18392-115">本節中的 hello 步驟說明如何 tooauthenticate Azure 資源管理員的要求。</span><span class="sxs-lookup"><span data-stu-id="18392-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="18392-116">如需詳細資訊，請參閱 [驗證 Azure Resource Manager 要求](http://msdn.microsoft.com/library/azure/dn790557.aspx)。</span><span class="sxs-lookup"><span data-stu-id="18392-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="18392-117">所有 hello 工作使用 hello Azure 資源管理員的資源上執行之必須使用 Azure Active Directory 使用下列步驟的 hello 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="18392-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="18392-118">新增應用程式 toohello Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="18392-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="18392-119">設定您加入的 hello 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="18392-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="18392-120">取得 hello 權杖來驗證要求 tooAzure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="18392-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="18392-121">hello 第一個步驟是 toocreate Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18392-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="18392-122">登入 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用 hello 訂用帳戶包含您的 API 管理服務執行個體，並瀏覽 toohello**應用程式**預設 Azure Active Directory 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="18392-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="18392-123">如果 hello Azure Active Directory 預設目錄是不可見的 tooyour 帳戶，hello Azure 訂用帳戶 toogrant hello hello 連絡系統管理員所需的權限 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="18392-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![建立 Azure Active Directory 應用程式][api-management-add-aad-application]

<span data-ttu-id="18392-125">按一下 [新增]，[新增我的組織正在開發的應用程式]，然後選擇 [原生用戶端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18392-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="18392-126">輸入描述性名稱，然後按一下 hello 下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="18392-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="18392-127">輸入預留位置 URL，例如`http://resources`hello**重新導向 URI**，就如同它是必要的欄位，但不是會更新版本使用 hello 值。</span><span class="sxs-lookup"><span data-stu-id="18392-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="18392-128">按一下 [hello] 核取方塊 toosave hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18392-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="18392-129">Hello 應用程式儲存之後，按一下**設定**，捲動 toohello**權限 tooother 應用程式**區段，然後按一下 **新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="18392-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![新增權限][api-management-aad-permissions-add]

<span data-ttu-id="18392-131">選取**Windows** **Azure 服務管理 API**按一下 hello 核取方塊 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18392-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![新增權限][api-management-aad-permissions]

<span data-ttu-id="18392-133">按一下**委派的權限**旁邊新加入的 hello **Windows** **Azure 服務管理 API**應用程式中，核取方塊 hello**存取 Azure服務管理 （預覽）**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="18392-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![新增權限][api-management-aad-delegated-permissions]

<span data-ttu-id="18392-135">先前 tooinvoking hello 產生的 Api hello 備份和還原它，就需要 tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="18392-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="18392-136">hello 下列範例會使用 hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget 封裝 tooretrieve hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="18392-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

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
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="18392-137">取代`{tentand id}`， `{application id}`，和`{redirect uri}`使用下列指示的 hello。</span><span class="sxs-lookup"><span data-stu-id="18392-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="18392-138">取代`{tenant id}`hello 的 hello 您剛才建立的 Azure Active Directory 應用程式的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="18392-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="18392-139">您可以按一下來存取 hello 識別碼**檢視端點**。</span><span class="sxs-lookup"><span data-stu-id="18392-139">You can access hello id by clicking **View endpoints**.</span></span>

![端點][api-management-aad-default-directory]

![端點][api-management-endpoint]

<span data-ttu-id="18392-142">取代`{application id}`和`{redirect uri}`使用 hello**用戶端識別碼**hello URL 從 hello 和**重新導向 Uri**來自 Azure Active Directory 應用程式的區段**設定**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="18392-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![資源][api-management-aad-resources]

<span data-ttu-id="18392-144">一旦指定 hello 值，hello 程式碼範例將返回語彙基元的類似 toohello，下列範例。</span><span class="sxs-lookup"><span data-stu-id="18392-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![權杖][api-management-arm-token]

<span data-ttu-id="18392-146">呼叫 hello 備份和還原 hello 下列各節中所述的作業之前，設定 REST 呼叫的 hello 授權要求標頭。</span><span class="sxs-lookup"><span data-stu-id="18392-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="18392-147"><a name="step1"> </a>備份 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="18392-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="18392-148">下列 HTTP 要求的 API 管理服務問題 hello 向上 tooback:</span><span class="sxs-lookup"><span data-stu-id="18392-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="18392-149">其中：</span><span class="sxs-lookup"><span data-stu-id="18392-149">where:</span></span>

* <span data-ttu-id="18392-150">`subscriptionId`-hello 訂用帳戶包含您正嘗試 toobackup hello API 管理服務識別碼</span><span class="sxs-lookup"><span data-stu-id="18392-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="18392-151">`resourceGroupName`-hello 'Api 表單的預設值-{服務區域}' 中的字串其中`service-region`識別 hello hello 想 toobackup API 管理服務的裝載位置的 Azure 區域，例如：`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="18392-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="18392-152">`serviceName`-hello hello 您要進行的備份在其建立 hello 時指定的 API 管理服務名稱</span><span class="sxs-lookup"><span data-stu-id="18392-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="18392-153">`api-version` - 取代為 `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="18392-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="18392-154">Hello hello 要求主體中指定 hello 目標 Azure 儲存體帳戶名稱、 存取金鑰、 blob 容器名稱，以及備份名稱：</span><span class="sxs-lookup"><span data-stu-id="18392-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="18392-155">設定 hello hello 值`Content-Type`要求標頭太`application/json`。</span><span class="sxs-lookup"><span data-stu-id="18392-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="18392-156">備份是一項長時間執行的作業，可能需要多個分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="18392-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="18392-157">如果 hello 要求成功，並已起始 hello 備份程序將會收到`202 Accepted`回應狀態碼和`Location`標頭。</span><span class="sxs-lookup"><span data-stu-id="18392-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="18392-158">請 'GET' 要求在 hello toohello URL`Location`標頭 toofind 出 hello hello 作業狀態。</span><span class="sxs-lookup"><span data-stu-id="18392-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="18392-159">Hello 備份正在進行時，您將繼續 tooreceive '202 已接受' 的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="18392-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="18392-160">回應碼`200 OK`會指出 hello 備份作業成功完成。</span><span class="sxs-lookup"><span data-stu-id="18392-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="18392-161">請注意下列條件約束進行的備份要求時的 hello。</span><span class="sxs-lookup"><span data-stu-id="18392-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="18392-162">**容器**hello 要求主體中指定**必須存在於**。</span><span class="sxs-lookup"><span data-stu-id="18392-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="18392-163">備份進行時，請「避免嘗試任何服務管理作業」  ，如提升或降低 SKU、變更網域名稱等。</span><span class="sxs-lookup"><span data-stu-id="18392-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="18392-164">還原**備份只會保證 30 天**自其建立 hello 快照。</span><span class="sxs-lookup"><span data-stu-id="18392-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="18392-165">**使用量資料**用來建立分析報表**就不會包含**hello 備份中。</span><span class="sxs-lookup"><span data-stu-id="18392-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="18392-166">使用[Azure API 管理 REST API] [ Azure API Management REST API] tooperiodically 擷取分析報表，以妥善保存。</span><span class="sxs-lookup"><span data-stu-id="18392-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="18392-167">hello 與您執行服務備份的頻率會影響您的復原點目標。</span><span class="sxs-lookup"><span data-stu-id="18392-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="18392-168">toominimize 它建議實作定期備份，以及執行指定備份後進行重要變更 tooyour API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="18392-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="18392-169">**變更**提出的 toohello 服務組態 （例如應用程式開發介面、 原則、 開發人員入口網站的外觀），備份作業正在進行**可能不會包含在 hello 備份，因此將會遺失**。</span><span class="sxs-lookup"><span data-stu-id="18392-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="18392-170"><a name="step2"> </a>還原 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="18392-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="18392-171">toorestore API 管理服務從先前建立的備份進行下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="18392-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="18392-172">其中：</span><span class="sxs-lookup"><span data-stu-id="18392-172">where:</span></span>

* <span data-ttu-id="18392-173">`subscriptionId`-hello 訂用帳戶包含您要還原備份時的 hello API 管理服務識別碼</span><span class="sxs-lookup"><span data-stu-id="18392-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="18392-174">`resourceGroupName`-hello 'Api 表單的預設值-{服務區域}' 中的字串其中`service-region`識別 hello Azure 區域裝載 hello API 管理服務，您要還原至備份的位置，例如：`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="18392-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="18392-175">`serviceName`-hello hello API 管理 hello 其建立時指定還原到的服務名稱</span><span class="sxs-lookup"><span data-stu-id="18392-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="18392-176">`api-version` - 取代為 `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="18392-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="18392-177">Hello hello 要求主體中指定 hello 備份檔案位置，也就是 Azure 儲存體帳戶名稱、 存取金鑰、 blob 容器名稱，以及備份名稱：</span><span class="sxs-lookup"><span data-stu-id="18392-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="18392-178">設定 hello hello 值`Content-Type`要求標頭太`application/json`。</span><span class="sxs-lookup"><span data-stu-id="18392-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="18392-179">還原是長時間執行的作業，可能會佔用 too30 或多個分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="18392-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="18392-180">如果 hello 要求成功，已起始 hello 還原程序，您會收到`202 Accepted`回應狀態碼和`Location`標頭。</span><span class="sxs-lookup"><span data-stu-id="18392-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="18392-181">請 'GET' 要求在 hello toohello URL`Location`標頭 toofind 出 hello hello 作業狀態。</span><span class="sxs-lookup"><span data-stu-id="18392-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="18392-182">Hello 還原正在進行時，您將繼續 tooreceive '202 已接受' 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="18392-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="18392-183">回應碼`200 OK`會指出 hello 還原作業成功完成。</span><span class="sxs-lookup"><span data-stu-id="18392-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18392-184">**hello SKU**的 hello 服務還原到**必須符合**hello hello 的 SKU 備份正在還原服務。</span><span class="sxs-lookup"><span data-stu-id="18392-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="18392-185">**變更**提出的 toohello 服務組態 （例如應用程式開發介面、 原則、 開發人員入口網站的外觀），還原作業正在進行中**可能會覆寫**。</span><span class="sxs-lookup"><span data-stu-id="18392-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="18392-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18392-186">Next steps</span></span>
<span data-ttu-id="18392-187">簽出 hello 遵循 hello 備份/還原程序的兩個不同的逐步解說的 Microsoft 部落格。</span><span class="sxs-lookup"><span data-stu-id="18392-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="18392-188">複寫 Azure API 管理帳戶 (英文)</span><span class="sxs-lookup"><span data-stu-id="18392-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="18392-189">感謝您 tooGisela 她比重 toothis 發行項。</span><span class="sxs-lookup"><span data-stu-id="18392-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="18392-190">Azure API 管理：備份和還原組態 (英文)</span><span class="sxs-lookup"><span data-stu-id="18392-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="18392-191">藉由 Stuart 詳細 hello 方法不符合 hello 正式的指導，但它是非常有趣。</span><span class="sxs-lookup"><span data-stu-id="18392-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

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
