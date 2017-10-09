---
title: "Azure Machine Learning 的進階分析案例 aaaIdentify |Microsoft 文件"
description: "選取適當 hello 的案例提供執行進階預測分析以 hello 小組資料科學程序。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>在 Azure 機器學習中的進階分析案例
本文概述 hello 各種不同的範例資料來源和目標案例，可以由 hello[小組資料科學程序 (TDSP)](data-science-process-overview.md)。 hello TDSP 小組 toocollaborate 上建置的智慧型應用程式提供系統化的方法。 這裡所呈現的 hello 案例說明可用的選項 hello 資料處理工作流程中的 hello 資料特性、 來源位置，以及在 Azure 中的目標儲存機制而定。

hello**決策樹**的選取適合您的資料和目標的 hello 範例案例會以 hello 最後一節。

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

每個 hello 下列各節提供範例案例。 在每個案例中，都會列出可能的資料科學或進階分析流程，以及支援的 Azure 資源。

> [!NOTE]
> **針對所有 hello 下列案例中，您都需要：**
> <br/>
> 
> * [建立儲存體帳戶](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>案例\#1： 小 toomedium 本機檔案中的表格式資料集
![小型 toomedium 本機檔案][1]

#### <a name="additional-azure-resources-none"></a>其他 Azure 資源：無
1. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
2. 上傳資料集。
3. 建置從上傳的資料集開始的 Azure 機器學習實驗流程。

## <a name="smalllocalprocess"></a>案例\#2： 小 toomedium 的本機檔案需要處理的資料集
![處理小型 toomedium 本機檔案][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)
1. 建立執行 IPython Notebook 的 Azure 虛擬機器。
2. 上傳資料 tooan Azure 儲存體容器。
3. 前置處理和清除 IPython Notebook 中的資料 (從 Azure 儲存體容器存取資料)。
4. 轉換資料 toocleaned，表格形式。
5. 將轉換的資料儲存在 Azure Blob 中。
6. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
7. 讀取 hello 資料從 Azure blob 使用 hello[匯入資料][ import-data]模組。
8. 建置從內嵌的資料集開始的 Azure 機器學習實驗流程。

## <a name="largelocal"></a>案例 \#3：本機檔案的大型資料集，以 Azure Blob 為目標
![大型本機檔案][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)
1. 建立執行 IPython Notebook 的 Azure 虛擬機器。
2. 上傳資料 tooan Azure 儲存體容器。
3. 前置處理和清除 IPython Notebook 中的資料 (從 Azure Blob 存取資料)。
4. 如有需要轉換資料 toocleaned，表格式。
5. 視需要瀏覽資料並建立功能。
6. 擷取中小型資料範例。
7. 在 Azure blob 儲存 hello 取樣資料。
8. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
9. 讀取 hello 資料從 Azure blob 使用 hello[匯入資料][ import-data]模組。
10. 建置從內嵌的資料集開始的 Azure 機器學習實驗流程。

## <a name="smalllocaltodb"></a>案例\#4： 小 toomedium 資料集的目標 Azure 虛擬機器中的 SQL Server 的本機檔案
![在 Azure 中的小型 toomedium 本機檔案 tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)
1. 建立執行 SQL Server + IPython Notebook 的 Azure 虛擬機器。
2. 上傳資料 tooan Azure 儲存體容器。
3. 使用 IPython Notebook 前置處理和清除 Azure 儲存體容器中的資料。
4. 如有需要轉換資料 toocleaned，表格式。
5. 儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。
6. 在 Azure VM 上執行負載資料 tooSQL 伺服器資料庫。
   
   選項 \#1：使用 SQL Server Management Studio。
   
   * 登入 tooSQL Server VM
   * 執行 SQL Server Management Studio。
   * 建立資料庫和目標資料表。
   * 從 VM 本機檔案，使用其中一個 hello 大量匯入方法 tooload hello 資料。
   
   選項 \#2：使用 IPython Notebook – 不建議用於中型和大型資料集
   
   <!-- -->    
   * 使用 ODBC 連接字串 tooaccess SQL Server VM 上。
   * 建立資料庫和目標資料表。
   * 從 VM 本機檔案，使用其中一個 hello 大量匯入方法 tooload hello 資料。
7. 視需要瀏覽資料並建立功能。 請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。 只有附註 hello 必要查詢 toocreate 它們。
8. 若有需要，請決定資料範例大小。
9. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
10. 讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。 貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。
11. 建置從內嵌的資料集開始的 Azure 機器學習實驗流程。

## <a name="largelocaltodb"></a>案例 \#5：本機資料中的大型資料集，目標 Azure VM 中的 SQL Server
![在 Azure 中的大型的本機檔案 tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)
1. 建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。
2. 上傳資料 tooan Azure 儲存體容器。
3. (選擇性) 前置處理和清除資料。
   
   a.  前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料
   
       blobs.
   
   b.  如有需要轉換資料 toocleaned，表格式。
   
   c.  儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。
4. 在 Azure VM 上執行負載資料 tooSQL 伺服器資料庫。
   
   a.  登入 tooSQL Server VM。
   
   b.  如果資料尚未儲存，請從 Azure 下載資料檔案
   
       storage container toolocal-VM folder.
   
   c.  執行 SQL Server Management Studio。
   
   d.  建立資料庫和目標資料表。
   
   e.  使用其中一個 hello 大量匯入方法 tooload hello 資料。
   
   f.  如果需要資料表聯結，來建立索引 tooexpedite 聯結。
   
   > [!NOTE]
   > 大型的資料大小更快載入，建議您建立資料分割的資料表和資料大量匯入 hello 以平行方式。 如需詳細資訊，請參閱[平行資料匯入 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。
   > 
   > 
5. 視需要瀏覽資料並建立功能。 請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。 只有附註 hello 必要查詢 toocreate 它們。
6. 若有需要，請決定資料範例大小。
7. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
8. 讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。 貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。
9. 從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程

## <a name="largedbtodb"></a>案例 \#6：SQL Server 資料庫內部部署中的大型資料集，以 Azure 虛擬機器中的 SQL Server 為目標
![在 Azure 中的大型 SQL 資料庫內部 tooSQL DB][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)
1. 建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。
2. 使用其中一個 hello 資料從 SQL Server toodump 檔案匯出方法 tooexport hello 資料。
   
   > [!NOTE]
   > 如果您決定 toomove hello 內部資料庫，替代 （較快） 方法 toomove hello 完整資料庫 toothe SQL Server 執行個體在 Azure 中的所有資料。 略過 hello 步驟 tooexport 資料、 建立資料庫，以及負載/匯入資料 toohello 目標資料庫，並遵循 hello 替代方法。
   > 
   > 
3. 上傳傾印檔案 tooAzure 儲存體容器。
4. 載入執行 Azure 虛擬機器上的 hello 資料 tooa SQL Server 資料庫。
   
   a.  登入 toohello SQL Server VM。
   
   b.  從 Azure 儲存體容器 toohello 本機 VM 資料夾下載資料檔案。
   
   c.  執行 SQL Server Management Studio。
   
   d.  建立資料庫和目標資料表。
   
   e.  使用其中一個 hello 大量匯入方法 tooload hello 資料。
   
   f.  如果需要資料表聯結，來建立索引 tooexpedite 聯結。
   
   > [!NOTE]
   > 更快載入大型的資料大小，建立資料分割的資料表和 toobulk hello 資料匯入以平行方式。 如需詳細資訊，請參閱[平行資料匯入 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。
   > 
   > 
5. 視需要瀏覽資料並建立功能。 請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。 只有附註 hello 必要查詢 toocreate 它們。
6. 若有需要，請決定資料範例大小。
7. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
8. 讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。 貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。
9. 從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>替代方法 toocopy 完整的資料庫從內部部署 SQL Server tooAzure SQL 資料庫
![Local DB 卸離和附加 tooSQL DB 在 Azure 中][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)
tooreplicate hello 整個 SQL Server 資料庫的 SQL Server VM，您應該複製資料庫從一個位置/伺服器 tooanother，假設該 hello 可以讓資料庫離線暫時。 您在 hello SQL Server Management Studio 物件總管 中，或是使用 hello 對等的 TRANSACT-SQL 命令。

1. 卸離 hello hello 來源位置的資料庫。 如需詳細資訊，請參閱[卸離資料庫](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)。
2. 在 Windows 檔案總管或 Windows 命令提示字元視窗中，複製 hello 卸離資料庫檔案或檔案和記錄檔或 hello Azure 中的 SQL Server VM 上的檔案 toohello 目標位置。
3. 附加複製的 hello 檔案 toohello 目標 SQL Server 執行個體。 如需詳細資訊，請參閱[連結資料庫](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)。

[使用卸離和連結來移動資料庫 (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>案例 \#7：本機檔案中的巨量資料，目標 Azure HDInsight Hadoop 叢集中的 Hive 資料庫
![本機目標 Hive 中的巨量資料][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>其他 Azure 資源：Azure HDInsight Hadoop 叢集和 Azure 虛擬機器 (IPython Notebook 伺服器)
1. 建立執行 IPython Notebook 伺服器的 Azure 虛擬機器。
2. 建立 Azure HDInsight Hadoop 叢集。
3. (選擇性) 前置處理和清除資料。
   
   a.  前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料
   
       blobs.
   
   b.  如有需要轉換資料 toocleaned，表格式。
   
   c.  儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。
4. 上傳所選 hello 步驟 2 中的 hello Hadoop 叢集的資料 toohello 預設容器。
5. 載入 Azure HDInsight Hadoop 叢集中的資料 tooHive 資料庫。
   
   a.  登入 toohello hello Hadoop 叢集前端節點
   
   b.  開啟 hello Hadoop 命令列。
   
   c.  命令所輸入 hello Hive 根目錄`cd %hive_home%\bin`Hadoop 命令列中。
   
   d.  執行 hello Hive 查詢 toocreate 資料庫和資料表，並從 blob 儲存體 tooHive 資料表載入資料。
   
   > [!NOTE]
   > 如果大 hello 資料，使用者可以建立 hello Hive 資料表與資料分割。 然後，使用者可以使用`for`hello 前端節點 tooload 資料至 hello Hive 資料表的資料分割來分割 hello Hadoop 命令列中的迴圈。
   > 
   > 
6. 在 Hadoop 命令列中，視需要瀏覽資料並建立功能。 請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。 只有附註 hello 必要查詢 toocreate 它們。
   
   a.  登入 toohello hello Hadoop 叢集前端節點
   
   b.  開啟 hello Hadoop 命令列。
   
   c.  命令所輸入 hello Hive 根目錄`cd %hive_home%\bin`Hadoop 命令列中。
   
   d.  Hello hello Hadoop 叢集 tooexplore hello 資料的前端節點上執行 hello Hive 查詢 Hadoop 命令列中，建立所需的功能。
7. 如果需要和/或所需，Azure Machine Learning Studio 中的 hello 資料 toofit 的範例。
8. 登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。
9. 直接從 hello 讀取 hello 資料`Hive Queries`使用 hello[匯入資料][ import-data]模組。 貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。
10. 從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。

## <a name="decisiontree"></a>用於案例選擇的決策樹
- - -
hello 圖摘要說明上述的 hello 案例和 hello 進階分析程序和技術做選擇的 hello 分項案例 tooeach 引導您。 請注意，可能需要資料處理、 瀏覽、 特徵設計和取樣置於一或多個方法/環境-hello 來源、 中繼、 和/或目標環境 – 並，仍然可以視需要重複。 hello 圖表只會做為一些可能的流程的說明，並不提供詳盡的列舉型別。

![範例 DS 程序逐步解說案例][8]

### <a name="advanced-analytics-in-action-examples"></a>進階分析實務範例
如需端對端 Azure Machine Learning 逐步解說採用 hello 進階分析程序和技術使用公用資料集，請參閱：

* [Team Data Science Process 實務：使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。
* [Team Data Science Process 實務：使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)。

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
