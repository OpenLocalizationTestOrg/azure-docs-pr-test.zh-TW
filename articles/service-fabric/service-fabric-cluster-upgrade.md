---
title: "aaaUpgrade Azure Service Fabric 叢集 |Microsoft 文件"
description: "升級 hello Service Fabric 程式碼和/或執行 Service Fabric 叢集，包括設定叢集更新模式，升級憑證，新增應用程式連接埠，執行發行作業系統修補程式的組態，並以此類推。 執行 hello 升級時，您可以預期什麼？"
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
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="35c86-104">升級 Azure Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="35c86-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35c86-105">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="35c86-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="35c86-106">獨立叢集</span><span class="sxs-lookup"><span data-stu-id="35c86-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="35c86-107">對於任何現代的系統，可升級性的設計是產品金鑰 tooachieving 長期成功。</span><span class="sxs-lookup"><span data-stu-id="35c86-107">For any modern system, designing for upgradability is key tooachieving long-term success of your product.</span></span> <span data-ttu-id="35c86-108">Azure Service Fabric 叢集是您所擁有，但部分由 Microsoft 管理的資源。</span><span class="sxs-lookup"><span data-stu-id="35c86-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="35c86-109">本文說明自動管理的部分以及您可以自行設定的部分。</span><span class="sxs-lookup"><span data-stu-id="35c86-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="35c86-110">控制在您的叢集執行的 hello fabric 版本</span><span class="sxs-lookup"><span data-stu-id="35c86-110">Controlling hello fabric version that runs on your Cluster</span></span>
<span data-ttu-id="35c86-111">您可以設定叢集 tooreceive 自動架構升級為 Microsoft 發行，或者您可以選取您要叢集 toobe 支援的網狀架構版本。</span><span class="sxs-lookup"><span data-stu-id="35c86-111">You can set your cluster tooreceive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster toobe on.</span></span>

