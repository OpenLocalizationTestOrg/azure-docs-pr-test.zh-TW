---
title: "使用的 Azure Data Lake Analytics aaaManage hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toomanage Data Lake Analytics 帳戶的必要項，資料來源、 使用者和工作。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站來管理 Azure Data Lake Analytics
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

了解 toomanage Azure Data Lake Analytics 帳戶、 帳戶資料來源、 使用者和工作使用 hello Azure 入口網站。 toosee 管理主題，需使用其他工具中，按一下 在 hello hello 頁面最上方的索引標籤。

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>管理 Data Lake Analytics 帳戶

### <a name="create-an-account"></a>建立帳戶

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [智慧 + 分析] > [Data Lake Analytics]。
3. 選取下列項目 hello 的值： 
   1. **名稱**: hello hello Data Lake Analytics 帳戶名稱。
   2. **訂用帳戶**: hello hello 帳戶所使用的 Azure 訂用帳戶。
   3. **資源群組**: hello Azure 資源群組中哪個 toocreate hello 帳戶。 
   4. **位置**: hello hello Data Lake Analytics 帳戶的 Azure 資料中心。 
   5. **Data Lake Store**: hello hello Data Lake Analytics 帳戶所使用的預設存放區 toobe。 hello Azure Data Lake Store 帳戶和 hello 資料湖分析帳戶必須在 hello 相同的位置。
4. 按一下 [建立] 。 

### <a name="delete-a-data-lake-analytics-account"></a>刪除 Data Lake Analytics 帳戶

在您刪除 Data Lake Analytics 帳戶前，請先刪除其預設 Data Lake Store 帳戶。

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [刪除] 。
3. 型別 hello 帳戶名稱。
4. 按一下 [刪除] 。

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>管理資料來源

Data Lake Analytics 支援下列資料來源的 hello:

* 資料湖存放區
* Azure 儲存體

您可以使用資料總管 toobrowse 資料來源，以及執行基本的檔案管理作業。 

### <a name="add-a-data-source"></a>建立資料來源

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [資料來源]。
3. 按一下 [ **新增資料來源**]。
    
   * tooadd Data Lake Store 帳戶，您需要 hello 帳戶名稱和存取 toohello 帳戶 toobe 無法 tooquery 它。
   * tooadd Azure Blob 儲存體，您需要 hello 儲存體帳戶和 hello 帳戶金鑰。 toofind 它們，請移 toohello hello 入口網站中的儲存體帳戶。

## <a name="set-up-firewall-rules"></a>設定防火牆規則

您可以使用 Data Lake Analytics toofurther 鎖定存取 tooyour Data Lake Analytics 帳戶在 hello 網路層級。 您可以啟用防火牆、指定 IP 位址或為受信任的用戶端定義 IP 位址範圍。 啟用這些量值之後，只有具有 hello hello 定義範圍內的 IP 位址的用戶端可以連接到 toohello 存放區。

如果其他 Azure 服務，例如 Azure Data Factory 或 Vm，toohello Data Lake Analytics 帳戶的連接，請確定**允許 Azure 服務**開啟**上**。 

### <a name="set-up-a-firewall-rule"></a>設定防火牆規則

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 在左側 hello hello 功能表上，按一下**防火牆**。

## <a name="add-a-new-user"></a>新增使用者

您可以使用 hello**新增使用者精靈**tooeasily 新的資料湖使用者佈建。

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 在 hello 左、 下**入門**，按一下 **新增使用者精靈**。
3. 選取使用者，然後按一下選取。
4. 選取角色，然後按一下選取。 設定新的開發人員 toouse Azure 資料湖選取 hello tooset**資料湖分析開發人員**角色。
5. 選取 hello 存取控制清單 (Acl) 的 hello U SQL 資料庫。 當您對您的選擇感到滿意時，請按一下 [選取]。
6. 選取檔案的 hello Acl。 對於 hello 預設存放區，請不要變更 hello 根資料夾的 hello Acl"/"和 hello/系統資料夾。 按一下 [選取] 。
7. 檢閱您選取的所有變更，然後按一下執行。
8. Hello 精靈完成時，請按一下**完成**。

## <a name="manage-role-based-access-control"></a>管理角色型存取控制

如同其他 Azure 服務，您可以使用角色型存取控制 (RBAC) toocontrol 使用者互動的方式與 hello 服務。

