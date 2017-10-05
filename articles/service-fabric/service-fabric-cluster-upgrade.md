---
title: "升級 Azure Service Fabric 叢集 | Microsoft Docs"
description: "升級執行 Service Fabric 叢集的 Service Fabric 程式碼和/或組態，包括設定叢集更新模式、升級憑證、新增應用程式連接埠、修補作業系統等等。 執行升級時，您可以期待些什麼？"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 7ea71ab891583c51b3c07a4d0a9f0b4f54e56669
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="b0408-104">升級 Azure Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b0408-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0408-105">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="b0408-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="b0408-106">獨立叢集</span><span class="sxs-lookup"><span data-stu-id="b0408-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="b0408-107">對於任何現代系統，可升級性的設計是產品達到長期成功的關鍵。</span><span class="sxs-lookup"><span data-stu-id="b0408-107">For any modern system, designing for upgradability is key to achieving long-term success of your product.</span></span> <span data-ttu-id="b0408-108">Azure Service Fabric 叢集是您所擁有，但部分由 Microsoft 管理的資源。</span><span class="sxs-lookup"><span data-stu-id="b0408-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="b0408-109">本文說明自動管理的部分以及您可以自行設定的部分。</span><span class="sxs-lookup"><span data-stu-id="b0408-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-the-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="b0408-110">控制叢集上執行的網狀架構版本</span><span class="sxs-lookup"><span data-stu-id="b0408-110">Controlling the fabric version that runs on your Cluster</span></span>
<span data-ttu-id="b0408-111">您可以將叢集設定為在 Microsoft 釋出網狀架構升級時自動接收該升級，或者，您也可以選取您想讓叢集執行的受支援網狀架構版本。</span><span class="sxs-lookup"><span data-stu-id="b0408-111">You can set your cluster to receive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster to be on.</span></span>