<span data-ttu-id="35c86-112">您可以設定 hello"upgradeMode"hello 入口網站或使用資源管理員在建立 hello 時或稍後即時叢集上的叢集設定</span><span class="sxs-lookup"><span data-stu-id="35c86-112">You do this by setting hello "upgradeMode" cluster configuration on hello portal or using Resource Manager at hello time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="35c86-113">請確定 tookeep 您永遠執行支援的網狀架構版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="35c86-113">Make sure tookeep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="35c86-114">如下，當我們宣佈 hello 發行新版的 service fabric hello 舊版標示為的支援即將結束後的 60 天內從該日期的最小值。</span><span class="sxs-lookup"><span data-stu-id="35c86-114">As and when we announce hello release of a new version of service fabric, hello previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="35c86-115">hello hello 新版本上經過宣布[hello 服務網狀架構小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)。</span><span class="sxs-lookup"><span data-stu-id="35c86-115">hello  hello new releases are announced [on hello service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="35c86-116">hello 新版本，就可用 toochoose。</span><span class="sxs-lookup"><span data-stu-id="35c86-116">hello new release is available toochoose then.</span></span> 
> 
> 

<span data-ttu-id="35c86-117">14 天先前 toohello 到期的 hello 發行您的叢集正在執行，就會產生健全狀況事件，以您的叢集到警告健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="35c86-117">14 days prior toohello expiry of hello release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="35c86-118">您升級 tooa 支援的 fabric 版本之前，hello 叢集會維持在警告狀態。</span><span class="sxs-lookup"><span data-stu-id="35c86-118">hello cluster remains in a warning state until you upgrade tooa supported fabric version.</span></span>

### <a name="setting-hello-upgrade-mode-via-portal"></a><span data-ttu-id="35c86-119">透過入口網站設定 hello 升級模式</span><span class="sxs-lookup"><span data-stu-id="35c86-119">Setting hello upgrade mode via portal</span></span>
<span data-ttu-id="35c86-120">當您建立 hello 叢集時，您可以設定 hello 叢集 tooautomatic 或手動。</span><span class="sxs-lookup"><span data-stu-id="35c86-120">You can set hello cluster tooautomatic or manual when you are creating hello cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="35c86-122">您可以設定 hello 叢集 tooautomatic 或手動在即時的叢集上，使用 hello 管理體驗。</span><span class="sxs-lookup"><span data-stu-id="35c86-122">You can set hello cluster tooautomatic or manual when on a live cluster, using hello manage experience.</span></span> 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a><span data-ttu-id="35c86-123">升級 tooa tooManual 模式透過入口網站設定的叢集上的新版本。</span><span class="sxs-lookup"><span data-stu-id="35c86-123">Upgrading tooa new version on a cluster that is set tooManual mode via portal.</span></span>
<span data-ttu-id="35c86-124">tooupgrade tooa 新版本，您只需要 toodo 是從 hello 下拉式清單中選取 hello 可用版本和儲存。</span><span class="sxs-lookup"><span data-stu-id="35c86-124">tooupgrade tooa new version, all you need toodo is select hello available version from hello dropdown and save.</span></span> <span data-ttu-id="35c86-125">hello Fabric 升級取得自動開始。</span><span class="sxs-lookup"><span data-stu-id="35c86-125">hello Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="35c86-126">hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-126">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="35c86-127">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-127">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="35c86-128">更多有關此文件 tooread 捲動 tooset 這些自訂的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="35c86-128">Scroll down this document tooread more on how tooset those custom health policies.</span></span> 

<span data-ttu-id="35c86-129">一旦您修正導致 hello 復原 hello 問題，您需要 tooinitiate hello 升級同樣地，由下列 hello 與之前相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="35c86-129">Once you have fixed hello issues that resulted in hello rollback, you need tooinitiate hello upgrade again, by following hello same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="35c86-131">設定資源管理員範本透過 hello 升級模式</span><span class="sxs-lookup"><span data-stu-id="35c86-131">Setting hello upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="35c86-132">加入 hello"upgradeMode 」 組態 toohello Microsoft.ServiceFabric/clusters 資源定義和組 hello"clusterCodeVersion"tooone hello 的支援如下所示的網狀架構版本，然後再部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="35c86-132">Add hello "upgradeMode" configuration toohello Microsoft.ServiceFabric/clusters resource definition and set hello "clusterCodeVersion" tooone of hello supported fabric versions as shown below and then deploy hello template.</span></span> <span data-ttu-id="35c86-133">hello"upgradeMode"有效值為 「 手動 」 或 「 自動 」</span><span class="sxs-lookup"><span data-stu-id="35c86-133">hello valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a><span data-ttu-id="35c86-135">升級 tooa 設定資源管理員範本透過 tooManual 模式在叢集上的新版本。</span><span class="sxs-lookup"><span data-stu-id="35c86-135">Upgrading tooa new version on a cluster that is set tooManual mode via a Resource Manager template.</span></span>
<span data-ttu-id="35c86-136">Hello 叢集處於手動模式中，tooupgrade tooa 新版本時變更 hello"clusterCodeVersion"tooa 支援的版本，並將其部署。</span><span class="sxs-lookup"><span data-stu-id="35c86-136">When hello cluster is in Manual mode, tooupgrade tooa new version, change hello "clusterCodeVersion" tooa supported version and deploy it.</span></span> <span data-ttu-id="35c86-137">hello hello 範本部署的 hello Fabric 升級已盡力而為取得開始自動。</span><span class="sxs-lookup"><span data-stu-id="35c86-137">hello deployment of hello template, kicks of hello Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="35c86-138">hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-138">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="35c86-139">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-139">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="35c86-140">更多有關此文件 tooread 捲動 tooset 這些自訂的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="35c86-140">Scroll down this document tooread more on how tooset those custom health policies.</span></span> 

<span data-ttu-id="35c86-141">一旦您修正導致 hello 復原 hello 問題，您需要 tooinitiate hello 升級同樣地，由下列 hello 與之前相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="35c86-141">Once you have fixed hello issues that resulted in hello rollback, you need tooinitiate hello upgrade again, by following hello same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="35c86-142">針對給定的訂用帳戶取得所有環境的所有可用版本清單</span><span class="sxs-lookup"><span data-stu-id="35c86-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="35c86-143">執行 hello 下列命令，以及您應該取得輸出類似 toothis。</span><span class="sxs-lookup"><span data-stu-id="35c86-143">Run hello following command, and you should get an output similar toothis.</span></span>

<span data-ttu-id="35c86-144">“supportExpiryUtc” 會告訴您給定的版本即將到期或已過期。</span><span class="sxs-lookup"><span data-stu-id="35c86-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="35c86-145">hello 最新版本沒有有效的日期-它的值為"9999-12-31T23:59:59.9999999"，這就表示未尚未設定 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="35c86-145">hello latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that hello expiry date is not yet set.</span></span>

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

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="35c86-146">為 [自動] 時 hello 叢集升級模式的 fabric 升級行為</span><span class="sxs-lookup"><span data-stu-id="35c86-146">Fabric upgrade behavior when hello cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="35c86-147">Microsoft 維護 hello 網狀架構程式碼和執行於 Azure 的叢集中的組態。</span><span class="sxs-lookup"><span data-stu-id="35c86-147">Microsoft maintains hello fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="35c86-148">我們對可視需要執行受監視的自動升級 toohello 軟體。</span><span class="sxs-lookup"><span data-stu-id="35c86-148">We perform automatic monitored upgrades toohello software on an as-needed basis.</span></span> <span data-ttu-id="35c86-149">升級的項目可能是程式碼、組態或兩者。</span><span class="sxs-lookup"><span data-stu-id="35c86-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="35c86-150">toomake 確定您的應用程式有任何影響或因為 toothese 升級的影響降到最低，我們會執行 hello 升級在 hello 下列階段：</span><span class="sxs-lookup"><span data-stu-id="35c86-150">toomake sure that your application suffers no impact or minimal impact due toothese upgrades, we perform hello upgrades in hello following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="35c86-151">階段 1：使用所有叢集健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="35c86-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="35c86-152">在此階段，hello 升級繼續執行一個升級網域一次，並執行 hello 叢集中的 hello 應用程式繼續 toorun 完全不需要停機。</span><span class="sxs-lookup"><span data-stu-id="35c86-152">During this phase, hello upgrades proceed one upgrade domain at a time, and hello applications that were running in hello cluster continue toorun without any downtime.</span></span> <span data-ttu-id="35c86-153">hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-153">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="35c86-154">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-154">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="35c86-155">然後以電子郵件傳送 toohello hello 訂用帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="35c86-155">Then an email is sent toohello owner of hello subscription.</span></span> <span data-ttu-id="35c86-156">hello 電子郵件會包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="35c86-156">hello email contains hello following information:</span></span>

* <span data-ttu-id="35c86-157">我們必須 tooroll 回叢集升級的通知。</span><span class="sxs-lookup"><span data-stu-id="35c86-157">Notification that we had tooroll back a cluster upgrade.</span></span>
* <span data-ttu-id="35c86-158">建議的修復動作 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="35c86-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="35c86-159">hello 天數 (n) 我們執行階段 2 之前。</span><span class="sxs-lookup"><span data-stu-id="35c86-159">hello number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="35c86-160">我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="35c86-160">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="35c86-161">Hello 之後已傳送 hello 日期 hello 電子郵件中的 n 天，我們繼續 tooPhase 2。</span><span class="sxs-lookup"><span data-stu-id="35c86-161">After hello n days from hello date hello email was sent, we proceed tooPhase 2.</span></span>

<span data-ttu-id="35c86-162">如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="35c86-162">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="35c86-163">在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。</span><span class="sxs-lookup"><span data-stu-id="35c86-163">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="35c86-164">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="35c86-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="35c86-165">這是傳送您太多的電子郵件-收到電子郵件應該視為例外狀況 toonormal tooavoid。</span><span class="sxs-lookup"><span data-stu-id="35c86-165">This is tooavoid sending you too many emails--receiving an email should be seen as an exception toonormal.</span></span> <span data-ttu-id="35c86-166">我們預期大部分的 hello 叢集升級 toosucceed 而不會影響您應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="35c86-166">We expect most of hello cluster upgrades toosucceed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="35c86-167">階段 2：僅使用預設健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="35c86-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="35c86-168">在這個階段中的 hello 健全狀況原則是設定的方式，已在 hello 開頭 hello 升級狀況良好的應用程式的 hello 數目會維持相同的 hello hello 升級程序的持續時間的 hello。</span><span class="sxs-lookup"><span data-stu-id="35c86-168">hello health policies in this phase are set in such a way that hello number of applications that were healthy at hello beginning of hello upgrade remains hello same for hello duration of hello upgrade process.</span></span> <span data-ttu-id="35c86-169">階段 1，如同 hello 階段 2 升級繼續執行一個升級網域一次，並執行 hello 叢集中的 hello 應用程式繼續 toorun 完全不需要停機。</span><span class="sxs-lookup"><span data-stu-id="35c86-169">As in Phase 1, hello Phase 2 upgrades proceed one upgrade domain at a time, and hello applications that were running in hello cluster continue toorun without any downtime.</span></span> <span data-ttu-id="35c86-170">hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 會遵守 toofor hello hello 升級期間。</span><span class="sxs-lookup"><span data-stu-id="35c86-170">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered toofor hello duration of hello upgrade.</span></span>

<span data-ttu-id="35c86-171">如果 hello 叢集健全狀況原則實際上不符合，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-171">If hello cluster health policies in effect are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="35c86-172">然後以電子郵件傳送 toohello hello 訂用帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="35c86-172">Then an email is sent toohello owner of hello subscription.</span></span> <span data-ttu-id="35c86-173">hello 電子郵件會包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="35c86-173">hello email contains hello following information:</span></span>

* <span data-ttu-id="35c86-174">我們必須 tooroll 回叢集升級的通知。</span><span class="sxs-lookup"><span data-stu-id="35c86-174">Notification that we had tooroll back a cluster upgrade.</span></span>
* <span data-ttu-id="35c86-175">建議的修復動作 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="35c86-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="35c86-176">hello 天數直到我們執行階段 3 (n)。</span><span class="sxs-lookup"><span data-stu-id="35c86-176">hello number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="35c86-177">我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="35c86-177">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="35c86-178">在 n 天到達的前幾天會傳送提醒電子郵件。</span><span class="sxs-lookup"><span data-stu-id="35c86-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="35c86-179">Hello 之後已傳送 hello 日期 hello 電子郵件中的 n 天，我們繼續 tooPhase 3。</span><span class="sxs-lookup"><span data-stu-id="35c86-179">After hello n days from hello date hello email was sent, we proceed tooPhase 3.</span></span> <span data-ttu-id="35c86-180">我們傳送給您在階段 2 中的 hello 電子郵件必須謹慎地加以，必須採取修復動作。</span><span class="sxs-lookup"><span data-stu-id="35c86-180">hello emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="35c86-181">如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="35c86-181">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="35c86-182">在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。</span><span class="sxs-lookup"><span data-stu-id="35c86-182">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="35c86-183">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="35c86-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="35c86-184">階段 3：使用積極的叢集健康狀態原則執行升級</span><span class="sxs-lookup"><span data-stu-id="35c86-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="35c86-185">在這個階段中的這些健全狀況原則會導向到 hello 升級完成，而不是 hello hello 應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="35c86-185">These health policies in this phase are geared towards completion of hello upgrade rather than hello health of hello applications.</span></span> <span data-ttu-id="35c86-186">很少叢集升級會最後會變成這個階段。</span><span class="sxs-lookup"><span data-stu-id="35c86-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="35c86-187">如果您的叢集取得 toothis 階段，會有很好的機會，您的應用程式會變為狀況不良 （或） 失去可用性。</span><span class="sxs-lookup"><span data-stu-id="35c86-187">If your cluster gets toothis phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="35c86-188">類似 toohello 其他兩個階段階段 3 升級一次前進一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="35c86-188">Similar toohello other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="35c86-189">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-189">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="35c86-190">我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="35c86-190">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="35c86-191">在這之後，已釘選 hello 叢集，使它不會再接收支援和 （或） 升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-191">After that, hello cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="35c86-192">這項資訊的電子郵件會傳送 toohello 訂用帳戶擁有者，以及 hello 修復動作。</span><span class="sxs-lookup"><span data-stu-id="35c86-192">An email with this information is sent toohello subscription owner, along with hello remedial actions.</span></span> <span data-ttu-id="35c86-193">我們不會任何叢集 tooget 進入階段 3 已失敗時的狀態。</span><span class="sxs-lookup"><span data-stu-id="35c86-193">We do not expect any clusters tooget into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="35c86-194">如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。</span><span class="sxs-lookup"><span data-stu-id="35c86-194">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="35c86-195">在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。</span><span class="sxs-lookup"><span data-stu-id="35c86-195">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="35c86-196">執行成功不會有任何電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="35c86-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="35c86-197">您控制的叢集組態</span><span class="sxs-lookup"><span data-stu-id="35c86-197">Cluster configurations that you control</span></span>
<span data-ttu-id="35c86-198">此外 toohello 能力 tooset hello 叢集升級模式，以下是您可以變更即時叢集的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="35c86-198">In addition toohello ability tooset hello cluster upgrade mode, Here are hello configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="35c86-199">憑證</span><span class="sxs-lookup"><span data-stu-id="35c86-199">Certificates</span></span>
<span data-ttu-id="35c86-200">您可以加入新檔案或輕鬆地刪除 hello 叢集和用戶端透過 hello 入口網站的憑證。</span><span class="sxs-lookup"><span data-stu-id="35c86-200">You can add new or delete certificates for hello cluster and client via hello portal easily.</span></span> <span data-ttu-id="35c86-201">請參閱太[如需詳細指示這份文件](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="35c86-201">Refer too[this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![如果螢幕擷取畫面顯示 hello Azure 入口網站中的憑證指紋。][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="35c86-203">應用程式連接埠</span><span class="sxs-lookup"><span data-stu-id="35c86-203">Application ports</span></span>
<span data-ttu-id="35c86-204">您可以藉由變更 hello 與 hello 節點類型相關聯的負載平衡器資源屬性來變更應用程式連接埠。</span><span class="sxs-lookup"><span data-stu-id="35c86-204">You can change application ports by changing hello Load Balancer resource properties that are associated with hello node type.</span></span> <span data-ttu-id="35c86-205">您可以使用 hello 入口網站，或您可以直接使用資源管理員 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="35c86-205">You can use hello portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="35c86-206">tooopen 新的連接埠節點型別中所有 Vm 上 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="35c86-206">tooopen a new port on all VMs in a node type, do hello following:</span></span>

1. <span data-ttu-id="35c86-207">加入新的探查 toohello 適當負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="35c86-207">Add a new probe toohello appropriate load balancer.</span></span>
   
    <span data-ttu-id="35c86-208">如果您使用 hello 入口網站部署您的叢集，hello 負載平衡器名為"LB-name 的 hello 資源群組 NodeTypename"，其中每個節點類型。</span><span class="sxs-lookup"><span data-stu-id="35c86-208">If you deployed your cluster by using hello portal, hello load balancers are named "LB-name of hello Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="35c86-209">因為 hello 負載平衡器名稱是唯一的只有在資源群組內，最好是如果您的特定資源群組下搜尋它們。</span><span class="sxs-lookup"><span data-stu-id="35c86-209">Since hello load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![螢幕擷取畫面顯示新增探查 tooa 的負載平衡器 hello 入口網站中。][AddingProbes]
2. <span data-ttu-id="35c86-211">加入新的規則 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="35c86-211">Add a new rule toohello load balancer.</span></span>
   
    <span data-ttu-id="35c86-212">加入新的規則 toohello 相同負載平衡器使用您建立 hello 上一個步驟中的 hello 探查。</span><span class="sxs-lookup"><span data-stu-id="35c86-212">Add a new rule toohello same load balancer by using hello probe that you created in hello previous step.</span></span>
   
    ![Hello 入口網站中加入新的規則 tooa 負載平衡器。][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="35c86-214">放置屬性</span><span class="sxs-lookup"><span data-stu-id="35c86-214">Placement properties</span></span>
<span data-ttu-id="35c86-215">針對每個 hello 節點型別，您可以新增您想 toouse 要在應用程式中的自訂放置屬性。</span><span class="sxs-lookup"><span data-stu-id="35c86-215">For each of hello node types, you can add custom placement properties that you want toouse in your applications.</span></span> <span data-ttu-id="35c86-216">NodeType 是您可使用而不需明確新增的預設屬性。</span><span class="sxs-lookup"><span data-stu-id="35c86-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="35c86-217">如需 hello 使用位置條件約束，節點屬性的詳細資訊和如何 toodefine 它們，請參閱 toohello > 一節 「 放置條件約束和節點屬性 」，在 hello Service Fabric 叢集資源管理員文件中的有關[描述您的叢集](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="35c86-217">For details on hello use of placement constraints, node properties, and how toodefine them, refer toohello section "Placement Constraints and Node Properties" in hello Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="35c86-218">容量度量</span><span class="sxs-lookup"><span data-stu-id="35c86-218">Capacity metrics</span></span>
<span data-ttu-id="35c86-219">針對每個 hello 節點型別，您可以加入您在應用程式 tooreport 負載想 toouse 自訂容量計量。</span><span class="sxs-lookup"><span data-stu-id="35c86-219">For each of hello node types, you can add custom capacity metrics that you want toouse in your applications tooreport load.</span></span> <span data-ttu-id="35c86-220">Hello 使用容量度量 tooreport 負載的詳細資訊，請參閱有關 toohello Service Fabric 叢集資源管理員的文件[描述叢集](service-fabric-cluster-resource-manager-cluster-description.md)和[度量和負載](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="35c86-220">For details on hello use of capacity metrics tooreport load, refer toohello Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="35c86-221">Fabric 升級設 - 健全狀況原則</span><span class="sxs-lookup"><span data-stu-id="35c86-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="35c86-222">您可以為網狀架構升級指定自訂的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="35c86-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="35c86-223">如果您已經設定叢集 tooAutomatic fabric 升級，這些原則會取得套用的 toohello 階段 1 的 hello 網狀架構自動升級。</span><span class="sxs-lookup"><span data-stu-id="35c86-223">If you have set your cluster tooAutomatic fabric upgrades, then these policies get applied toohello Phase-1 of hello automatic fabric upgrades.</span></span>
<span data-ttu-id="35c86-224">如果您已將您手動網狀架構的叢集升級，則這些原則會套用每次您選取觸發 hello 系統 tookick 關閉 hello fabric 升級在叢集中的新版本。</span><span class="sxs-lookup"><span data-stu-id="35c86-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering hello system tookick off hello fabric upgrade in your cluster.</span></span> <span data-ttu-id="35c86-225">如果您不會覆寫 hello 原則，則會使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="35c86-225">If you do not override hello policies, hello defaults are used.</span></span>

<span data-ttu-id="35c86-226">您可以指定 hello 自訂健全狀況原則，或選取進階升級設定 hello 檢閱 hello hello 「 網狀架構升級 」 刀鋒視窗中，在目前的設定。</span><span class="sxs-lookup"><span data-stu-id="35c86-226">You can specify hello custom health policies or review hello current settings under hello "fabric upgrade" blade, by selecting hello advanced upgrade settings.</span></span> <span data-ttu-id="35c86-227">檢閱 hello 如何下列圖片。</span><span class="sxs-lookup"><span data-stu-id="35c86-227">Review hello following picture on how to.</span></span> 

![管理自訂的健康狀態原則][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="35c86-229">自訂叢集的 Fabric 設定</span><span class="sxs-lookup"><span data-stu-id="35c86-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="35c86-230">請參閱太[服務網狀架構叢集網狀架構設定](service-fabric-cluster-fabric-settings.md)功能以及自訂它們。</span><span class="sxs-lookup"><span data-stu-id="35c86-230">Refer too[service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a><span data-ttu-id="35c86-231">Hello hello 叢集所組成的 Vm 上的 OS 修補程式</span><span class="sxs-lookup"><span data-stu-id="35c86-231">OS patches on hello VMs that make up hello cluster</span></span>
<span data-ttu-id="35c86-232">參照太[修補程式的協調流程的應用程式](service-fabric-patch-orchestration-application.md)的可部署於您叢集 tooinstall 修補程式，從 Windows Update 以協調的方式，保留 hello world hello 服務可用。</span><span class="sxs-lookup"><span data-stu-id="35c86-232">Refer too[Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster tooinstall patches from Windows Update in an orchestrated manner, keeping hello services available all hello time.</span></span> 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a><span data-ttu-id="35c86-233">在 hello hello 叢集所組成的 Vm 上的作業系統升級</span><span class="sxs-lookup"><span data-stu-id="35c86-233">OS upgrades on hello VMs that make up hello cluster</span></span>
<span data-ttu-id="35c86-234">如果您必須升級 hello hello 的 hello 叢集的虛擬機器上的作業系統映像，您必須進行一個 VM 一次。</span><span class="sxs-lookup"><span data-stu-id="35c86-234">If you must upgrade hello OS image on hello virtual machines of hello cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="35c86-235">您要負責這項升級，因為目前沒有將這項升級自動化。</span><span class="sxs-lookup"><span data-stu-id="35c86-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35c86-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35c86-236">Next steps</span></span>
* <span data-ttu-id="35c86-237">深入了解如何 toocustomize 某些 hello[服務網狀架構叢集網狀架構設定](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="35c86-237">Learn how toocustomize some of hello [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="35c86-238">了解如何太[叢集及相應放大](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="35c86-238">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="35c86-239">了解 [應用程式升級](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="35c86-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