hello 標準 RBAC 角色有下列功能的 hello:
* **擁有者**： 可以將工作提交、 監控工作、 取消工作，從任何使用者，並設定 hello 帳戶。
* **參與者**： 可以將工作提交、 監控工作、 取消工作，從任何使用者，並設定 hello 帳戶。
* **讀取者**：可以監視作業。

使用 hello 資料湖分析開發人員角色 tooenable U-SQL 開發人員 toouse hello 資料湖分析服務。 您可以使用 hello 資料湖分析開發人員角色：
* 提交作業。
* 監視工作狀態和 hello 任何的進度使用者所提交的工作。
* 請參閱 hello U-SQL 指令碼，從任何使用者所提交的作業。
* 只取消您自己的作業。

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>新增使用者或安全性群組 tooa Data Lake Analytics 帳戶

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [存取控制 (IAM)] > [新增]。
3. 選取角色。
4. 新增使用者。
5. 按一下 [確定] 。

>[!NOTE]
>如果使用者或安全性群組需要 toosubmit 工作，他們也需要 hello 存放區帳戶的權限。 如需詳細資訊，請參閱[保護儲存在 Data Lake Store 中的資料](../data-lake-store/data-lake-store-secure-data.md)。
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>管理工作

### <a name="submit-a-job"></a>提交作業

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。

2. 按一下 [ **新增工作**]。 對於每項作業，請設定：

    1. **工作名稱**: hello hello 作業名稱。
    2. **優先順序**：數字越小，優先順序越高。 如果兩個工作會排入佇列，值較低優先順序的 hello 其中一個會執行第一次。
    3. **平行處理原則**: hello 最大數目計算處理 tooreserve 此作業。

3. 按一下 [ **提交作業**]。

### <a name="monitor-jobs"></a>監視工作

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [檢視所有作業]。 顯示所有 hello 帳戶中的 hello 作用中和最近完成工作的清單。
3. （選擇性） 按一下**篩選**toohelp 尋找 hello 工作依**時間範圍**，**工作名稱**，和**作者**值。 

### <a name="monitoring-pipeline-jobs"></a>監視管線作業
屬於管線的作業工作分組，通常就循序 tooaccomplish 特定案例。 例如，您可以有一個管線，來清除、擷取、轉換、彙總客戶深入解析的使用。 識別管線工作提交 hello 作業時，使用 hello 「 管線 」 屬性。 使用 ADF V2 排程的作業會自動填入此屬性。 

tooview U-SQL 工作屬於管線的清單： 

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [作業深入解析]。 [所有工作] 索引標籤將預設，顯示一份執行中、 hello 排入佇列，並結束作業。
3. 按一下 hello**管線作業** 索引標籤。這會顯示管線作業清單，以及每個管線的彙總統計資料。

### <a name="monitoring-recurring-jobs"></a>監視週期性作業
重複執行的作業是指具有 hello 相同的商務邏輯但使用不同的輸入的資料，它一次。 在理想情況下，一定會成功，並有相當穩定的執行時間; 週期性工作監視這些行為有助於確定 hello 作業為狀況良好。 週期性工作，會識別使用 hello"Recurrence"屬性。 使用 ADF V2 排程的作業會自動填入此屬性。

tooview 週期性的 U-SQL 工作清單： 

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [作業深入解析]。 [所有工作] 索引標籤將預設，顯示一份執行中、 hello 排入佇列，並結束作業。
3. 按一下 hello**週期性工作** 索引標籤。這會顯示週期性作業清單，以及每個週期性作業的彙總統計資料。

## <a name="manage-policies"></a>管理原則

### <a name="account-level-policies"></a>帳戶層級原則

這些原則會套用 tooall Data Lake Analytics 帳戶中的工作。

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Data Lake Analytics 帳戶中的 AU 數目上限
原則會控制 hello 分析單位總數 (AUs) 可以使用 Data Lake Analytics 帳戶。 根據預設，設定 too250 hello 值。 比方說，如果此值設定 too250 澳洲，您可以有 250 澳洲指派 tooit，以執行的一項作業或 10 個工作執行與 25 澳洲每個。 送出的其他工作會排入佇列，直到 hello 正在執行的作業。 澳洲正在執行的作業完成時，會釋放給 hello toorun 工作排入佇列。

toochange hello 數目澳洲 Data Lake Analytics 帳戶：

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [內容] 。
3. 在下**最大澳洲**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。 
4. 按一下 [儲存] 。

