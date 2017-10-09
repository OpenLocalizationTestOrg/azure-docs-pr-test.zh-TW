---
title: "aaaAzure VMware 到 azure Site Recovery 部署計劃 |Microsoft 文件"
description: "這是 hello Azure Site Recovery 部署規劃使用者指南。"
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
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery Deployment Planner
本文是 VMware-Azure 生產部署的 hello Azure 站台復原部署規劃使用者指南。

## <a name="overview"></a>概觀

您開始使用 Site Recovery 的保護任何 VMware 虛擬機器 (Vm) 之前，請配置足夠的頻寬，根據您每日資料變更率，toomeet 所需要的復原點目標 (RPO)。 為確定 toodeploy hello 正確數目的組態伺服器與處理序伺服器在內部。

您也需要 toocreate hello 正確類型及數量的目標 Azure 儲存體帳戶。 您可建立標準或進階儲存體帳戶，將使用量隨時間增加所造成的來源生產伺服器成長納入考量。 選擇每個 VM，根據工作負載特性 （例如，每個第二個 [IOPS] 或資料變換量的讀取/寫入 I/O 作業） 的 hello 儲存類型，而站台復原限制。

目前僅適用於 hello VMware-Azure 案例的命令列工具的 hello Site Recovery 部署規劃公用預覽。 您可以從遠端剖析 VMware Vm 成功複寫使用此工具 （而不實際執行會影響恕不另行通知） toounderstand hello 頻寬和 Azure 儲存體需求，並測試容錯移轉。 您可以執行 hello 工具而不需要安裝任何站台復原元件在內部。 不過，精確 tooget 達到的輸送量結果，我們建議您在符合 hello 最低需求 hello 站台復原設定的伺服器，您最終需要 toodeploy 做為其中一個 hello 第一個步驟的 Windows 伺服器上執行 hello 規劃在生產環境部署。

hello 工具提供下列詳細資料的 hello:

**相容性評估**

* 以磁碟數目、磁碟大小、IOPS、變換和開機類型 (EFI/BIOS) 為基礎的 VM 合適性評估
* hello 差異複寫所需的估計的網路頻寬

**網路頻寬需求與 RPO 評估**

* hello 差異複寫所需的估計的網路頻寬
* 站台復原可以從內部部署 tooAzure 取得 hello 輸送量
* 估計頻寬 toocomplete 初始複寫指定一段時間內的 Vm toobatch，根據 hello 的 hello 數目。

**Azure 基礎結構需求**

* 每個 VM 的 hello 的存放裝置類型 （standard 或 premium 儲存體帳戶） 需求
* 設定用於複寫的標準和進階儲存體帳戶 toobe 的 hello 總數
* 以 Azure 儲存體指引為基礎的儲存體帳戶命名建議
* 所有 Vm 的 hello 儲存體帳戶位置
* 測試容錯移轉或 hello 訂用帳戶的容錯移轉之前設定 hello Azure 核心 toobe 數目
* hello Azure VM 建議的大小，每個內部部署 VM

**內部部署基礎結構需求**
* hello 需要設定伺服器的數目和處理序伺服器 toobe 部署在內部部署

