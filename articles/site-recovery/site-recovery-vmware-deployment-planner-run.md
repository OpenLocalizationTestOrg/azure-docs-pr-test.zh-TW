---
title: "VMware 到 Azure 的 Azure Site Recovery Deployment Planner | Microsoft Docs"
description: "本文說明針對 VMware 到 Azure 的案例執行 Azure Site Recovery 部署規劃工具的模式。"
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/04/2017
ms.author: nisoneji
ms.openlocfilehash: 9aedd5561397c78622a43f39f423c618000a2a33
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2018
---
# <a name="run-azure-site-recovery-deployment-planner-for-vmware-to-azure"></a>針對 VMware 到 Azure 執行 Azure Site Recovery 部署規劃工具
本文是 VMware 到 Azure 生產部署的 Azure Site Recovery Deployment Planner 使用者指南。


## <a name="modes-of-running-deployment-planner"></a>執行部署規劃工具的模式
您可以在下列任何模式中執行命令列工具 (ASRDeploymentPlanner.exe)： 

1.  [分析](#profile-vmware-vms)
2.  [報告產生](#generate-report)
3.  [取得輸送量](#get-throughput)

首先，在分析模式中執行此工具，以蒐集 VM 資料變換和 IOPS。 接著，執行此工具來產生報告，以找出網路頻寬、儲存體需求和 DR 成本。

## <a name="profile-vmware-vms"></a>分析 VMware VM
在分析模式中，Deployment Planner 工具會連接到 vCenter Server/vSphere ESXi 主機，以收集有關 VM 的效能資料。

* 分析作業不會直接連線到生產 VM，所以不會影響其效能。 所有效能資料都是從 vCenter Server/vSphere ESXi 主機收集而來。
* 為了確保分析對伺服器造成的影響微不足道，工具會每隔 15 分鐘查詢一次 VCenter Server/vSphere EXSi 主機。 此查詢間隔並不會損及分析精確度，因為此工具會儲存每分鐘的效能計數器資料。

### <a name="create-a-list-of-vms-to-profile"></a>建立要剖析的 VM 清單
首先，您需有要分析的 VM 清單。 您可以在下列程序中使用 VMware vSphere PowerCLI 命令，取得 vCenter Server 或 vSphere ESXi 主機上的所有 VM 名稱。 或者，您可以列出您想要以手動方式剖析的好記 VM 名稱 / IP 位址。

1. 登入已安裝 VMware vSphere PowerCLI 的 VM。
2. 開啟 VMware vSphere PowerCLI 主控台。
3. 確保已啟用指令碼的執行原則。 如果已停用，請在系統管理員模式中啟動 VMware vSphere PowerCLI 主控台，然後執行下列命令來啟用它︰

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. 如果 Connect-VIServer 無法辨識為 Cmdlet 名稱，您可能需要執行下列命令。
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. 若要取得 vCenter Server/vSphere ESXi 主機的所有 VM 名稱並將此清單儲存在 .txt 檔案中，請執行此處所列的兩個命令。
以您的輸入取代 &lsaquo;server name&rsaquo;、&lsaquo;user name&rsaquo;、&lsaquo;password&rsaquo;、&lsaquo;outputfile.txt&rsaquo;。

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. 在「記事本」中開啟輸出檔案，然後將您要剖析的所有 VM 名稱複製到另一個檔案 (例如 ProfileVMList.txt)，每一行一個 VM 名稱。 此檔案可做為命令列工具之 -VMListFile 參數的輸入。

    ![Deployment Planner 中的 VM 名稱清單
](media/site-recovery-vmware-deployment-planner-run/profile-vm-list-v2a.png)

### <a name="start-profiling"></a>開始分析
取得要分析的 VM 清單之後，您可以在分析模式中執行此工具。 以下是要在分析模式中執行之工具的必要和選擇性參數清單。

```
ASRDeploymentPlanner.exe -Operation StartProfiling /?
```

| 參數名稱 | 說明 |
|---|---|
| -Operation | StartProfiling |
| -Server | 要剖析其 VM 之 vCenter Server/vSphere ESXi 主機的完整網域名稱或 IP 位址。|
| -User | 用於連線至 vCenter Server/vSphere ESXi 主機的使用者名稱。 使用者必須至少具備唯讀存取權限。|
| -VMListFile | 包含要剖析之 VM 清單的檔案。 此檔案路徑可以是絕對或相對路徑。 此檔案的每一行應包含一個 VM 名稱/IP 位址。 檔案中指定的虛擬機器名稱應該與 vCenter Server/vSphere ESXi 主機上的 VM 名稱相同。<br>例如，VMList.txt 檔案包含下列 VM︰<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
|-NoOfMinutesToProfile|要執行分析的分鐘數。 最小值為 30 分鐘。|
|-NoOfHoursToProfile|要執行分析的時數。|
| -NoOfDaysToProfile | 要執行分析的天數。 建議您執行分析 7 天以上，以確保觀察到指定期間內您環境中的工作負載模式，並用來提供精確的建議。 |
|-Virtualization|指定虛擬化類型 (VMware 或 Hyper-V)。|
| -Directory | (選用) 用來儲存分析期間所產生之分析資料的通用命名慣例 (UNC) 或本機目錄路徑。 如果未指定目錄名稱，目前路徑下名為 'ProfiledData' 的目錄將會做為預設目錄。 |
| -Password | (選用) 用來連線至 vCenter Server/vSphere ESXi 主機的密碼。 如果現在未指定密碼，系統將會在命令執行時提示您輸入密碼。|
|-Port|(選用) 要連線到 vCenter/ESXi 主機的連接埠號碼。 預設連接埠為 443。|
|-Protocol| (選用) 指定用來連線至 vCenter 的通訊協定 ('http' 或 'https')。 預設通訊協定為 https。|
| -StorageAccountName | (選用) 儲存體帳戶名稱，用於找出從內部部署至 Azure 的資料複寫可達成的輸送量。 此工具會將測試資料上傳到此儲存體帳戶，以計算輸送量。 儲存體帳戶必須是一般用途 v1 或 storageV2 (一般用途 v2)|
| -StorageAccountKey | (選用) 用來存取儲存體帳戶的儲存體帳戶金鑰。 移至 [Azure 入口網站] > [儲存體帳戶] > [<儲存體帳戶名稱>] > [設定] > [存取金鑰] > [Key1]。 |
| -Environment | (選擇性) 這是您的目標 Azure 儲存體帳戶環境。 可以是下列三個值之一 - AzureCloud、AzureUSGovernment、AzureChinaCloud。 預設值為 AzureCloud。 當目標 Azure 區域是 Azure US Government 或 Azure China 雲端時，請使用此參數。 |


我們建議至少分析您的 VM 7 天以上。 如果變換模式在一個月內改變，我們建議在您看到最大變換的一週內進行分析。 最好的方法是分析 31 天，以取得更好的建議。 在分析期間，ASRDeploymentPlanner.exe 會持續執行。 此工具會採用分析階段輸入 (以天為單位)。 如需工具快速測試或概念證明，您可以分析幾個小時或幾分鐘。 允許的最小分析時間為 30 分鐘。

在分析期間，您可以選擇性地傳送儲存體帳戶名稱和金鑰，以尋找 Site Recovery 可在從組態伺服器或處理序伺服器複寫至 Azure 時達成的輸送量。 如果未在分析期間傳送儲存體帳戶名稱和金鑰，此工具就不會計算可達成的輸送量。

您可以針對不同組的 VM 執行多個工具執行個體。 確保 VM 名稱不會在任何分析集中重複出現。 例如，若已剖析 10 部 VM (VM1 到 VM10)，而在幾天後您想要剖析另外 5 部 VM (VM11 到 VM15)，您可以針對第二組的 VM (VM11 到 VM15) 從另一個命令列主控台執行此工具。 確保第二組的 VM 沒有任何來自第一個分析執行個體的 VM 名稱，或您使用不同的輸出目錄進行第二次執行。 如有兩個工具執行個體用於分析相同的 VM 並使用相同的輸出目錄，所產生的報告則會不正確。

根據預設，此工具設定為分析並產生最多 1000 個 VM 的報告。 您可以藉由變更 ASRDeploymentPlanner.exe.config 檔案中的 MaxVMsSupported 索引鍵值來變更限制。
```
<!-- Maximum number of vms supported-->
<add key="MaxVmsSupported" value="1000"/>
```
使用預設設定，來分析假設 1500 個 VM，建立兩個 VMList.txt 檔案。 其中一個包含 1000 個 VM 和另一個包含 500 個 VM 的清單。 執行兩個 ASR 部署規劃工具的執行個體，其中一個包含 VMList1.txt，另一個包含 VMList2.txt。 您可以使用相同的目錄路徑來儲存兩個 VMList VM 的已分析資料。 

我們已經看到，作業會以硬體設定 (特別是執行工具從而產生報告之伺服器的 RAM 大小) 作為基礎，可能會因記憶體不足而發生失敗。 如果您的硬體良好，可以將 MaxVMsSupported 變更為任何較高的值。  

如果您有多部 vCenter 伺服器，就必須針對每一部 vCenter 伺服器執行一個 ASRDeploymentPlanner 的執行個體來進行分析。

在分析作業開始時會擷取一次 VM 組態，並儲存在名為 VMDetailList.xml 的檔案。 產生報告時會使用此資訊。 從分析開始到結尾，不會擷取任何 VM 組態變更 (例如，增加的核心、磁碟或 NIC 數目)。 如果有分析的 VM 組態在分析過程中發生變更，在公開預覽版本中，以下是在產生報告時取得最新 VM 詳細資料的因應措施：

* 備份 VMdetailList.xml，然後從其目前的位置刪除此檔案。
* 在報告產生時傳遞 -User 和 -Password 引數。

分析命令會在分析目錄中產生數個檔案。 請勿刪除任何檔案，因為這麼做會影響報告產生。

#### <a name="example-1-profile-vms-for-30-days-and-find-the-throughput-from-on-premises-to-azure"></a>範例 1︰剖析 VM 30 天，並找出從內部部署至 Azure 的輸送量
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Virtualization VMware -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>範例 2︰剖析 VM 15 天

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Virtualization VMware -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-60-minutes-for-a-quick-test-of-the-tool"></a>範例 3：分析 VM 60 分鐘以便快速測試工具
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Virtualization VMware -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfMinutesToProfile 60  -User vCenterUser1
```

#### <a name="example-4-profile-vms-for-2-hours-for-a-proof-of-concept"></a>範例 4：分析 VM 2 小時以取得概念證明
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Virtualization VMware -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -NoOfHoursToProfile 2 -User vCenterUser1
```

>[!NOTE]
>
>* 如果此工具執行所在的伺服器已重新啟動或已當機，或如果您使用 Ctrl + C 關閉工具，則會保留剖析的資料。 不過，過去 15 分鐘的剖析資料有可能會遺失。 在這種情況下，請在伺服器開始備份之後，於分析模式中重新執行此工具。
>* 傳遞儲存體帳戶名稱和金鑰時，此工具會在分析的最後一個步驟測量輸送量。 如果此工具在分析完成前關閉，則不會計算輸送量。 若要在產生報告之前找到輸送量，您可以從命令列主控台執行 GetThroughput 作業。 否則，產生的報告不會包含輸送量資訊。


## <a name="generate-report"></a>產生報告
此工具會產生啟用巨集的 Microsoft Excel 檔案 (XLSM) 做為報告輸出，其中摘要說明所有的部署建議。 此報告的名稱為 DeploymentPlannerReport_<unique numeric identifier>.xlsm 且置於指定的目錄中。

分析完成後，您可以在報告產生模式中執行工具。 下表包含要在報告產生模式中執行之必要和選用工具參數的清單。

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|參數名稱 | 說明 |
|-|-|
| -Operation | GenerateReport |
| -Server |  將產生報告之已分析 VM 所在的 vCenter/vSphere Server 完整網域名稱或 IP 位址 (使用您在分析時所用的相同名稱或 IP 位址)。 請注意，如果您在分析時使用 vCenter Server，則無法使用 vSphere Server 產生報告，反之亦然。|
| -VMListFile | 包含要產生報告之已剖析 VM 清單的檔案。 此檔案路徑可以是絕對或相對路徑。 此檔案的每一行應包含一個 VM 名稱或 IP 位址。 檔案中指定的 VM 名稱應該與 vCenter Server/vSphere ESXi 主機上的 VM 名稱相同，並符合分析期間所用的名稱。|
|-Virtualization|指定虛擬化類型 (VMware 或 Hyper-V)。|
| -Directory | (選用) 儲存分析資料 (分析期間產生的檔案) 的 UNC 或本機目錄路徑。 產生報告時需要這項資料。 如未指定，將會使用 ‘ProfiledData’ 目錄。 |
| -GoalToCompleteIR | (選用) 必須完成已剖析 VM 之初始複寫的時數。 所產生的報告會提供可以在指定的時間內完成初始複寫的 VM 數目。 預設值為 72 小時。 |
| -User | (選用) 用於連線至 vCenter/vSphere Server 的使用者名稱。 此名稱用來擷取 VM 的最新組態資訊，例如磁碟數目、核心數目和 NIC 數目)，以使用於報告中。 如未提供此名稱，則會使用在分析開始時收集的組態資訊。 |
| -Password | (選用) 用來連線至 vCenter Server/vSphere ESXi 主機的密碼。 如果未將此密碼指定為一個參數，系統將會在命令執行時提示您稍後輸入密碼。 |
|-Port|(選用) 要連線到 vCenter/ESXi 主機的連接埠號碼。 預設連接埠為 443。|
|-Protocol|(選用) 指定用來連線至 vCenter 的通訊協定 ('http' 或 'https')。 預設通訊協定為 https。|
| -DesiredRPO | (選用) 以分鐘為單位的所需復原點目標。 預設值是 15 分鐘。|
| -Bandwidth | 頻寬 (以 Mbps 為單位)。 此參數用來計算指定的頻寬可達成的 RPO。 |
| -StartDate | (選用) 採用 MM-DD-YYYY:HH:MM 格式 (24 小時制) 的開始日期和時間。 StartDate 必須與 EndDate 一起指定。 若已指定 StartDate，則會針對在 StartDate 與 EndDate 之間收集的剖析資料產生報告。 |
| -EndDate | (選用) 採用 MM-DD-YYYY:HH:MM 格式 (24 小時制) 的結束日期和時間。 EndDate 必須與 StartDate 一起指定。 若已指定 EndDate，則會針對在 StartDate 與 EndDate 之間收集的剖析資料產生報告。 |
| -GrowthFactor | (選用) 以百分比表示的成長因子。 預設值為 30%。 |
| -UseManagedDisks | (選擇性) UseManagedDisks - 是/否。 預設值為 [是]。 計算可以放入單一儲存體帳戶的虛擬機器數目時，請考慮在受控磁碟而不是非受控磁碟上進行虛擬機器的容錯移轉/測試容錯移轉。 |
|-SubscriptionId |(選用) 訂用帳戶 GUID。 使用這個參數來產生成本估計報告，其中包含以您的訂用帳戶為基礎的最新價格 (以指定的貨幣計價)，與您的訂用帳戶相關聯的優惠，以及適用於您特定目標 Azure 區域的優惠。|
|-TargetRegion|(選用) 複寫的目標 Azure 區域。 因為 Azure 在每個區域有不同的成本，若要產生特定目標 Azure 區域的報告，請使用此參數。<br>預設值是 WestUS2 或上次使用的目標區域。<br>請參閱[支援的目標區域](site-recovery-vmware-deployment-planner-cost-estimation.md#supported-target-regions)清單。|
|-OfferId|(選用) 與指定訂用帳戶相關聯的優惠。 預設值為 MS-AZR-0003P (預付型方案)。|
|-Currency|(選用) 在所產生的報告中用於顯示成本的貨幣。 預設值是美元 ($) 或上次使用的貨幣。<br>請參閱[支援的貨幣](site-recovery-vmware-deployment-planner-cost-estimation.md#supported-currencies)清單。|

根據預設，此工具設定為分析並產生最多 1000 個 VM 的報告。 您可以藉由變更 ASRDeploymentPlanner.exe.config 檔案中的 MaxVMsSupported 索引鍵值來變更限制。
```
<!-- Maximum number of vms supported-->
<add key="MaxVmsSupported" value="1000"/>
```

#### <a name="example-1-generate-a-report-with-default-values-when-the-profiled-data-is-on-the-local-drive"></a>範例 1︰當剖析的資料位於本機磁碟機時，使用預設值來產生報告
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualiztion VMware -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-the-profiled-data-is-on-a-remote-server"></a>範例 2︰當剖析的資料位於遠端伺服器時產生報告
您應具備遠端目錄的讀取/寫入存取權。
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualization VMware -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-to-complete-ir-within-specified-time"></a>範例 3︰使用特定頻寬和目標來產生報告，以在指定的時間內完成 IR
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualization VMware -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-the-default-30-percent"></a>範例 4︰使用 5% (而非預設值 30%) 的成長因子來產生報告
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualzation VMware -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>範例 5︰使用剖析資料子集來產生報告
例如，您有 30 天的剖析資料，而只想要產生 20 天的報告。
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualization VMware -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>範例 6：針對 5 分鐘 RPO 產生報告
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualization VMware -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

#### <a name="example-7-generate-a-report-for-south-india-azure-region-with-indian-rupee-and-specific-offer-id"></a>範例 7：使用印度盧比和特定優惠識別碼，產生南印度 Azure 區域的報告
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Virtualization VMware  -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -SubscriptionID 4d19f16b-3e00-4b89-a2ba-8645edf42fe5 -OfferID MS-AZR-0148P -TargetRegion southindia -Currency INR
```

## <a name="percentile-value-used-for-the-calculation"></a>用來計算的百分位數值
**工具在產生報告時，會使用分析期間所收集之效能計量的哪些預設百分位數值？**

此工具預設為在所有 VM 的分析期間收集之讀/寫 IOPS、寫入 IOPS 及資料變換的第 95 個百分位數值。 此計量可確保您的 VM 可以看到第 100 個百分位數尖峰，因為暫存事件不會用來判斷您的目標儲存體帳戶和來源頻寬需求。 例如，暫存事件可能是一天執行一次的備份作業、定期資料庫檢索或分析報告產生活動，或其他類似的短期時間點事件。

使用第 95 個百分位數值可提供實際工作負載特性的真實情況，並且讓您在 Azure 上執行這些工作負載時獲得最佳效能。 我們不希望您會需要變更這個數字。 如果您變更此數字 (例如，變更為第 90 個百分位數)，您可以更新預設資料夾中的組態檔 ASRDeploymentPlanner.exe.config 並加以儲存，以產生現有剖析資料的新報告。
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>成長因子考量
**規劃部署時為何應考量成長因子？**

假設使用量可能會隨著時間增加，請務必考量您的工作負載特性成長。 防護就緒之後，如果工作負載特性變更，在未停用並重新啟用保護的情況下，您無法切換到不同的儲存體帳戶進行保護。

例如，假設您的 VM 位於置於標準儲存體複寫帳戶中。 接下來的三個月，可能會發生幾項變更︰

* 在 VM 上執行之應用程式的使用者數目會增加。
* 結果在 VM 上增加的變換會要求 VM 移至進階儲存體，Site Recovery 複寫才可以保持一致。
* 因此，您必須對進階儲存體帳戶停用並重新啟用保護。

強烈建議您在規劃部署期間規劃成長，而預設值為 30%。 您最瞭解您的應用程式使用量模式和成長預測，而且可以在產生報告時相應變更此數字。 此外，您可以使用不同的成長因子，針對相同的剖析資料產生多份報告，判斷哪些目標儲存體和來源頻寬建議最適合您。

產生的 Microsoft Excel 報告包含下列資訊：

* [內部部署摘要](site-recovery-vmware-deployment-planner-analyze-report.md#on-premises-summary)
* [建議](site-recovery-vmware-deployment-planner-analyze-report.md#recommendations)
* [VM<->儲存體放置](site-recovery-vmware-deployment-planner-analyze-report.md#vm-storage-placement)
* [相容的 VM](site-recovery-vmware-deployment-planner-analyze-report.md#compatible-vms)
* [不相容的 VM](site-recovery-vmware-deployment-planner-analyze-report.md#incompatible-vms)
* [成本估計](site-recovery-vmware-deployment-planner-cost-estimation.md)

![Deployment Planner](media/site-recovery-vmware-deployment-planner-analyze-report/Recommendations-v2a.png)

## <a name="get-throughput"></a>取得輸送量

若要預估 Site Recovery 在複寫期間可以達成的輸送量 (從內部部署至 Azure)，請以 GetThroughput 模式執行工具。 此工具會計算來自工具執行所在伺服器的輸送量。 在理想情況下，此伺服器是以組態伺服器調整大小指南為基礎。 如果您已在內部部署環境部署 Site Recovery 基礎結構元件，請在組態伺服器上執行此工具。

開啟命令列主控台，然後移至 Site Recovery 部署規劃工具資料夾。 使用下列參數執行 ASRDeploymentPlanner.exe。

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|參數名稱 | 說明 |
|-|-|
| -Operation | GetThroughput |
|-Virtualization|指定虛擬化類型 (VMware 或 Hyper-V)。|
| -Directory | (選用) 儲存分析資料 (分析期間產生的檔案) 的 UNC 或本機目錄路徑。 產生報告時需要這項資料。 如未指定目錄，則會使用 ‘ProfiledData’ 目錄。 |
| -StorageAccountName | 儲存體帳戶名稱，用於找出從內部部署至 Azure 的資料複寫所耗用的頻寬。 此工具會將測試資料上傳到此儲存體帳戶，以找出所耗用的頻寬。 儲存體帳戶必須是一般用途 v1 或 storageV2 (一般用途 v2)。|
| -StorageAccountKey | 用來存取儲存體帳戶的儲存體帳戶金鑰。 移至 Azure 入口網站 > 儲存體帳戶 > <儲存體帳戶名稱> > 設定 > 存取金鑰 > Key1 (或傳統儲存體帳戶的主要存取金鑰)。 |
| -VMListFile | 包含要剖析之 VM 清單的檔案，以便計算所耗用的頻寬。 此檔案路徑可以是絕對或相對路徑。 此檔案的每一行應包含一個 VM 名稱/IP 位址。 檔案中指定的 VM 名稱應該與 vCenter Server/vSphere ESXi 主機上的 VM 名稱相同。<br>例如，VMList.txt 檔案包含下列 VM︰<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (選擇性) 這是您的目標 Azure 儲存體帳戶環境。 可以是下列三個值之一 - AzureCloud、AzureUSGovernment、AzureChinaCloud。 預設值為 AzureCloud。 當目標 Azure 區域是 Azure US Government 或 Azure China 雲端時，請使用此參數。 |

此工具會在指定的目錄中建立數個 64MB asrvhdfile<#>.vhd 檔案 (其中 # 是檔案數目)。 此工具會將這些檔案上傳至儲存體帳戶，以找出輸送量。 測量輸送量之後，此工具會從儲存體帳戶和本機伺服器中刪除所有這類檔案。 如果此工具在計算輸送量時因為任何原因而終止，它不會從儲存體或本機伺服器中刪除檔案。 您必須手動加以刪除。

輸送量會在指定的時間點進行測量，而這是 Site Recovery 可以在複寫期間內達成的最大輸送量 (前提是所有其他因子維持不變)。 例如，如果任何應用程式開始在相同網路上耗用更多頻寬，則複寫期間的實際輸送量會有所不同。 如果您是從組態伺服器執行 GetThroughput 命令，此工具不會留意任何受保護的 VM 和進行中的複寫作業。 如果 GetThroughput 作業在受保護的 VM 有高度資料變換時執行，則測量的輸送量結果會不同。 建議在分析期間的各種時間點執行此工具，以了解可在不同時間達成的輸送量等級。 在報告中，此工具會顯示最後測量的輸送量。

### <a name="example"></a>範例
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> 在具有與組態伺服器相同之儲存體和 CPU 特性的伺服器上執行此工具。
>
> 如需複寫，請設定建議的頻寬，以符合當時的 100% RPO。 在設定適當的頻寬之後，如果您未看到此工具所報告的達成輸送量有任何增加，請執行下列作業︰
>
>  1. 檢查以判斷是否有任何網路服務品質 (QoS) 會限制 Site Recovery 輸送量。
>
>  2. 檢查以判斷 Site Recovery 保存庫是否位於支援的最近實體 Microsoft Azure 區域，以縮小網路延遲。
>
>  3. 檢查本機儲存體特性，以判斷是否可以改善硬體 (例如 HDD 變成 SSD)。
>
>  4. 變更處理序伺服器中的 Site Recovery 設定，以[增加用於複寫的網路頻寬](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth)。

## <a name="next-steps"></a>後續步驟
* [分析已產生的報告](site-recovery-vmware-deployment-planner-analyze-report.md)。