> [!NOTE]
> 如果您需要多個 hello 預設 （250 個） 澳洲，在 hello 入口網站中，按一下 **說明 + 支援**toosubmit 支援要求。 可以增加 hello 澳洲 Data Lake Analytics 帳戶中所提供的數目。
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>可以同時執行的作業數目上限
原則會控制多少的工作都可以在 hello 執行相同的時間。 根據預設，這個值會設定 too20。 如果您的 Data Lake Analytics 澳洲可用，新的工作，才排程的 toorun 立即 hello 執行工作的總數目達到 hello 值，這個原則。 當您到達 hello 可以同時執行的作業數目上限時，後續的工作會依優先順序佇列，直到一或多個執行中的工作完成 （取決於 AU 可用性）。

toochange hello 數目可以同時執行的作業：

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [內容] 。
3. 在下**最大數目的執行工作**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。 
4. 按一下 [儲存] 。

> [!NOTE]
> 如果您需要更多超過 hello 預設 (20) 中的工作數目，hello 入口網站中，按一下的 toorun**說明 + 支援**toosubmit 支援要求。 可以增加 hello Data Lake Analytics 帳戶中可以同時執行的作業數目。
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>多久 tookeep 工作中繼資料和資源 
當您的使用者執行 U SQL 作業時，hello 資料湖分析服務會保留所有相關的檔案。 相關的檔案包含 hello U-SQL 指令碼，hello hello U-SQL 指令碼、 已編譯的資源，與統計資料中參考的 DLL 檔案。 hello 檔案位於 hello /system/ 資料夾中的 hello 預設 Azure 資料湖存放區帳戶。 此原則會控制會自動刪除之前要儲存這些資源的時間長度 （hello 預設為 30 天）。 偵錯，以及您將在未來的 hello 重新執行的工作的效能微調，您可以使用這些檔案。

toochange 多久 tookeep 工作中繼資料和資源：

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [內容] 。
3. 在下**天 tooRetain 工作查詢**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。  
4. 按一下 [儲存] 。

### <a name="job-level-policies"></a>作業層級原則
您可以使用工作層級原則，控制 hello 最大澳洲和 hello 個別的使用者 （或特定安全性群組的成員） 可以在他們所提交的工作設定的最高優先順序。 這可讓您控制使用者所造成的 hello 成本。 它也可讓您控制的排程工作的 hello 效果可能會有高優先權上正在執行中的實際執行工作 hello 相同的資料湖分析帳戶。

資料湖分析有兩個您可以在 hello 作業層級設定的原則：

* **AU 限制每個作業**： 使用者只能提交 toothis 數目澳洲正常的作業。 根據預設，這項限制是 hello 與 hello AU 上限 hello 帳戶相同。
* **優先順序**： 使用者只能提交工作的優先權低於或等於 toothis 值。 請注意，數字較高表示優先順序較低。 根據預設，這會設定 too1，這是 hello 高的可能優先權。

每個帳戶都已設定預設原則。 hello 預設原則適用於 tooall 的 hello 帳戶的使用者。 您可以針對特定使用者和群組設定其他原則。 

> [!NOTE]
> 帳戶層級原則和作業層級原則可同時套用。
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>新增特定使用者或群組的原則

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [內容] 。
3. 在下**工作提交限制**，按一下 hello**新增原則** 按鈕。 然後，選取或輸入 hello 下列設定：
    1. **計算原則名稱**： 輸入原則名稱，tooremind 您 hello 目的 hello 原則。
    2. **選取使用者或群組**: hello 使用者或群組，此原則適用於選取。
    3. **設定工作 AU 限制 hello**: hello AU 限制適用於 toohello 選取使用者或群組。
    4. **設定優先順序限制 hello**: hello 優先順序限制適用於 toohello 選取使用者或群組。

4. 按一下 [確定] 。

5. hello 新原則會列在 hello**預設**底下原則資料表**工作提交限制**。 

#### <a name="delete-or-edit-an-existing-policy"></a>刪除或編輯現有原則

1. 在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。
2. 按一下 [內容] 。
3. 在下**工作提交限制**，尋找您想 tooedit 的 hello 原則。
4.  toosee hello**刪除**和**編輯**hello hello 資料表的最右邊資料行中的選項，請按一下**...**.

### <a name="additional-resources-for-job-policies"></a>作業原則的其他資源
* [原則概觀部落格文章](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [帳戶層級原則部落格文章](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [作業層級原則部落格文章](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>後續步驟

* [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [開始使用 Data Lake Analytics 使用 hello Azure 入口網站](data-lake-analytics-get-started-portal.md)
* [使用 Azure PowerShell 管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-powershell.md)