>[!IMPORTANT]
>
>使用量會很有可能 tooincrease 經過一段時間，因為所有 hello 執行計算的假設工作負載特性，30%的成長納入而使用的所有程式碼剖析度量的 hello 的第 95 個百分上述的工具 (讀取/寫入 IOPS、 變換，因此等）。 這兩個元素 (成長因子和百分位數計算) 皆可設定。 toolearn 深入了解成長係數，請參閱 hello"成長係數考量 > 一節。 toolearn 有關百分位數值的詳細資訊，請參閱 hello 「 用於 hello 計算百分位數值 」 一節。
>

## <a name="requirements"></a>需求
hello 工具有兩個主要階段： 產生程式碼剖析和報表。 另外還有第三個選項 toocalculate 輸送量只有。 起始程式碼剖析和輸送量的測量從哪些 hello hello 伺服器 hello 需求會出現在下表中的 hello:

| 伺服器需求 | 說明|
|---|---|
|剖析和輸送量測量| <ul><li>作業系統：Microsoft Windows Server 2012 R2<br>(在理想情況下比對至少 hello[大小 hello 組態伺服器的建議](https://aka.ms/asr-v2a-on-prem-components))</li><li>機器組態︰8 個 vCPU、16 GB RAM、300 GB HDD</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[適用於 Visual Studio 2012 的 Microsoft Visual C++ 可轉散發套件](https://aka.ms/vcplusplus-redistributable)</li><li>從這部伺服器的網際網路存取 tooAzure</li><li>Azure 儲存體帳戶</li><li>Hello 伺服器上的系統管理員存取權</li><li>100 GB 的可用磁碟空間下限 (假設剖析平均各有 3 個磁碟的 1000 部 VM 30 天)</li><li>Too2 或高的層級應該設定 VMware vCenter 統計資料的層級設定</li><li>允許連接埠 443: ASR 部署規劃使用此連接埠 tooconnect toovCenter 伺服器/ESXi 主機</ul></ul>|
| 報告產生 | 具有 Microsoft Excel 2013 和更新版本的 Windows PC 或 Windows Server |
| 使用者權限 | 已使用 tooaccess hello VMware vCenter server/VMware vSphere ESXi 主機程式碼剖析期間的 hello 使用者帳戶的唯讀權限 |

> [!NOTE]
>
>hello 工具可以分析只 VMDK 和 RDM 磁碟的 Vm。 不能剖析具有 iSCSI 或 NFS 磁碟的 VM。 站台復原也 VMware 伺服器支援 iSCSI 和 NFS 磁碟，但 hello 工具 hello 部署規劃並非 hello 客體內，且該設定檔只能透過 vCenter 效能計數器，因為並沒有這些磁碟類型的可視性。
>

## <a name="download-and-extract-hello-public-preview"></a>下載並解壓縮 hello 公開預覽
1. 下載 hello 最新版 hello [Site Recovery 部署規劃公用預覽](https://aka.ms/asr-deployment-planner)。  
hello 工具會封裝在.zip 資料夾。 hello 目前 hello 工具版本支援 hello VMware-Azure 案例。

2. 將複製 hello.zip 資料夾 toohello Windows 伺服器要從中 toorun hello 工具。  
如果 hello 伺服器的網路存取 tooconnect toohello vCenter 伺服器 /vsphere ESXi 主機保存 hello Vm toobe 分析，您可以從 Windows Server 2012 R2 執行 hello 工具。 不過，我們建議您在其硬體設定符合 hello 的伺服器上執行 hello 工具[組態伺服器大小調整指導方針](https://aka.ms/asr-v2a-on-prem-components)。 如果您已部署站台復原元件在內部，執行 hello 工具從 hello 組態伺服器。

 我們建議您擁有 hello hello 組態伺服器 （有內建的處理序伺服器） hello hello 工具執行所在的伺服器上相同的硬體組態。 這種組態可確保該 hello 達成輸送量該 hello 工具報告符合 hello 實際輸送量在複寫期間可達成的站台復原。 hello 輸送量計算則取決於 hello 伺服器和硬體設定 （CPU、 儲存體，等等） 的 hello 伺服器上可用的網路頻寬。 如果您從任何其他伺服器執行 hello 工具，就會從該伺服器 tooMicrosoft Azure 計算 hello 輸送量。 此外，因為 hello 組態伺服器可能會與不同 hello 伺服器 hello 硬體組態，達成的 hello 輸送量 hello 工具報表，可能不正確。

3. 擷取 hello.zip 資料夾。  
hello 資料夾包含多個檔案和子資料夾。 hello 可執行檔是 ASRDeploymentPlanner.exe hello 父資料夾中。

    範例：  
    複製 hello.zip 檔案 tooE: \ 磁碟機，並將它解壓縮。
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>功能
您可以在任何 hello 下列三種模式中執行 hello 命令列工具 (ASRDeploymentPlanner.exe):

1. 剖析  
2. 報告產生
3. 取得輸送量

首先，執行 hello 工具中分析模式 toogather VM 資料變換量和 IOPS。 接下來，執行 hello 工具 toogenerate hello 報表 toofind hello 網路頻寬和儲存需求。

## <a name="profiling"></a>剖析
在程式碼剖析模式中，hello 部署規劃工具連接 toohello vCenter 伺服器 /vsphere ESXi 主機 toocollect hello VM 相關的效能資料。

* 程式碼剖析不會影響 hello 效能的 hello 實際執行的 Vm，因為沒有直接連線 toothem。 Hello vCenter 伺服器 /vsphere ESXi 主機會收集所有效能資料。
* tooensure 沒有明顯的影響 hello 伺服器因為程式碼剖析，hello 工具查詢 hello vCenter 伺服器 /vsphere ESXi 主機一次每隔 15 分鐘。 此查詢間隔並不會降低程式碼剖析的精確度，因為 hello 工具會儲存每分鐘效能計數器資料。

### <a name="create-a-list-of-vms-tooprofile"></a>建立 Vm tooprofile 的清單
首先，您需要一份 hello Vm toobe 分析。 您可以取得 vCenter 伺服器 /vsphere ESXi 主機上的所有 hello 名稱的 Vm 使用 hello 遵循程序中的 hello VMware vSphere PowerCLI 命令。 或者，您可以列出檔案 hello 易記名稱中，或 IP 位址的 hello 手動想 tooprofile 的 Vm。

1. 登入 toohello PowerCLI 安裝在該 VMware vSphere VM。
2. 開啟 hello VMware vSphere PowerCLI 主控台。
3. 確定 hello 執行原則已啟用 hello 指令碼。 如果已停用，啟動 hello VMware vSphere PowerCLI 主控台以系統管理員模式並啟用它藉由執行下列命令的 hello:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. 貴用戶選項需要 toorun hello 下列命令，如果連接 VIServer 無法辨識為 cmdlet hello 名稱。
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget vCenter 伺服器 /vsphere ESXi 上 vm 的所有 hello 名稱裝載，並將 hello 清單儲存在.txt 檔案中，執行的 hello 此處所列的兩個命令。
以您的輸入取代 &lsaquo;server name&rsaquo;、&lsaquo;user name&rsaquo;、&lsaquo;password&rsaquo;、&lsaquo;outputfile.txt&rsaquo;。

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. 在 記事本 開啟 hello 輸出檔，然後複製 您希望 tooprofile tooanother 檔案 (例如，ProfileVMList.txt)，每行一個 VM 名稱的所有 Vm 的 hello 名稱。 這個檔案作為輸入 toohello *-VMListFile* hello 命令列工具的參數。

    ![VM 名稱 清單中 hello 部署規劃](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>開始剖析
您有 Vm toobe 分析 hello 清單之後，您可以執行 hello 工具中分析模式。 以下是 hello 參數清單的必要和選擇性的 hello 工具 toorun 中分析模式。

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| 參數名稱 | 說明 |
|---|---|
| -Operation | StartProfiling |
| -Server | hello 完整的網域名稱或 IP 位址的 hello vCenter 伺服器 /vsphere ESXi 主機的 Vm 為 toobe 分析。|
| -User | hello 使用者名稱 tooconnect toohello vCenter 伺服器 /vsphere ESXi 主機。 hello 使用者需要 toohave 唯讀存取時，最小值。|
| -VMListFile | hello 包含 Vm toobe 分析 hello 清單的檔案。 hello 檔案路徑可以是絕對或相對的。 hello 檔案應包含一個 VM 名稱 /IP 位址，每行。 Hello 檔案中指定的虛擬機器名稱應該 hello 與 hello hello vCenter 伺服器 /vsphere ESXi 主機上的 VM 名稱相同。<br>例如，hello 檔案 VMList.txt 包含下列 Vm hello:<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | 執行的程式碼剖析的 toobe 的 hello 天數。 我們建議您執行程式碼剖析超過 15 天 hello hello 透過您的環境中的工作負載模式的 tooensure 指定期間觀察到和使用 tooprovide 精確的建議。 |
| -Directory | （選擇性） hello 通用命名慣例 (UNC) 或本機目錄路徑 toostore 分析程式碼剖析期間所產生的資料。 如果沒有指定目錄名稱，hello 目前路徑下名為 'ProfiledData' hello 目錄將當做 hello 預設目錄。 |
| -Password | （選擇性） hello 密碼 toouse tooconnect toohello vCenter 伺服器 /vsphere ESXi 主機。 如果您未指定其中一個現在，您會提示針對它執行 hello 命令時。|
| -StorageAccountName | （選擇性） hello 是可達成的複寫資料從使用的 toofind hello 輸送量的儲存體帳戶名稱在內部 tooAzure。 hello 工具上傳測試資料 toothis 儲存體帳戶 toocalculate 輸送量。|
| -StorageAccountKey | 已使用 tooaccess hello 儲存體帳戶的 hello （選擇性） 儲存體帳戶金鑰。 前往 Azure 入口網站 toohello > 儲存體帳戶 ><*儲存體帳戶名稱*>> 設定 > 存取金鑰 > Key1 （或傳統的儲存體帳戶的主要存取金鑰）。 |
| -Environment | (選擇性) 這是您的目標 Azure 儲存體帳戶環境。 可以是下列三個值之一 - AzureCloud、AzureUSGovernment、AzureChinaCloud。 預設值為 AzureCloud。 您的目標 Azure 區域為 Azure 美國政府或 Azure China 雲端時，請使用 hello 參數。 |


我們建議您至少 15 too30 天分析您的 Vm。 在程式碼剖析期間的 hello，ASRDeploymentPlanner.exe 會繼續執行。 hello 工具會分析階段輸入，以天為單位。 如果您想要 tooprofile 幾個小時或分鐘 hello 工具，快速測試 hello 公開預覽狀態，您必須 tooconvert hello 時間到 hello 的天數內的對等量值。 範例中，為 30 分鐘，tooprofile hello 輸入必須是 30/(60*24) = 0.021 天。 hello 最小允許程式碼剖析時間為 30 分鐘。

在剖析期間，您可以選擇性地傳遞儲存體帳戶名稱和站台復原時可以達成的複寫從 hello 組態伺服器或處理序伺服器 tooAzure hello 次金鑰 toofind hello 輸送量。 Hello 儲存體帳戶名稱和金鑰並不會在分析期間，如果 hello 工具不會計算可達到的輸送量。

您可以執行多個不同的 Vm 集合 hello 工具執行個體。 請確定不會在任何程式碼剖析集合 hello 重複 hello VM 名稱。 比方說，如果您已經分析十個 Vm (透過 VM10 VM1)，而且在幾天後您想 tooprofile 另一個的五個 Vm (VM11 透過 VM15)，您可以從另一個命令列主控台 hello 第二個集合的 Vm 執行 hello 工具 (透過 VM15 VM11)。 請確定 hello 第二個 Vm 設定不會有任何 VM 名稱，從 hello 第一個程式碼剖析執行個體，或您的第二次執行的 hello 使用不同的輸出目錄。 如果兩個執行個體的 hello 工具會使用程式碼剖析 hello 同一個 Vm 並使用 hello 相同的輸出目錄，產生的 hello 報表可能會不正確。

VM 組態都會擷取一次的作業程式碼剖析的 hello hello 開頭，並儲存在稱為 VMDetailList.xml 的檔案。 產生 hello 報告時，會使用此資訊。 不會擷取從 hello 開頭 toohello 結尾程式碼剖析的 VM 組態 （例如，次數增加核心、 磁碟或 Nic） 中的任何變更。 如果已分析的 VM 組態已變更的程式碼剖析，hello 公開預覽，在 hello 過程如下 hello 因應措施 tooget 最新 VM 詳細資料產生 hello 報表時：

* 備份 VMdetailList.xml，並刪除 hello 檔案從目前的位置。
* -使用者和密碼將引數傳遞時的報表產生 hello。

程式碼剖析命令的 hello hello 設定檔的目錄中產生數個檔案。 請勿刪除任何 hello 檔案，因為這樣做，會影響產生報告。

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>範例 1： 設定檔 Vm 30 天，以及從內部部署 tooAzure 尋找 hello 輸送量
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>範例 2︰剖析 VM 15 天

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>範例 3： 設定檔 1 小時，讓 hello 工具快速測試 Vm
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* 如果 hello 伺服器 hello 工具上執行已重新啟動或已毀損，或者如果您關閉 hello 工具使用 Ctrl + C，hello 分析資料會保留。 不過，有可能會遺失 hello 已分析資料的過去 15 分鐘內。 在這種情況下，重新執行 hello 工具中分析模式 hello 伺服器重新啟動之後。
>* 當 hello 儲存體帳戶名稱和金鑰傳遞，hello 在 hello 最後一個步驟的程式碼剖析工具的量值 hello 輸送量。 如果程式碼剖析完成之前，已關閉 hello 工具，hello 輸送量不會計算。 在產生之前 toofind hello 輸送量 hello 報表，您可以執行 hello GetThroughput 作業從 hello 命令列主控台。 否則，產生的 hello 報表不會包含 hello 輸送量資訊。


## <a name="generate-a-report"></a>產生報告
hello 工具會產生 hello 報表輸出，摘要說明所有 hello 部署建議的啟用巨集的 Microsoft Excel 檔案 （XLSM 檔案）。 hello 報表名稱為 「 DeploymentPlannerReport_ <*唯一數值識別碼*>.xlsm 並放置在 hello 指定目錄。

分析完成後，您可以在報表產生模式中執行 hello 工具。 hello 下表包含在報表產生模式中的強制與選用工具參數 toorun 的清單。

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|參數名稱 | 說明 |
|-|-|
| -Operation | GenerateReport |
| -Server |  hello vCenter/vSphere 伺服器完整網域名稱或 IP 位址 (使用 hello 相同名稱或 IP 位址，您的程式碼剖析 hello 次使用) 位於 hello 要分析之的 Vm 的報表是 toobe 產生。 請注意，是否您的程式碼剖析 hello 次使用的 vCenter 伺服器，您不可使用 vSphere server 報表產生，反之亦然。|
| -VMListFile | 產生 toobe hello 檔案，其中包含相關分析 hello 報表的 Vm 的 hello 份。 hello 檔案路徑可以是絕對或相對的。 hello 檔案應包含一個 VM 名稱或 IP 位址，每行。 hello hello 檔案中指定的 VM 名稱應該 hello 與 hello hello vCenter 伺服器 /vsphere ESXi 主機和功能已在分析期間使用的相符項目上的 VM 名稱相同。|
| -Directory | （選擇性） hello UNC 或本機目錄路徑 hello 要分析之資料 （程式碼剖析期間所產生的檔案） 儲存。 這項資料，才能產生 hello 報表。 如未指定，將會使用 ‘ProfiledData’ 目錄。 |
| -GoalToCompleteIR | （選擇性） hello 數小時中的 hello hello 的初始複寫分析 Vm 需要 toobe 完成。 產生的 hello 報表會提供 hello Vm 的初始複寫的時間即可完成 hello 指定數目的時間。 hello 預設值為 72 小時。 |
| -User | （選擇性） hello 名稱 toouse tooconnect toohello vCenter/vSphere 伺服器的使用者。 hello 名稱是 hello 的使用的 toofetch hello 最新組態資訊 Vm，例如 hello 磁碟數目、 核心數目，以及 toouse hello 報表中的 Nic 數目。 如果未提供 hello 名稱，會使用收集程式碼剖析開始的 hello hello 開頭處的 hello 組態資訊。 |
| -Password | （選擇性） hello 密碼 toouse tooconnect toohello vCenter 伺服器 /vsphere ESXi 主機。 如果未指定 hello 密碼，做為參數，您會提示，稍後執行 hello 命令時。 |
| -DesiredRPO | （選擇性） hello 所需要的復原點目標，以分鐘為單位。 hello 預設值為 15 分鐘。|
| -Bandwidth | 頻寬 (以 Mbps 為單位)。 hello 參數 toouse toocalculate hello hello 可達成的 RPO 指定頻寬。 |
| -StartDate | （選擇性） hello 公釐開始日期和時間-DD-YYYY:HH:MM （24 小時制）。 StartDate 必須與 EndDate 一起指定。 指定開始日期時，會產生 hello 報告收集 StartDate 與 EndDate 之間的 hello 分析資料。 |
| -EndDate | （選擇性） hello 結束日期和時間格式 MM-DD-YYYY:HH:MM （24 小時制）。 EndDate 必須與 StartDate 一起指定。 當指定 EndDate 時，會產生 hello 報告收集 StartDate 與 EndDate 之間的 hello 分析資料。 |
| -GrowthFactor | （選擇性） hello 成長係數，以百分比表示。 hello 預設值為 30%。 |
| -UseManagedDisks | (選擇性) UseManagedDisks - 是/否。 預設值為 [是]。 請考慮是否在受管理的磁碟，而不是未受管理的磁碟上完成測試容錯移轉/容錯移轉的虛擬機器計算 hello 可以放入單一儲存體帳戶的虛擬機器數目。 |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>範例 1: Hello 本機磁碟機上 hello 分析資料時，產生報表，以使用預設值
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>範例 2： 遠端伺服器上 hello 分析資料時，產生一份報表
您應該對 hello 遠端目錄讀取/寫入存取。
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>範例 3： 指定的時間內產生與特定的頻寬和以目標為 toocomplete IR 報表
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>範例 4： 產生報告以 5%的成長因數，而不是 hello 預設值 30%
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>範例 5︰使用剖析資料子集來產生報告
例如，您會有 30 天的已分析資料，而且只 20 天想 toogenerate 報表。
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>範例 6：針對 5 分鐘 RPO 產生報告
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>用於 hello 計算百分位數值
**產生報表時，將沒有 hello 工具使用程式碼剖析期間，收集哪些預設百分位數值 hello 效能度量？**

hello 工具的預設值 toohello 第 95 個百分位數的值讀取/寫入 IOPS，寫入 IOPS 和所有 hello Vm 的程式碼剖析期間所收集的資料變換。 這項標準可確保該 hello 第 100 個百分位數突然增加您的 Vm 可能會看到因為暫存的事件是未使用的 toodetermine 目標儲存體帳戶和來源頻寬需求。 例如，暫存事件可能是一天執行一次的備份作業、定期資料庫檢索或分析報告產生活動，或其他類似的短期時間點事件。

Azure 上執行 hello 工作負載時，使用第 95 個百分位數的值，則為 true 的圖片是真實的工作負載特性，它可讓您提供 hello 達到最佳效能。 我們不打算將需要 toochange 這個數字。 如果您變更 hello 值 （toohello 90th 百分位數，例如），您可以更新 hello 設定檔*ASRDeploymentPlanner.exe.config*在 hello 預設資料夾，並儲存在 hello 現有程式碼剖析 toogenerate 新報表資料。
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>成長因子考量
**規劃部署時為何應考量成長因子？**

在您的工作負載特性，假設一段時間可能增加的使用量中成長的重大 tooaccount 它。 保護的位置，如果您的工作負載特性變更之後，您無法切換保護 tooa 不同的儲存體帳戶而不需要停用並重新啟用保護，hello。

例如，假設您的 VM 位於置於標準儲存體複寫帳戶中。 Hello 未來三個月，幾項變更是可能 toooccur:

* hello hello VM 執行的 hello 應用程式的使用者數目會增加。
* hello 產生更高的變換 hello VM 上將需要 hello VM toogo toopremium 儲存體，以便可以跟 Site Recovery 的複寫。
* 因此，您會有 toodisable，並重新啟用保護 tooa 進階儲存體帳戶。

我們強烈建議您計劃在部署計劃期間，而 hello 預設值是 30%的成長。 您 hello 專家對您應用程式使用模式和成長預測，而且您可以變更這個編號，據以產生報表期間。 此外，您可以產生多個報表與 hello 與各種成長因數相同，程式碼剖析資料且判斷哪些目標儲存體和來源頻寬的建議最適合您。

hello 產生 Microsoft Excel 報表包含下列資訊的 hello:

* [輸入](site-recovery-deployment-planner.md#input)
* [建議](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [建議頻寬輸入](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM<->儲存體放置](site-recovery-deployment-planner.md#vm-storage-placement)
* [相容的 VM](site-recovery-deployment-planner.md#compatible-vms)
* [不相容的 VM](site-recovery-deployment-planner.md#incompatible-vms)

![Deployment Planner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>取得輸送量

Site Recovery 在複寫期間，在 GetThroughput 模式中執行 hello 工具，可以達到從內部部署 tooAzure tooestimate hello 輸送量。 hello 工具會計算 hello 輸送量從 hello hello 工具的伺服器上執行。 在理想情況下，此伺服器根據 hello 設定伺服器調整大小指南 >。 如果您已部署 Site Recovery 基礎結構元件在內部，執行 hello 工具 hello 組態伺服器上。

開啟命令列主控台中，並移 toohello 站台復原 」 部署計劃工具的資料夾。 使用下列參數執行 ASRDeploymentPlanner.exe。

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|參數名稱 | 說明 |
|-|-|
| -Operation | GetThroughput |
| -Directory | （選擇性） hello UNC 或本機目錄路徑 hello 要分析之資料 （程式碼剖析期間所產生的檔案） 儲存。 這項資料，才能產生 hello 報表。 如未指定目錄，則會使用 ‘ProfiledData’ 目錄。 |
| -StorageAccountName | 用於複寫的資料從內部部署 tooAzure toofind hello 頻寬用量的 hello 儲存體帳戶名稱。 hello 工具上傳測試資料 toothis 儲存體帳戶 toofind hello 所使用的頻寬。 |
| -StorageAccountKey | 已使用 tooaccess hello 儲存體帳戶的 hello 儲存體帳戶金鑰。 前往 Azure 入口網站 toohello > 儲存體帳戶 ><*儲存體帳戶名稱*>> 設定 > 存取金鑰 > Key1 （或傳統的儲存體帳戶的主要存取金鑰）。 |
| -VMListFile | hello 包含分析所使用的計算 hello 頻寬的 Vm toobe hello 清單的檔案。 hello 檔案路徑可以是絕對或相對的。 hello 檔案應包含一個 VM 名稱 /IP 位址，每行。 hello hello 檔案中指定的 VM 名稱應該 hello 與 hello hello vCenter 伺服器 /vsphere ESXi 主機上的 VM 名稱相同。<br>例如，hello 檔案 VMList.txt 包含下列 Vm hello:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (選擇性) 這是您的目標 Azure 儲存體帳戶環境。 可以是下列三個值之一 - AzureCloud、AzureUSGovernment、AzureChinaCloud。 預設值為 AzureCloud。 您的目標 Azure 區域為 Azure 美國政府或 Azure China 雲端時，請使用 hello 參數。 |

hello 工具會建立數個 64 MB asrvhdfile <> #.vhd 檔案 （其中"#"是檔案的 hello 數目） hello 指定的目錄。 hello 工具上傳 hello 檔案 toohello 儲存體帳戶 toofind hello 輸送量。 Hello 輸送量的測量之後，hello 工具從 hello 儲存體帳戶和 hello 本機伺服器，就會刪除所有 hello 檔案。 如果它計算產能時，即會終止因故 hello 工具，它並不會刪除 hello 檔案從 hello 儲存體或 hello 本機伺服器。 您必須 toodelete 它們以手動方式。

hello 輸送量來測量在指定的時間點的時間，而且它是在複寫期間，一種站台復原的 hello 最大輸送量前提是所有其他因素仍 hello 相同。 例如，如果任何應用程式啟動時耗用更多的頻寬，在複寫期間而異的相同網路，hello 實際輸送量 hello。 如果您正在從組態伺服器 hello GetThroughput 命令，hello 工具不會察覺任何受保護的 Vm 和進行中的複寫。 hello 的 hello 測量結果是輸送量的不同 hello GetThroughput hello 受保護的 Vm 時執行作業有高資料變換。 我們建議您執行 hello 工具在不同時間點分析 toounderstand 期間的時間層級可以在不同時間達到何種輸送量。 Hello 報表中 hello 工具會顯示 hello 最後一個測量的輸送量。

### <a name="example"></a>範例
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> 在具有 hello 的伺服器上執行 hello 工具相同的儲存體和 hello 組態伺服器的 CPU 特性。
>
> 對於複寫，設定 hello 建議的頻寬 toomeet hello RPO 100%的 hello 時間。 如果您沒有看見 hello 工具回報的 hello 達成輸送量增加，設定 hello 右頻寬之後，請勿 hello 遵循：
>
>  1. 是否有任何網路服務品質 (QoS)，會限制站台復原輸送量，請檢查 toodetermine。
>
>  2. 您的站台復原保存庫是否在最近的實體上支援的 Microsoft Azure 區域 toominimize 網路延遲的 hello，請檢查 toodetermine。
>
>  3. 請檢查您的本機儲存體特性 toodetermine，是否可以提升 hello 硬體 (例如，HDD tooSSD)。
>
>  4. 變更在 hello 處理序伺服器 hello Site Recovery 設定太[增加複寫所用的網路頻寬的 hello 量](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth)。

## <a name="recommendations-with-desired-rpo-as-input"></a>建議以所需的 RPO 做為輸入

### <a name="profiled-data"></a>剖析的資料

![hello 部署計劃中的 hello 分析資料檢視](./media/site-recovery-deployment-planner/profiled-data-period.png)

**已分析的資料期間**: hello 期間哪些 hello 期間執行程式碼剖析。 根據預設，hello 工具包含所有已分析的資料在 hello 計算中，除非 hello 報表針對特定期間所產生在報表產生期間使用 StartDate 和 EndDate 的選項。

**伺服器名稱**: hello 名稱或 IP 位址 hello VMware vCenter 或 ESXi 主機會產生其 Vm 的報表。

**預期 RPO**: hello 的復原點目標，為您的部署。 根據預設，hello 所需的網路頻寬計算 15、 30 到 60 分鐘的 RPO 值。 根據 hello 選取，受影響的 hello 值更新 hello 張紙上。 如果您已經使用 hello *DesiredRPOinMin*時產生的值都會顯示 hello 預期 RPO 結果中的 hello 報表的參數。

### <a name="profiling-overview"></a>剖析概觀

![Hello 部署計劃中的分析結果](./media/site-recovery-deployment-planner/profiling-overview.png)

**程式碼剖析虛擬機器的總**: hello 其已分析的資料可供使用的 Vm 數目總計。 如果 hello VMListFile 不經過分析的所有 Vm 的名稱，這些 Vm 不會視為在 hello 報表產生並排除在 hello 分析 Vm 總數。

**相容的虛擬機器**: hello 可能是受保護的 tooAzure 使用站台復原中 Vm 數目。 它是 hello 相容的 hello 所需的網路頻寬、 儲存體帳戶數目、 Azure 的核心數目和組態伺服器與其他處理序伺服器的數目計算的 Vm 數目總計。 hello 」 相容的 Vm 」 一節中有 hello 詳細資料的每個相容的 VM。

**不相容的虛擬機器**: hello 分析不相容的 Site recovery 保護的 Vm 數目。 不相容的 hello 原因會記載 hello"不相容的 Vm 」 一節。 如果 hello VMListFile 不經過分析的所有 Vm 的名稱，這些 Vm 會排除 hello 不相容的 Vm 計數。 這些 Vm 列在 「 資料找不到"hello"不相容的 Vm 」 一節的 hello 結尾處。

**所需 RPO**：以分鐘為單位的所需復原點目標。 hello 報表會產生三個的 RPO 值： 15 （預設）、 30 到 60 分鐘。 依據 hello 工作表在 hello 右上方的 hello 預期 RPO 下拉式清單中選取範圍變更 hello 報表中的 hello 頻寬建議。 如果您使用 hello 產生 hello 報表*-DesiredRPO*參數以自訂值，這個自訂的值將會顯示為 hello hello 預期 RPO 下拉式清單中的預設值。

### <a name="required-network-bandwidth-mbps"></a>所需的網路頻寬 (Mbps)

![Hello 部署計劃中的所需的網路頻寬](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100%的 hello 時間：** hello 建議 Mbps toobe 的頻寬配置 toomeet 您想要的 RPO 100%的 hello 時間。 這個數量的頻寬必須專供程式相容的 Vm tooavoid 的穩定狀態差異複寫任何 RPO 違規。

**toomeet RPO hello 時間的 90%**： 因為寬頻定價或其他原因，如果您不能設定 hello 所需的頻寬 toomeet 您想要的 RPO 100%的 hello 時間，您可以選擇 toogo 擁有較低的頻寬設定，可滿足您所需的 RPO hello 時間的 90%。 設定此較低頻寬的 toounderstand hello 顧慮，hello 報表會提供假設分析 hello 數目和 RPO 違規 tooexpect 持續時間。

**達到的輸送量：** hello 輸送量從 hello 執行的伺服器上您擁有 hello GetThroughput 命令 toohello Microsoft Azure 地區 hello 儲存體帳戶所在的位置。 這個輸送量數字表示，可讓您保護使用 Site Recovery，前提是您設定伺服器或處理序伺服器儲存體和網路特性保持相容 Vm 相同的 hello 的 hello 時的估計 hello 層級您已從中執行 hello 工具 hello 伺服器。

複寫，您應該設定 hello 建議的頻寬 toomeet hello RPO 100%的 hello 時間。 如果您沒有看到任何 hello 達成輸送量增加，hello 工具所報告，您會設定 hello 頻寬後，執行下列 hello:

1. 是否有任何網路服務品質 (QoS)，會限制站台復原輸送量，請檢查 toosee。

2. 您的站台復原保存庫是否在最近的實體上支援的 Microsoft Azure 區域 toominimize 網路延遲的 hello，請檢查 toosee。

3. 請檢查您的本機儲存體特性 toodetermine，是否可以提升 hello 硬體 (例如，HDD tooSSD)。

4. 變更在 hello 處理序伺服器 hello Site Recovery 設定太[增加 hello 數量的網路頻寬用於複寫](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth)。

如果您執行 hello 工具設定伺服器或已有受保護 Vm 的處理序伺服器上，執行幾次 hello 工具。 hello 達成輸送量數字有所不同 hello 變換正在處理中該時間點的時間量。

對於所有企業 Site Recovery 部署，建議使用 [ExpressRoute](https://aka.ms/expressroute)。

### <a name="required-storage-accounts"></a>所需的儲存體帳戶
下列圖表顯示 hello 總數的儲存體帳戶 （standard 和 premium） 的所有必要的 tooprotect hello hello 相容的 Vm。 toolearn 的儲存體帳戶 toouse 針對每個 VM，請參閱 hello 」 VM 存放位置 」 一節。

![需要儲存體帳戶的 hello 部署規劃](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>所需的 Azure 核心數目
這個結果會是核心 toobe 之前的所有容錯移轉或測試容錯移轉 hello 相容的 Vm 設定的 hello 總數。 站台復原太少核心 hello 訂用帳戶中使用時，失敗時的 hello toocreate Vm 測試容錯移轉或容錯移轉。

![需要的 Azure hello 部署計劃中的核心數目](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>所需的內部部署基礎結構
此圖是 hello 總數的組態伺服器與其他處理序伺服器 toobe 設定碼，就足以 tooprotect 所有 hello 相容的 Vm。 根據支援的 hello[大小 hello 組態伺服器的建議](https://aka.ms/asr-v2a-on-prem-components)，hello 工具可能會建議使用額外的伺服器。 hello 建議的依據 hello 較大的 hello 每天變換或 hello （假設每個 VM 的三個磁碟的平均） 的受保護 Vm 的數目上限，兩者取其較叫用伺服器 hello 組態或 hello 額外的處理序伺服器上的第一個。 Hello 「 輸入 」 一節中找到每個日期和受保護的磁碟總數變換總計的 hello 詳細的資料。

![需要在內部部署基礎結構在 hello 部署規劃](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>假設分析
這項分析會概述多少違規期間可能發生程式碼剖析的期間，當您設定的 hello 低頻寬的所需的 hello RPO toobe 符合只 hello 時間的 90%。 任何指定的日期都可能發生一或多個 RPO 違規。 hello 圖形會顯示 hello 尖峰 hello 一天的 RPO。
根據這項分析，您可以決定 hello hello 所有天和尖峰 RPO 達到每日之間的 RPO 違規數目是否與可接受指定較低的頻寬。 如果是可接受的您可以配置複寫的 hello 較低的頻寬，否則配置 hello 較高的頻寬，只要建議的 toomeet hello RPO 100%的 hello 時間。

![Hello 部署規劃的假設分析](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>初始複寫的建議 VM 批次大小
在本節中，我們建議 hello 可以受到平行 toocomplete hello 初始複寫以 hello 72 個小時內的 Vm 數目建議頻寬 toomeet 預期 RPO 100%的 hello 時間設定。 此值是可設定的值。 toochange 它在產生報告時，使用 hello *GoalToCompleteIR*參數。

hello 圖形這裡會顯示一個範圍的頻寬值和導出的 VM 批次大小計數 toocomplete 初始複寫在 72 小時內，根據 hello 平均偵測到的 VM 大小，在所有 hello 相容的 Vm。

Hello 公開預覽，在 hello 報表未指定哪些 Vm 應該包含在批次。 您可以使用每個 VM 大小所示 hello"相容 Vm 」 一節 toofind hello 磁碟大小，並選取其供批次，或者您可以選取 hello Vm 根據已知的工作負載特性。 hello 的 hello 初始複寫變更的完成時間按比例，根據 hello 實際 VM 磁碟大小，使用磁碟空間和可用的網路輸送量。

![建議的 VM 批次大小](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>使用的成長因子和百分位數值
本節中的 hello hello 底部表用於分析的 hello Vm （預設為第 95 個百分位數） 的所有 hello 效能計數器顯示 hello 百分位數值及 hello 成長係數 （預設值為 30%），都用於所有 hello 計算。

![使用的成長因子和百分位數值](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>以可用頻寬做為輸入的建議

![以可用頻寬做為輸入的建議](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

您可能會遇到一下情況：您知道無法針對 Site Recovery 複寫設定超過 x Mbps 的頻寬。 hello 工具可讓您 tooinput 可用的頻寬 (使用 hello-頻寬參數在報表產生期間)，以及如何取得 hello 可達成的 RPO，以分鐘為單位。 您可以使用這個可達成的 RPO 值，決定是否需要額外的頻寬設定 tooset 或您是使用擁有具有此 RPO 為災害復原方案的 [確定]。

![500 Mbps 頻寬可達成的 RPO](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>輸入
hello 輸入工作表會提供程式碼剖析的 VMware 環境的 hello 概觀。

![程式碼剖析的 VMware 環境的 hello 概觀](./media/site-recovery-deployment-planner/Input.png)

**開始日期**和**結束日期**: hello hello 程式碼剖析資料視為產生報告的開始和結束日期。 根據預設，hello 開始日期是 hello 程式碼剖析開始的日期，且 hello 結束日期 hello 分析停止的日期。 如果 hello 報表就會產生含有這些參數，這可以是 hello 'StartDate' 和 'EndDate' 值。

**程式碼剖析天總數**: hello 總天數的程式碼剖析 hello 之間開始和結束的日期的 hello 產生報告。

**相容的虛擬機器數目**: hello Vm 數目總計相容的 hello 所需的網路頻寬，所需的數目的儲存體帳戶，Microsoft Azure 核心設定伺服器和額外的處理序伺服器計算。

**所有相容的虛擬機器的磁碟總數**： 用來做為其中一個 hello hello 號碼輸入 toodecide hello 組態伺服器數目和額外的處理序伺服器 toobe hello 部署中使用。

**每個相容的虛擬機器磁碟的平均數目**: hello 平均計算不限數目的磁碟相容的所有 Vm 之間。

**平均磁碟大小 (GB)**： 計算所有相容的 Vm 之間的 hello 平均磁碟大小。

**預期 RPO （分鐘）**： 是 hello 預設復原點目標值或 hello 值 hello 'DesiredRPO' 參數傳遞時的所需的報表產生 tooestimate hello 頻寬。

**所需的頻寬 (Mbps)**: hello 您在報表產生 tooestimate hello 時間傳送 hello '頻寬' 參數的值達到 RPO。

**觀察到的一般資料變換每日 (GB)**: hello 平均資料變換觀察到所有程式碼剖析天之間。 此編號用做為其中一個 hello 輸入 toodecide hello 組態伺服器數目和額外的處理序伺服器 toobe hello 部署中使用。


## <a name="vm-storage-placement"></a>VM 儲存體放置

![VM 儲存體放置](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**磁碟儲存體類型**： 其中一個標準或進階儲存體帳戶，也就是所有 hello 對應 hello 中所述的 Vm 使用的 tooreplicate **Vm tooPlace**資料行。

**建議的前置詞**: hello 建議三個字元前置詞，可以用來命名 hello 儲存體帳戶。 您可以使用您自己的前置詞，但是 hello 工具的建議遵循 hello[分割儲存體帳戶的命名慣例](https://aka.ms/storage-performance-checklist)。

**建議的帳戶名稱**: hello 儲存體帳戶名稱之後包含 hello 建議前置詞。 取代 hello 名稱 hello 角括號內 （< 和 >） 與您自訂的輸入。

**記錄儲存體帳戶**： 所有 hello 複寫記錄檔會都儲存在標準儲存體帳戶。 對於複寫 tooa 進階儲存體帳戶的 Vm，設定記錄檔儲存體的額外標準儲存體帳戶。 多個進階複寫儲存體帳戶可以使用單一標準記錄儲存體帳戶。 為複寫的 toostandard 儲存體帳戶使用的 Vm hello 的記錄檔的相同儲存體帳戶。

**建議的記錄檔的帳戶名稱**： 儲存體記錄的帳戶有名稱之後包含 hello 建議前置詞。 取代 hello 名稱 hello 角括號內 （< 和 >） 與您自訂的輸入。

**放置摘要**: hello 摘要時的複寫 hello 總計 hello 儲存體帳戶上的 Vm 的負載，並測試容錯移轉或容錯移轉。 它包含 Vm 對應的 toohello 儲存體帳戶總讀取/寫入 （複寫） IOPS，總設定大小，在所有磁碟和磁碟的總數目，撰寫跨所有的 Vm 放在這個儲存體帳戶總 IOPS hello 的總數。

**虛擬機器 tooPlace**： 一份所有 hello 應放在 hello 提供最佳效能和使用的儲存體帳戶的 Vm。

## <a name="compatible-vms"></a>相容的 VM
![相容 VM 的 Excel 試算表](./media/site-recovery-deployment-planner/compatible-vms.png)

**VM 名稱**: hello VM 名稱或 IP 位址，就會產生報告時用於 hello VMListFile。 此資料行也會列出附加的 toohello vm 的 hello 磁碟 (Vmdk)。 toodistinguish vCenter Vm 具有重複的名稱或 IP 位址，hello 名稱包含 hello ESXi 主機名稱。 hello 列出的 ESXi 主機是一個 hello hello VM 已放置在程式碼剖析期間的 hello 期間發現 hello 工具時。

**VM 相容性**：值為 [是] 和 [是\*]。 **[是]** \*適用於執行個體中的 hello VM 適合[Azure 高階儲存體](https://aka.ms/premium-storage-workload)。 在這裡，hello 分析高變換或 IOPS 磁碟納入 hello P20 或 P30 類別，但是 hello hello 磁碟大小會導致它 toobe 向 tooa P10 或 P20 下對應。 hello 儲存體帳戶會決定哪些 premium 儲存體磁碟輸入 toomap 磁碟，請以根據其大小。 例如：
* <128 GB 為 P10。
* 128 GB too512 GB 是 P20。
* 512 GB too1024 GB 是 P30。
* 1025 GB too2048 GB 是 P40。
* 2049 是 P50 GB too4095 GB。

如果 hello 工作負載特性的磁碟將其放在 hello P20 或 P30 類別，但 hello 大小將它對應向 tooa 低 premium 儲存體磁碟類型，hello 工具會將標示為該 VM**是**\*。 hello 工具也建議您將變更 hello 來源磁碟大小 toofit hello 建議使用 premium 儲存體磁碟類型，或變更 hello 目標磁碟型容錯移轉後的。

**儲存體類型**：標準或進階。

**建議的前置詞**: hello 三個字元的儲存體帳戶的前置詞。

**儲存體帳戶**: hello 名稱使用 hello 建議的儲存體帳戶的前置詞。

**R/W IOPS （與成長係數）**: hello 尖峰工作負載讀取/寫入 IOPS hello 磁碟上 （預設為第 95 個百分位數），包括 hello 未來成長係數 （預設值為 30%）。 請注意，hello 總讀取/寫入 IOPS 的 VM 不一定 hello hello VM 的個別磁碟的讀取/寫入 IOPS 總數，因為 hello 尖峰讀取/寫入 IOPS 的 hello VM hello 尖峰其個別磁碟 hello 總和的讀取/寫入 IOPS hello 的每一分鐘期間程式碼剖析期間。

**在 Mbps （含成長因數） 中的資料變換量**: hello 磁碟上的 hello 尖峰變換率 （預設為第 95 個百分位數），包括 hello 未來成長係數 （預設值為 30%）。 請注意該 hello hello VM 的總資料變換不一定 hello 總和 hello VM 的個別磁碟的資料變換量，因為 hello 尖峰資料變換量的 hello VM hello 總和的個別磁碟的變換的 hello 尖峰期間的程式碼剖析期間的 hello 每隔一分鐘。

**Azure VM 大小**: hello 理想對應 Azure 雲端服務的虛擬機器大小，這在內部部署 VM。 hello 對應根據 hello 在內部部署 VM 的記憶體、 磁碟/核心/Nic 和讀取/寫入 IOPS 數目。 hello 建議一律是 hello 最低 Azure VM 大小符合所有的 hello 在內部部署 VM 的特性。

**磁碟數目**: hello hello VM 上的虛擬機器磁碟 (Vmdk) 的總數。

**磁碟大小 (GB)**: hello hello VM 的所有磁碟大小總計的安裝程式。 hello 工具也會顯示 hello VM 中的 hello hello 個別磁碟的磁碟大小。

**核心**: hello 的 CPU 核心數目 hello VM 上。

**記憶體 (MB)**: hello RAM hello VM 上的。

**Nic**: hello hello VM 上的 Nic 數目。

**開機類型**： 它是 hello VM 的啟動類型。 可以是 BIOS 或 EFI。 Azure Site Recovery 目前僅支援 BIOS 開機類型。 不相容的 Vm 工作表會列出所有 hello 虛擬機器的 EFI 開機型別。

**OS 類型**: hello 是 hello VM 的 OS 類型。 可以是 Windows 或 Linux 或其他。

## <a name="incompatible-vms"></a>不相容的 VM

![不相容 VM 的 Excel 試算表](./media/site-recovery-deployment-planner/incompatible-vms.png)

**VM 名稱**: hello VM 名稱或 IP 位址，就會產生報告時用於 hello VMListFile。 此資料行也會列出附加的 toohello vm 的 hello Vmdk。 toodistinguish vCenter Vm 具有重複的名稱或 IP 位址，hello 名稱包含 hello ESXi 主機名稱。 hello 列出的 ESXi 主機是一個 hello hello VM 已放置在程式碼剖析期間的 hello 期間發現 hello 工具時。

**VM 的相容性**： 表示指定 VM 的 hello 為何使用站台復原與不相容。 hello 原因所述，對每個不相容的 hello VM 的磁碟，以在發行[儲存體限制](https://aka.ms/azure-storage-scalbility-performance)，可以是 hello 下列任何一項：

* 磁碟大小 >4095 GB。 Azure 儲存體目前不支援大於 4095 GB 的資料磁碟大小。
* OS 磁碟 >2048 GB。 Azure 儲存體目前不支援大於 2048 GB 的 OS 磁碟大小。
* 啟動類型為 EFI。 Azure Site Recovery 目前僅支援 BIOS 開機類型虛擬機器。

* VM 的總大小 （複寫 + TFO） 超過支援的 hello 儲存體帳戶大小限制 (35 TB)。 Hello VM 中的單一磁碟具有超過 hello 支援的 Azure 或站台復原的上限標準儲存體的效能特性時，通常會發生此不相容。 這種情況下會將 hello VM 推入 hello premium 儲存體區域。 不過，最大支援的進階儲存體帳戶的大小是 35 TB，而且單一受保護 VM 的 hello 無法保護跨多個儲存體帳戶。 也請注意，受保護的 VM 上執行測試容錯移轉時，它會執行 hello 中相同的儲存體帳戶複寫所在的進度。 在本例中，設定 2 x hello 複寫 tooprogress hello 磁碟大小及測試容錯移轉 toosucceed 以平行方式。
* 來源 IOPS 超過支援的儲存體 IOPS 限制 (每個磁碟 5000)。
* 來源 IOPS 超過支援的儲存體 IOPS 限制 (每個 VM 80,000)。
* 平均資料變換量超過支援站台復原資料變換限制 hello 磁碟的平均 I/O 大小為 10 MBps。
* 在 hello VM 上的所有磁碟的總資料變換量超過 hello 最大支援站台復原資料變換限制為每個 VM 的 54 MBps。
* 平均有效寫入 IOPS 超過磁碟 840 hello 支援站台復原 IOPS 限制。
* 導出的快照集儲存超過 10 TB hello 支援快照集儲存體限制。

**R/W IOPS （與成長係數）**: hello 尖峰工作負載 IOPS hello 磁碟上的 （預設為第 95 個百分位數），包括 hello 未來成長係數 （預設值為 30%）。 請注意，hello 總讀取/寫入 IOPS 的 hello VM 不一定 hello hello VM 的個別磁碟的讀取/寫入 IOPS 總數，因為 hello 尖峰讀取/寫入 IOPS 的 hello VM 是其個別磁碟 hello 總和的 hello 尖峰讀取/寫入 IOPS 的 hello 每隔一分鐘期間程式碼剖析期間。

**在 Mbps （含成長因數） 中的資料變換量**: hello 尖峰變換速率，包括 hello 未來成長係數 （預設值 30%) 的 hello 磁碟 （預設值第 95 個百分位數）。 請注意該 hello hello VM 的總資料變換不一定 hello 總和 hello VM 的個別磁碟的資料變換量，因為 hello 尖峰資料變換量的 hello VM hello 總和的個別磁碟的變換的 hello 尖峰期間的程式碼剖析期間的 hello 每隔一分鐘。

**磁碟數目**: hello 總數 Vmdk hello VM 上的。

**磁碟大小 (GB)**: hello hello VM 的所有磁碟大小總計的安裝程式。 hello 工具也會顯示 hello VM 中的 hello hello 個別磁碟的磁碟大小。

**核心**: hello 的 CPU 核心數目 hello VM 上。

**記憶體 (MB)**: hello 上 RAM 容量的 hello VM。

**Nic**: hello hello VM 上的 Nic 數目。

**開機類型**： 它是 hello VM 的啟動類型。 可以是 BIOS 或 EFI。 Azure Site Recovery 目前僅支援 BIOS 開機類型。 不相容的 Vm 工作表會列出所有 hello 虛擬機器的 EFI 開機型別。

**OS 類型**: hello 是 hello VM 的 OS 類型。 可以是 Windows 或 Linux 或其他。


## <a name="site-recovery-limits"></a>Site Recovery 限制

**複寫儲存體目標** | **平均來源磁碟 I/O 大小** |**平均來源磁碟資料變換** | **每日的來源磁碟資料變換總計**
---|---|---|---
標準儲存體 | 8 KB | 2 MBps | 每個磁碟 168 GB
進階 P10 磁碟 | 8 KB | 2 MBps | 每個磁碟 168 GB
進階 P10 磁碟 | 16 KB | 4 MBps | 每個磁碟 336 GB
進階 P10 磁碟 | 32 KB 或更大 | 8 MBps | 每個磁碟 672 GB
進階 P20 或 P30 磁碟 | 8 KB  | 5 MBps | 每個磁碟 421 GB
進階 P20 或 P30 磁碟 | 16 KB 或更大 |10 MBps | 每個磁碟 842 GB

以上是採用 30% I/O 重疊時的平均數字。 Site Recovery 能夠處理更高的輸送量 (以重疊比為基礎)、較大的寫入大小和實際工作負載 I/O 行為。 hello 的數字之前假設大約五分鐘一般待辦項目。 也就是說，資料上傳之後，便會進行處理並在五分鐘內建立復原點。

上述限制是以我們的測試為基礎，但無法涵蓋所有可能的應用程式 I/O 組合。 實際的結果會隨著您的應用程式 I/O 混合而有所不同。 為獲得最佳結果，即使部署計畫之後，一定建議您執行測試所使用的測試容錯移轉 tooget hello true 效能圖片廣泛的應用程式。

## <a name="updating-hello-deployment-planner"></a>更新 hello 部署規劃
tooupdate hello 部署規劃中，執行下列 hello:

1. 下載 hello 最新版 hello [Azure Site Recovery 部署規劃](https://aka.ms/asr-deployment-planner)。

2. 複製 hello.zip 資料夾 tooa 伺服器要 toorun 其上。

3. 擷取 hello.zip 資料夾。

4. 執行 hello 下列其中一項：
 * 如果 hello 最新版本未包含的程式碼剖析的修正程式碼剖析已在您目前版本的 hello 計劃的進度，繼續執行程式碼剖析 hello。
 * 如果 hello 最新版本所包含的程式碼剖析的修正，我們建議您停止您目前的版本上的分析，並重新啟動 hello 分析 hello 新版本。

  >[!NOTE]
  >
  >當您開始分析 hello 新版本，傳遞 hello 相同的輸出目錄路徑，以便 hello 工具設定檔將資料附加上 hello 現有的檔案。 一組完整的分析的資料將會使用 toogenerate hello 報表。 如果沒有傳遞不同的輸出目錄中，建立新的檔案，且舊程式碼剖析資料並非 toogenerate hello 報表。
  >
  >每個新部署規劃是 hello.zip 檔案的累計更新。 您不需要 toocopy hello 最新檔案 toohello 前一個資料夾。 您可以建立及使用新的資料夾。


## <a name="version-history"></a>版本歷程記錄

### <a name="131"></a>1.3.1
更新日期：2017 年 7 月 19 日

已新增下列新功能︰

* 在報告產生階段新增了大型磁碟 (> 1TB) 的支援。 現在您可以使用部署規劃 tooplan 複寫之虛擬機器的磁碟大小大於 1 TB (最多到 4095 GB)。
深入了解 [Azure Site Recovery 中的大型磁碟支援](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
更新日期：2017 年 5 月 9 日

已新增下列新功能︰

* 在產生報告中新增了受控磁碟支援。 hello 的虛擬機器數目可以放 tooa 單一儲存體帳戶是如果受管理磁碟為基礎的計算已選取的測試容錯移轉/容錯移轉。        


### <a name="12"></a>1.2
更新日期：2017 年 4 月 7 日

已新增下列修正程式︰

* 新增的開機類型 （BIOS 或 EFI） 的核取的每個虛擬機器 toodetermine hello 虛擬機器為 hello 保護的版本不相容或相容。
* 加入的 OS 輸入 hello 相容的 Vm 中的每個虛擬機器的資訊和不相容的 Vm 工作表。
* hello GetThroughput 作業現在支援 hello 美國政府和中國的 Microsoft Azure 地區。
* 已針對 vCenter 和 ESXi 伺服器新增更多必要條件檢查。
* 取得產生錯誤報表的地區設定設定 toonon 英文。


### <a name="11"></a>1.1
更新日期：2017 年 3 月 9 日

固定的 hello 下列問題：

* hello 工具無法設定檔的 Vm，如果 hello vCenter 具有兩個或多個 Vm hello 跨不同的 ESXi 主機相同的名稱或 IP 位址。
* Hello 相容的 Vm 和 Vm 不相容的工作表已停用複製與搜尋。

### <a name="10"></a>1.0
更新日期：2017 年 2 月 23 日

Azure 站台復原部署規劃公用預覽 1.0 具有 hello 下列已知問題 (即將推出的更新中解決 toobe):

* hello 工具只適用於 VMware 到 Azure 的情況下，不會針對 Hyper-v-V-至 Azure 部署。 Hyper-v-V-至 Azure 的情況下，使用 hello [HYPER-V 產能規劃工具](./site-recovery-capacity-planning-for-hyper-v-replication.md)。
* hello GetThroughput 作業不支援 hello 美國政府和中國的 Microsoft Azure 地區。
* hello 工具無法設定檔的 Vm，如果 hello vCenter 伺服器有兩個或多個 Vm hello 跨不同的 ESXi 主機相同的名稱或 IP 位址。 在此版本中，hello 工具會略過重複的 VM 名稱或 IP 位址在 hello VMListFile 中的程式碼剖析。 hello 因應措施是 tooprofile hello Vm 使用 ESXi 主機而非 hello vCenter 伺服器。 您必須為每部 ESXi 主機執行一個執行個體。