<span data-ttu-id="b0408-112">作法是在入口網站上設定 “upgrademode” 叢集組態，或是建立時或稍後在即時叢集上使用 Resource Manager 來設定。</span><span class="sxs-lookup"><span data-stu-id="b0408-112">You do this by setting the "upgradeMode" cluster configuration on the portal or using Resource Manager at the time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="b0408-113">請務必保持您的叢集一律執行支援的網狀架構版本。</span><span class="sxs-lookup"><span data-stu-id="b0408-113">Make sure to keep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="b0408-114">當我們宣布發行新版本的 Service Fabric 時，從當日起至少 60 天後，舊版就會標示為結束支援。</span><span class="sxs-lookup"><span data-stu-id="b0408-114">As and when we announce the release of a new version of service fabric, the previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="b0408-115">新的版本會於 [Service Fabric 小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)發佈。</span><span class="sxs-lookup"><span data-stu-id="b0408-115">the  The new releases are announced [on the service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="b0408-116">那時就有新的版本可選擇。</span><span class="sxs-lookup"><span data-stu-id="b0408-116">The new release is available to choose then.</span></span> 
> 
> 

<span data-ttu-id="b0408-117">叢集執行的版本在到期前 14 天會產生健全狀況事件，使您的叢集進入警告健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="b0408-117">14 days prior to the expiry of the release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="b0408-118">在您升級至支援的網狀架構版本之前，叢集會停留在警告狀態。</span><span class="sxs-lookup"><span data-stu-id="b0408-118">The cluster remains in a warning state until you upgrade to a supported fabric version.</span></span>

### <a name="setting-the-upgrade-mode-via-portal"></a><span data-ttu-id="b0408-119">透過入口網站設定升級模式</span><span class="sxs-lookup"><span data-stu-id="b0408-119">Setting the upgrade mode via portal</span></span>
<span data-ttu-id="b0408-120">當您建立叢集時，您可以將叢集設為自動或手動。</span><span class="sxs-lookup"><span data-stu-id="b0408-120">You can set the cluster to automatic or manual when you are creating the cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="b0408-122">在即時叢集上，您可以利用管理體驗將叢集設為自動或手動。</span><span class="sxs-lookup"><span data-stu-id="b0408-122">You can set the cluster to automatic or manual when on a live cluster, using the manage experience.</span></span> 

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-portal"></a><span data-ttu-id="b0408-123">在設定為手動模式的叢集上，透過入口網站升級至新的版本。</span><span class="sxs-lookup"><span data-stu-id="b0408-123">Upgrading to a new version on a cluster that is set to Manual mode via portal.</span></span>
<span data-ttu-id="b0408-124">若要升級至新的版本，只需要從下拉式清單中選取可用的版本並儲存即可。</span><span class="sxs-lookup"><span data-stu-id="b0408-124">To upgrade to a new version, all you need to do is select the available version from the dropdown and save.</span></span> <span data-ttu-id="b0408-125">Fabric 升級會自動開始進行。</span><span class="sxs-lookup"><span data-stu-id="b0408-125">The Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="b0408-126">升級期間會遵守叢集健康狀態原則 (綜合節點健康狀態和所有在叢集中執行之應用程式的健康狀態)。</span><span class="sxs-lookup"><span data-stu-id="b0408-126">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="b0408-127">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-127">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="b0408-128">請往下捲動本文，以深入了解如何設定這些自訂的健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="b0408-128">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="b0408-129">在解決導致復原的問題後，您需要依照之前的相同步驟再次起始升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-129">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-the-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="b0408-131">透過 Resource Manager 範本設定升級模式</span><span class="sxs-lookup"><span data-stu-id="b0408-131">Setting the upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="b0408-132">將 “upgradeMode" 組態新增至 Microsoft.ServiceFabric/clusters 資源定義，並將 “clusterCodeVersion" 設為其中一個支援的網狀架構版本，如下所示，然後部署範本。</span><span class="sxs-lookup"><span data-stu-id="b0408-132">Add the "upgradeMode" configuration to the Microsoft.ServiceFabric/clusters resource definition and set the "clusterCodeVersion" to one of the supported fabric versions as shown below and then deploy the template.</span></span> <span data-ttu-id="b0408-133">“upgradeMode" 的有效值為 “Manual” 或 “Automatic”。</span><span class="sxs-lookup"><span data-stu-id="b0408-133">The valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-a-resource-manager-template"></a><span data-ttu-id="b0408-135">在設定為手動模式的叢集上，透過 Resource Manager 範本升級至新的版本。</span><span class="sxs-lookup"><span data-stu-id="b0408-135">Upgrading to a new version on a cluster that is set to Manual mode via a Resource Manager template.</span></span>
<span data-ttu-id="b0408-136">當叢集處於手動模式時，若要升級至新的版本，請將 “clusterCodeVersion" 變更為支援的版本並部署。</span><span class="sxs-lookup"><span data-stu-id="b0408-136">When the cluster is in Manual mode, to upgrade to a new version, change the "clusterCodeVersion" to a supported version and deploy it.</span></span> <span data-ttu-id="b0408-137">部署範本時會自動展開 Fabric 升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-137">The deployment of the template, kicks of the Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="b0408-138">升級期間會遵守叢集健康狀態原則 (綜合節點健康狀態和所有在叢集中執行之應用程式的健康狀態)。</span><span class="sxs-lookup"><span data-stu-id="b0408-138">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="b0408-139">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-139">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="b0408-140">請往下捲動本文，以深入了解如何設定這些自訂的健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="b0408-140">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="b0408-141">在解決導致復原的問題後，您需要依照之前的相同步驟再次起始升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-141">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="b0408-142">針對給定的訂用帳戶取得所有環境的所有可用版本清單</span><span class="sxs-lookup"><span data-stu-id="b0408-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="b0408-143">執行下列命令，應該會得到類似如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="b0408-143">Run the following command, and you should get an output similar to this.</span></span>

<span data-ttu-id="b0408-144">“supportExpiryUtc” 會告訴您給定的版本即將到期或已過期。</span><span class="sxs-lookup"><span data-stu-id="b0408-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="b0408-145">最新版本並無有效日期 - 它的值為 "9999-12-31T23:59:59.9999999"，這只是表示到期日還沒有設定。</span><span class="sxs-lookup"><span data-stu-id="b0408-145">The latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that the expiry date is not yet set.</span></span>

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-the-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="b0408-146">叢集升級模式為自動時的 Fabric 升級行為</span><span class="sxs-lookup"><span data-stu-id="b0408-146">Fabric upgrade behavior when the cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="b0408-147">Microsoft 會維護 Azure 叢集中執行的網狀架構程式碼和組態。</span><span class="sxs-lookup"><span data-stu-id="b0408-147">Microsoft maintains the fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="b0408-148">視情況需要，我們會對軟體執行受監視的自動升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-148">We perform automatic monitored upgrades to the software on an as-needed basis.</span></span> <span data-ttu-id="b0408-149">升級的項目可能是程式碼、組態或兩者。</span><span class="sxs-lookup"><span data-stu-id="b0408-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="b0408-150">為了確保您的應用程式不受這些升級影響或將影響降到最低，我們會分成下列階段執行升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-150">To make sure that your application suffers no impact or minimal impact due to these upgrades, we perform the upgrades in the following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="b0408-151">階段 1：使用所有叢集健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="b0408-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="b0408-152">在這個階段，升級會一次進行一個升級網域，而已在叢集中執行的應用程式會繼續執行，而不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="b0408-152">During this phase, the upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="b0408-153">升級期間會遵守叢集健康狀態原則 (綜合節點健康狀態和所有在叢集中執行之應用程式的健康狀態)。</span><span class="sxs-lookup"><span data-stu-id="b0408-153">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="b0408-154">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-154">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="b0408-155">然後系統會傳送一封電子郵件給訂用帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="b0408-155">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="b0408-156">電子郵件中包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b0408-156">The email contains the following information:</span></span>

* <span data-ttu-id="b0408-157">我們必須回復叢集升級的通知。</span><span class="sxs-lookup"><span data-stu-id="b0408-157">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="b0408-158">建議的修復動作 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="b0408-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="b0408-159">距離我們執行階段 2 之前的天數 (n)。</span><span class="sxs-lookup"><span data-stu-id="b0408-159">The number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="b0408-160">如果有任何升級因為基礎結構方面的原因而失敗，我們會試著多執行幾次相同的升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-160">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="b0408-161">在電子郵件寄送日期的 n 天之後，我們會繼續進行階段 2。</span><span class="sxs-lookup"><span data-stu-id="b0408-161">After the n days from the date the email was sent, we proceed to Phase 2.</span></span>

<span data-ttu-id="b0408-162">如果符合叢集健康狀態原則，則升級會被視為成功並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="b0408-162">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="b0408-163">在此階段執行初次升級或重新執行任何升級期間，可能會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="b0408-163">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="b0408-164">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="b0408-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="b0408-165">這是為了避免傳送給您太多電子郵件，如果您收到電子郵件，則應該將其視為例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b0408-165">This is to avoid sending you too many emails--receiving an email should be seen as an exception to normal.</span></span> <span data-ttu-id="b0408-166">我們預期大部分的叢集升級都會成功，並不會影響您的應用程式可用性。</span><span class="sxs-lookup"><span data-stu-id="b0408-166">We expect most of the cluster upgrades to succeed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="b0408-167">階段 2：僅使用預設健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="b0408-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="b0408-168">此階段的健康狀態原則的設定方式為，升級開始時健康狀態良好的應用程式數目在升級程序期間會維持不變。</span><span class="sxs-lookup"><span data-stu-id="b0408-168">The health policies in this phase are set in such a way that the number of applications that were healthy at the beginning of the upgrade remains the same for the duration of the upgrade process.</span></span> <span data-ttu-id="b0408-169">和階段 1 一樣，階段 2 的升級會一次進行一個升級網域，而已在叢集中執行的應用程式會繼續執行，而不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="b0408-169">As in Phase 1, the Phase 2 upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="b0408-170">在升級期間，會遵守叢集健康狀態原則 (節點健康狀態和所有在叢集中執行之應用程式的健康狀態的組合)。</span><span class="sxs-lookup"><span data-stu-id="b0408-170">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to for the duration of the upgrade.</span></span>

<span data-ttu-id="b0408-171">如果不符合生效的叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-171">If the cluster health policies in effect are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="b0408-172">然後系統會傳送一封電子郵件給訂用帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="b0408-172">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="b0408-173">電子郵件中包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b0408-173">The email contains the following information:</span></span>

* <span data-ttu-id="b0408-174">我們必須回復叢集升級的通知。</span><span class="sxs-lookup"><span data-stu-id="b0408-174">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="b0408-175">建議的修復動作 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="b0408-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="b0408-176">距離我們執行階段 3 之前的天數 (n)。</span><span class="sxs-lookup"><span data-stu-id="b0408-176">The number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="b0408-177">如果有任何升級因為基礎結構方面的原因而失敗，我們會試著多執行幾次相同的升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-177">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="b0408-178">在 n 天到達的前幾天會傳送提醒電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b0408-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="b0408-179">在電子郵件寄送日期的 n 天之後，我們會繼續進行階段 3。</span><span class="sxs-lookup"><span data-stu-id="b0408-179">After the n days from the date the email was sent, we proceed to Phase 3.</span></span> <span data-ttu-id="b0408-180">您必須認真看待我們在階段 2 寄送的電子郵件並採取補救動作。</span><span class="sxs-lookup"><span data-stu-id="b0408-180">The emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="b0408-181">如果符合叢集健康狀態原則，則升級會被視為成功並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="b0408-181">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="b0408-182">在此階段執行初次升級或重新執行任何升級期間，可能會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="b0408-182">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="b0408-183">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="b0408-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="b0408-184">階段 3：使用積極的叢集健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="b0408-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="b0408-185">此階段的這些健康狀態原則的目的是升級完成，而不是應用程式的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="b0408-185">These health policies in this phase are geared towards completion of the upgrade rather than the health of the applications.</span></span> <span data-ttu-id="b0408-186">很少叢集升級會最後會變成這個階段。</span><span class="sxs-lookup"><span data-stu-id="b0408-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="b0408-187">如果您的叢集進入這個階段，表示您的應用程式很可能會變成狀況不良和 (或) 失去可用性。</span><span class="sxs-lookup"><span data-stu-id="b0408-187">If your cluster gets to this phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="b0408-188">類似其他兩個階段，階段 3 升級會一次進行一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="b0408-188">Similar to the other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="b0408-189">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-189">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="b0408-190">如果有任何升級因為基礎結構方面的原因而失敗，我們會試著多執行幾次相同的升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-190">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="b0408-191">之後，便會鎖住叢集，使它不會再收到支援和 (或) 升級。</span><span class="sxs-lookup"><span data-stu-id="b0408-191">After that, the cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="b0408-192">系統會傳送含有這項資訊的電子郵件給訂用帳戶擁有者，其中也會附上修復動作。</span><span class="sxs-lookup"><span data-stu-id="b0408-192">An email with this information is sent to the subscription owner, along with the remedial actions.</span></span> <span data-ttu-id="b0408-193">我們預期不會有任何叢集會進入階段 3 失敗的狀態。</span><span class="sxs-lookup"><span data-stu-id="b0408-193">We do not expect any clusters to get into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="b0408-194">如果符合叢集健康狀態原則，則升級會被視為成功並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="b0408-194">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="b0408-195">在此階段執行初次升級或重新執行任何升級期間，可能會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="b0408-195">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="b0408-196">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="b0408-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="b0408-197">您控制的叢集組態</span><span class="sxs-lookup"><span data-stu-id="b0408-197">Cluster configurations that you control</span></span>
<span data-ttu-id="b0408-198">除了能夠設定叢集升級模式，您還可以在即時叢集上變更以下的設定。</span><span class="sxs-lookup"><span data-stu-id="b0408-198">In addition to the ability to set the cluster upgrade mode, Here are the configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="b0408-199">憑證</span><span class="sxs-lookup"><span data-stu-id="b0408-199">Certificates</span></span>
<span data-ttu-id="b0408-200">您可以透過入口網站輕鬆地新增或刪除叢集和用戶端的憑證。</span><span class="sxs-lookup"><span data-stu-id="b0408-200">You can add new or delete certificates for the cluster and client via the portal easily.</span></span> <span data-ttu-id="b0408-201">請參閱 [這份文件了解詳細指示](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="b0408-201">Refer to [this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![顯示 Azure 入口網站中憑證指紋的螢幕擷取畫面。][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="b0408-203">應用程式連接埠</span><span class="sxs-lookup"><span data-stu-id="b0408-203">Application ports</span></span>
<span data-ttu-id="b0408-204">您可以透過變更與節點類型相關聯的負載平衡器資源屬性來變更應用程式連接埠。</span><span class="sxs-lookup"><span data-stu-id="b0408-204">You can change application ports by changing the Load Balancer resource properties that are associated with the node type.</span></span> <span data-ttu-id="b0408-205">您可以使用入口網站，或是直接使用資源管理員 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b0408-205">You can use the portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="b0408-206">若要在某個節點類型中的所有 VM 上開啟新的連接埠，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="b0408-206">To open a new port on all VMs in a node type, do the following:</span></span>

1. <span data-ttu-id="b0408-207">將新的探查新增至適當的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0408-207">Add a new probe to the appropriate load balancer.</span></span>
   
    <span data-ttu-id="b0408-208">如果您已使用入口網站部署您的叢集，則負載平衡器會命名為 "LB-name of the Resource group-NodeTypename"，每個節點類型有一個負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0408-208">If you deployed your cluster by using the portal, the load balancers are named "LB-name of the Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="b0408-209">因為負載平衡器名稱只有在資源群組中是唯一的，所以最好在特定資源群組下搜尋名稱。</span><span class="sxs-lookup"><span data-stu-id="b0408-209">Since the load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![顯示在入口網站中對負載平衡器新增探查的螢幕擷取畫面。][AddingProbes]
2. <span data-ttu-id="b0408-211">將新規則加入至負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0408-211">Add a new rule to the load balancer.</span></span>
   
    <span data-ttu-id="b0408-212">使用您在上一個步驟中建立的探查，對相同的負載平衡器加入新的規則。</span><span class="sxs-lookup"><span data-stu-id="b0408-212">Add a new rule to the same load balancer by using the probe that you created in the previous step.</span></span>
   
    ![在入口網站中對負載平衡器新增規則。][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="b0408-214">放置屬性</span><span class="sxs-lookup"><span data-stu-id="b0408-214">Placement properties</span></span>
<span data-ttu-id="b0408-215">對於每個節點類型，您可以加入您要在應用程式中使用的自訂放置屬性。</span><span class="sxs-lookup"><span data-stu-id="b0408-215">For each of the node types, you can add custom placement properties that you want to use in your applications.</span></span> <span data-ttu-id="b0408-216">NodeType 是您可使用而不需明確新增的預設屬性。</span><span class="sxs-lookup"><span data-stu-id="b0408-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="b0408-217">如需使用放置條件約束、節點屬性及如何定義它們的詳細資訊，請參閱《Service Fabric 叢集 Resource Manager 文件》 [描述您的叢集](service-fabric-cluster-resource-manager-cluster-description.md)中的＜放置條件約束和節點屬性＞一節。</span><span class="sxs-lookup"><span data-stu-id="b0408-217">For details on the use of placement constraints, node properties, and how to define them, refer to the section "Placement Constraints and Node Properties" in the Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="b0408-218">容量度量</span><span class="sxs-lookup"><span data-stu-id="b0408-218">Capacity metrics</span></span>
<span data-ttu-id="b0408-219">對於每個節點類型，您可以加入您要在應用程式中用來報告負載的自訂容量計量。</span><span class="sxs-lookup"><span data-stu-id="b0408-219">For each of the node types, you can add custom capacity metrics that you want to use in your applications to report load.</span></span> <span data-ttu-id="b0408-220">如需使用容量度量報告負載的詳細資訊，請參閱《Service Fabric 叢集 Resource Manager 文件》的[描述您的叢集](service-fabric-cluster-resource-manager-cluster-description.md)和[度量和負載](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b0408-220">For details on the use of capacity metrics to report load, refer to the Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="b0408-221">Fabric 升級設 - 健全狀況原則</span><span class="sxs-lookup"><span data-stu-id="b0408-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="b0408-222">您可以為網狀架構升級指定自訂的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="b0408-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="b0408-223">如果已將您的叢集設定為自動網狀架構升級，這些原則會套用於自動網狀架構升級的階段 1。</span><span class="sxs-lookup"><span data-stu-id="b0408-223">If you have set your cluster to Automatic fabric upgrades, then these policies get applied to the Phase-1 of the automatic fabric upgrades.</span></span>
<span data-ttu-id="b0408-224">如果已將您的叢集設定為手動網狀架構升級，則每當您選取新版本而觸發系統開始在叢集中展開網狀架構升級時，就會套用這些原則。</span><span class="sxs-lookup"><span data-stu-id="b0408-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering the system to kick off the fabric upgrade in your cluster.</span></span> <span data-ttu-id="b0408-225">如果您不覆寫原則，則會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="b0408-225">If you do not override the policies, the defaults are used.</span></span>

<span data-ttu-id="b0408-226">在 [網狀架構升級] 刀鋒視窗下，您可以選取進階升級設定來指定自訂的健康狀態原則，或檢閱目前的設定。</span><span class="sxs-lookup"><span data-stu-id="b0408-226">You can specify the custom health policies or review the current settings under the "fabric upgrade" blade, by selecting the advanced upgrade settings.</span></span> <span data-ttu-id="b0408-227">檢閱下列作法圖片。</span><span class="sxs-lookup"><span data-stu-id="b0408-227">Review the following picture on how to.</span></span> 

![管理自訂的健康狀態原則][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="b0408-229">自訂叢集的 Fabric 設定</span><span class="sxs-lookup"><span data-stu-id="b0408-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="b0408-230">請參閱 [Service Fabric 叢集網狀架構設定](service-fabric-cluster-fabric-settings.md) ，以了解該自訂什麼及如何自訂。</span><span class="sxs-lookup"><span data-stu-id="b0408-230">Refer to [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="b0408-231">組成叢集的 VM 上的作業系統修補程式</span><span class="sxs-lookup"><span data-stu-id="b0408-231">OS patches on the VMs that make up the cluster</span></span>
<span data-ttu-id="b0408-232">請參閱[修補程式協調流程應用程式](service-fabric-patch-orchestration-application.md)，可在叢集上部署，以協調的方式從 Windows Update 安裝修補程式，讓服務隨時可供使用。</span><span class="sxs-lookup"><span data-stu-id="b0408-232">Refer to [Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster to install patches from Windows Update in an orchestrated manner, keeping the services available all the time.</span></span> 

### <a name="os-upgrades-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="b0408-233">組成叢集的 VM 上的作業系統升級</span><span class="sxs-lookup"><span data-stu-id="b0408-233">OS upgrades on the VMs that make up the cluster</span></span>
<span data-ttu-id="b0408-234">如果您必須升級叢集的虛擬機器上的作業系統映像，則必須一次升級一部 VM。</span><span class="sxs-lookup"><span data-stu-id="b0408-234">If you must upgrade the OS image on the virtual machines of the cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="b0408-235">您要負責這項升級，因為目前沒有將這項升級自動化。</span><span class="sxs-lookup"><span data-stu-id="b0408-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0408-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0408-236">Next steps</span></span>
* <span data-ttu-id="b0408-237">了解如何自訂一些 [Service Fabric 叢集網狀架構設定](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="b0408-237">Learn how to customize some of the [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="b0408-238">了解如何 [相應放大和相應縮小叢集](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="b0408-238">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="b0408-239">了解 [應用程式升級](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="b0408-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
