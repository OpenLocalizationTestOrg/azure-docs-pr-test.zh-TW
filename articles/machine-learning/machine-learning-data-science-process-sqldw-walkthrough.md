---
title: "在動作中的 hello 小組資料科學程序： 使用 SQL 資料倉儲 |Microsoft 文件"
description: "進階分析程序和技術實務"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>在動作中的 hello 小組資料科學程序： 使用 SQL 資料倉儲
在本教學課程中，我們會逐步引導您建立及部署使用 SQL 資料倉儲 (SQL DW) 的機器學習模型公開可用的資料集-hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集。 建構的 hello 二元分類模型會預測提示支付路線，以及多級分類和迴歸模型，也會探討預測 hello 發佈 hello 提示金額付費。

hello 程序會遵循 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)工作流程。 我們會示範如何 toosetup 資料科學環境中，如何 tooload hello 資料到 SQL DW 及如何使用 SQL DW 或 IPython 筆記型電腦 tooexplore hello 資料和工程師功能 toomodel。 然後顯示如何 toobuild 和部署 Azure 機器學習模型。

## <a name="dataset"></a>hello NYC 計程車往返的資料集
hello NYC 計程車路線資料包含約 20 GB 的壓縮的 CSV 檔案 (~ 48 GB 未壓縮)，錄製超過 173 百萬個個別的往返和 hello fares 支付每往返作業。 每個往返記錄包括 hello 收取和下車位置以及時間、 匿名 hack (driver) 授權編號，並重新 hello medallion (計程車的唯一 id) 數目。 hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:

1. hello **trip_data.csv**檔案包含路線詳細資料，例如乘客、 收取和 dropoff 點、 路線期間與路線長度的數目。 以下是一些範例記錄：
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. hello **trip_fare.csv**檔案包含的 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。 以下是一些範例記錄：
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

hello**唯一索引鍵**用 toojoin 路線\_資料和路線\_價位組成 hello 下列三個欄位：

* medallion、
* hack\_license 和
* pickup\_datetime。

## <a name="mltasks"></a>處理三種類型的預測工作
我們制訂根據 hello 的三個預測問題*提示\_量*tooillustrate 三種模型化工作：

1. **二元分類**: toopredict 是否提示支付路線，也就是*提示\_量*大比 $0 為正數的範例，而*提示\_量* $0 是負的範例。
2. **多級分類**: hello 路線支付 toopredict hello 範圍的提示。 我們將 hello*提示\_量*到五個紙匣或類別：
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **迴歸工作**: toopredict hello 數量提示支付路線。  

## <a name="setup"></a>設定進階分析 hello Azure 資料科學環境
tooset Azure 資料科學環境，請遵循下列步驟。

**建立自己的 Azure Blob 儲存體帳戶**

* 當您佈建您自己的 Azure blob 儲存體時，選擇 Azure blob 儲存體中或盡可能接近的地理位置太**美國中南部**，這是儲存 hello NYC 計程車資料。 會使用您自己的儲存體帳戶中所提供的 hello 公用 blob 儲存體容器 tooa 容器 AzCopy 複製 hello 資料。 hello 接近您的 Azure blob 儲存體是 tooSouth 美國中部、 hello 速度 (步驟 4)，這項工作將會完成。
* toocreate 您自己的 Azure 儲存體帳戶，步驟所述，在後續 hello[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 在此逐步解說稍後會需要這些是確定 toomake 注意事項 hello 值，如下列儲存體帳戶認證。
  
  * **儲存體帳戶名稱**
  * **儲存體帳戶金鑰**
  * **容器名稱**（其中要儲存在 hello Azure blob 儲存體中的 hello 資料 toobe）

**佈建 Azure SQL DW 執行個體。**
請遵循 hello 文件，網址[建立 SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)tooprovision SQL 資料倉儲執行個體。 請確定您遵循 SQL 資料倉儲的認證將用於在稍後步驟中的 hello 上進行標記法。

* **伺服器名稱**：<server Name>.database.windows.net
* **SQLDW (資料庫) 名稱**
* **使用者名稱**
* **密碼**

**安裝 Visual Studio 和 SQL Server Data Tools。** 如需指示，請參閱 [安裝適用於 SQL 資料倉儲的 Visual Studio 2015 及/或 SSDT (SQL Server Data Tools)](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md)中概述的步驟。

**使用 Visual Studio 中連接 tooyour Azure SQL DW。** 如需指示，請參閱 < 步驟 1 和 2 中的[連接 Visual Studio 中的 SQL 資料倉儲 tooAzure](../sql-data-warehouse/sql-data-warehouse-connect-overview.md)。

> [!NOTE]
> 執行 hello 下列在您的 SQL 資料倉儲中建立 hello 資料庫上的 SQL 查詢 （而不是所提供的 hello 步驟 3 中的 hello 查詢連接 > 主題） 太**建立主要金鑰**。
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**在 Azure 訂用帳戶下建立 Azure Machine Learning 工作區。** 如需指示，請參閱 [建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)中概述的步驟。

## <a name="getdata"></a>Hello 資料載入 SQL 資料倉儲
開啟 Windows PowerShell 命令主控台。 執行 hello 下列 PowerShell 命令 toodownload hello 範例 SQL 指令碼檔案我們與您共用 GitHub tooa 本機目錄上您指定與 hello 參數*-DestDir*。 您可以變更參數值 hello *-DestDir* tooany 本機目錄。 如果*-DestDir*不存在，則會建立由 hello PowerShell 指令碼。

> [!NOTE]
> 您可能需要**系統管理員身分執行**執行下列 PowerShell 指令碼，如果 hello 時您*DestDir*需系統管理員權限 toocreate 或 toowrite tooit 目錄。
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

成功執行之後，您目前的工作目錄太變更*-DestDir*。 您應該會類似如下的 toosee 螢幕：

![][19]

在您*-DestDir*，執行下列 PowerShell 指令碼，以系統管理員模式的 hello:

    ./SQLDW_Data_Import.ps1

當 hello PowerShell 指令碼執行 hello 第一次時，您會從您的 Azure SQL DW 和 Azure blob 儲存體帳戶要求 tooinput hello 資訊。 這個 PowerShell 指令碼完成時執行第一次，hello 認證 hello 您輸入將已經寫入 tooa 組態檔 SQLDW.conf hello 存在的工作目錄中。 hello 未來執行這個 PowerShell 指令碼檔案有 hello 選項 tooread 所需的所有參數從這個組態檔。 如果您需要 toochange 某些參數時，您可以選擇 tooinput hello 囉 」 畫面時刪除這個組態檔，並在出現提示時輸入 hello 參數值的提示字元或 toochange hello 參數值的參數，藉由編輯 hello SQLDW.conf 檔案在您*-DestDir*目錄。

> [!NOTE]
> 在訂單 tooavoid 結構描述名稱衝突與已存在於 Azure SQL DW 中，直接從 hello SQLDW.conf 檔案讀取參數時，3 位數的隨機數字加入 toohello 結構描述名稱從 hello SQLDW.conf 檔案做為 hello 預設結構描述名稱每次執行。 hello PowerShell 指令碼可能會提示您輸入的結構描述名稱： hello 名稱可指定使用者自行決定。
> 
> 

這**PowerShell 指令碼**檔完成下列工作的 hello:

* 如果尚未安裝 AzCopy，請**下載並安裝 AzCopy**
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **複製資料 tooyour 私用 blob 儲存體帳戶**從利用 azcopy 進行 hello 公用 blob
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **載入資料，使用 Polybase （藉由執行 LoadDataToSQLDW.sql） tooyour Azure SQL DW**從私用 blob 儲存體帳戶以 hello 下列命令。
  
  * 建立結構描述
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * 建立資料庫範圍認證
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * 建立 Azure 儲存體 Blob 的外部資料來源。
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * 建立 CSV 檔案的外部檔案格式。 未壓縮的資料，並以 hello 管道字元分隔的欄位。
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * 為 Azure Blob 儲存體的 NYC 計程車資料集建立外部 fare 和 trip 資料表。
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - 從 Azure blob 儲存體 tooSQL 資料倉儲內的外部資料表載入資料

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - 建立範例資料表 (NYCTaxi_Sample) 並插入資料 tooit 選取 hello 行程及價位資料表上的 SQL 查詢。 （這個逐步解說的部分步驟需要 toouse 這個範例資料表。）

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

hello 的儲存體帳戶的地理位置會影響載入時間。

> [!NOTE]
> 根據 hello 私用 blob 儲存體帳戶的地理位置、 公用 blob tooyour 私人儲存體帳戶複製資料 hello 程序需要大約 15 分鐘的時間，或甚至更久，與 hello 程序的儲存體帳戶中的資料載入Azure SQL DW tooyour 花費 20 分鐘或更長。  
> 
> 

您必須 toodecide 如果您有重複的來源和目的地檔案該怎麼做。

> [!NOTE]
> 如果已經從 hello 公用 blob 儲存體 tooyour 私用 blob 儲存體帳戶複製 hello.csv 檔案 toobe 存在於私用 blob 儲存體帳戶，AzCopy 會詢問您是否要 toooverwrite 它們。 如果您不想 toooverwrite 它們，請輸入 **n** 出現提示時。 如果您想 toooverwrite**所有**項目，請輸入出現提示時。 您也可以輸入**y** toooverwrite.csv 個別檔案。
> 
> 

![圖 #21][21]

您可以使用自己的資料。 如果您的資料位於內部部署電腦應用程式的真實生活中，您仍然可以使用 AzCopy tooupload 在內部部署資料 tooyour 私用的 Azure blob 儲存體。 您只需要 toochange hello**來源**位置， `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`，在 hello hello PowerShell 指令碼檔案 toohello 本機目錄，包含資料的 AzCopy 命令。

> [!TIP]
> 如果您的資料已在您應用程式的真實生活中的私用的 Azure blob 儲存體中，您可以略過的 hello AzCopy hello PowerShell 指令碼中的步驟，並直接上傳 hello 資料 tooAzure SQL DW。 這將需要其他編輯的 hello 指令碼 tootailor 它 toohello 格式的資料。
> 
> 

這個 Powershell 指令碼也插入 hello Azure SQL DW 資訊至 hello 資料瀏覽範例檔案 SQLDW_Explorations.sql，SQLDW_Explorations.ipynb 和 SQLDW_Explorations_Scripts.py 如此這三個檔案會立即嘗試準備 toobehello PowerShell 指令碼完成。

成功執行之後，您會看到如下畫面：

![][20]

## <a name="dbexplore"></a>Azure SQL 資料倉儲中的資料探索和特徵工程
在本節中，我們會使用 **Visual Studio Data Tools**直接對 Azure SQL DW 執行 SQL 查詢，以探索資料和產生特徵。 使用本節中的所有 SQL 查詢可以都在 hello 範例指令碼名為*SQLDW_Explorations.sql*。 這個檔案已下載的 tooyour hello PowerShell 指令碼的本機目錄。 您也可以從 [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql) 擷取此檔案。 但在 GitHub 中的 hello 檔案沒有 hello Azure SQL DW 資訊插入。

連接 tooyour Azure SQL DW hello SQL DW 登入名稱和密碼使用 Visual Studio，並開啟 hello **SQL 物件總管**tooconfirm hello 資料庫和資料表已匯入。 擷取 hello *SQLDW_Explorations.sql*檔案。

> [!NOTE]
> tooopen Parallel Data Warehouse (PDW) 查詢編輯器中，使用 hello**新查詢**命令，讓您 PDW 中 hello 選取**SQL 物件總管**。 PDW 不支援 hello 標準 SQL 查詢編輯器。
> 
> 

以下是 hello 類型的資料探索和功能產生的工作執行這一節：

* 在變動的時間範圍中探索數個欄位的資料分佈。
* 調查 hello 經度和緯度欄位的資料品質。
* 產生二進位和多級分類標籤根據 hello**提示\_量**。
* 產生功能，並計算或比較車程距離。
* 聯結 hello 兩個資料表，和擷取將會使用的 toobuild 模型的隨機取樣。

### <a name="data-import-verification"></a>資料匯入驗證
這些查詢提供快速驗證數目的資料列和資料行中 hello 資料表填入先前使用 Polybase 的平行大量匯入，hello

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**輸出：** 您應該有 173,179,759 個資料列和 14 個資料行。

### <a name="exploration-trip-distribution-by-medallion"></a>探索：依據 medallion 的車程分佈
這個範例查詢會識別特定的時間週期內完成超過 100 個往返的 hello medallions （計程車數字）。 hello 查詢獲益 hello 分割資料表的存取因為它由 hello 分割區配置所**收取\_datetime**。 查詢 hello 完整資料集也會進行 hello 資料分割資料表的使用及/或索引掃描。

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**輸出：** hello 查詢應該傳回具有指定 hello 13,369 medallions (taxis) 的資料列的資料表和 hello 路線 2013年中已完成的數目。 hello 最後一個資料行包含 hello 的往返次數已完成的 hello 的計數。

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>探索：依據 medallion 和 hack_license 的車程分佈
這個範例會識別 hello medallions （計程車數字） 和 hack_license 數字 （驅動程式） 完成的多個 100 往返指定的時間範圍內。

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**輸出：** hello 查詢應該傳回 13,369 指定 hello 13,369 汽車/驅動程式已完成多該 100 往返 2013年中的識別碼的資料列的資料表。 hello 最後一個資料行包含 hello 的往返次數已完成的 hello 的計數。

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>資料品質評估：驗證含有不正確經度和/或緯度的記錄
此範例中，以調查如果任一個 hello 經度和/或緯度的欄位可能包含無效的值 （弧度角度應該介於-90 到 90 之間），或具有 （0，0） 座標。

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**輸出：** hello 查詢會傳回具有無效的經度和/或緯度欄位 837,467 往返。

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>探索：已支付小費和未支付小費的車程分佈
此範例會尋找 hello 已傾斜與 hello 數目，已不傾斜指定的時間內 （或在 hello 完整資料集，如果它已設定此處涵蓋 hello 完整的年份） 的往返次數。 此分佈會反映 hello 二進位標籤發佈 toobe 稍後用於二元分類模型。

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**輸出：** hello 查詢應該傳回 hello 下列秘訣頻率 hello 年份 2013年: 90,447,622 傾斜和 82,264,709 not 傾斜。

### <a name="exploration-tip-classrange-distribution"></a>探索：小費類別/範圍分佈
此範例會計算 hello 布提示範圍中指定的時間週期 （或在 hello 完整資料集，如果涵蓋 hello 完整年）。 這是 hello 發佈的 hello 標籤類別會用於多級分類模型的更新版本。

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**輸出：**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>探索：計算並比較車程距離
這個範例會將轉換 hello 收取和下車經度和緯度 tooSQL geography 點、 計算 hello 旅行距離使用 SQL geography 點差異，並傳回隨機取樣的 hello 比較結果。 hello 範例限制 hello toovalid 協調只能使用稍早討論的 hello 資料品質評估查詢的結果。

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>使用 SQL 函式的功能工程
有時 SQL 函式會是有效率進行功能工程的合適選項。 在本逐步解說中，我們會定義 SQL 函式 toocalculate hello 直接之間的距離 hello 收取和 dropoff 位置。 您可以執行下列 SQL 指令碼中的 hello **Visual Studio Data Tools**。

以下是定義 hello 距離函式的 hello SQL 指令碼。

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

以下是範例 toocall 此函式 toogenerate 功能在 SQL 查詢：

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**輸出：**收取和 dropoff 經緯度與此查詢會產生的資料表 （含 2,803,538 資料列） 和您該與 hello 對應導向英里內的距離。 前 3 個資料列的 hello 結果如下：

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>準備資料以進行模型建置
hello 下列查詢會聯結 hello **nyctaxi\_路線**和**nyctaxi\_價位**資料表時，會產生二進位分類標籤**傾斜**、多級分類標籤**提示\_類別**，然後從 hello 完整聯結的資料集擷取的範例。 hello 取樣是擷取 hello 往返收取時間為基礎的子集。  此查詢可以複製，然後直接在 hello 貼入[Azure Machine Learning Studio](https://studio.azureml.net) [匯入資料][ import-data] hello SQL 資料庫執行個體中的直接資料擷取的模組在 Azure 中。 hello 查詢排除具有不正確的記錄 （0，0） 座標。

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

當您準備好 tooproceed tooAzure 機器學習服務，您可以：  

1. 儲存 hello 最終 SQL 查詢 tooextract 和範例 hello 資料和複製-貼上 hello 查詢直接[匯入資料][ import-data]模組在 Azure Machine Learning 中，或
2. 保存取樣的 hello 與工程的資料您計劃 toouse 模型建立新的 SQL DW 中的資料表，並在 hello 使用 hello 新資料表[匯入資料][ import-data] Azure Machine Learning 中的模組。 hello PowerShell 指令碼，在先前步驟中所做的這。 您可以直接從這個資料表 hello 資料匯入模組中讀取。

## <a name="ipnb"></a>IPython Notebook 中的資料探索和特徵工程設計
在本節中，我們將會執行資料探索和使用這兩個 Python 的功能產生並稍早建立 hello SQL DW 的 SQL 查詢。 名為範例 IPython 筆記型電腦**SQLDW_Explorations.ipynb**和 Python 指令碼檔案**SQLDW_Explorations_Scripts.py**已下載的 tooyour 本機目錄。 您也可以在 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW)上取得這兩個檔案。 在 Python 指令碼中，這兩個檔案是相同的。 如果您沒有 IPython Notebook 伺服器，會提供 tooyou hello Python 指令碼檔案。 這兩個範例 Python 檔案是以 **Python 2.7**設計。

hello hello 範例 IPython 筆記型電腦中所需的 Azure SQL DW 資訊和 hello 的 Python 指令碼檔案下載的 tooyour 本機電腦已插入 hello PowerShell 指令碼之前。 因此，不必進行任何修改就可以執行。

如果您已經設定 AzureML 工作區，您就可以直接上傳 hello 範例 IPython 筆記型電腦 toohello AzureML IPython 筆記型電腦服務，並開始執行。 以下是 hello 步驟 tooupload tooAzureML IPython 筆記型電腦服務：

1. 登入 tooyour AzureML 工作區，在 hello 頂端，按一下 「 Studio 」 然後按一下 [筆記型電腦] 左側 hello hello 網頁。
   
    ![圖 #22][22]
2. Hello 左下角的 hello 網頁上，按一下 [新增]，然後選取 「 Python 2"。 接著，提供名稱 toohello 筆記本，然後按一下 hello 核取記號 toocreate hello 新空白 IPython 筆記型電腦。
   
    ![圖 #23][23]
3. 按一下 hello"Jupyter"符號 hello 左角 hello 新 IPython 筆記型電腦。
   
    ![圖 #24][24]
4. 拖曳和卸除 hello 範例 IPython 筆記型電腦 toohello**樹狀**您 AzureML IPython 筆記型電腦服務，然後按一下頁面**上傳**。 然後，hello 範例 IPython 筆記型電腦將上傳的 toohello AzureML IPython 筆記型電腦服務。
   
    ![圖 #25][25]

在訂單 toorun hello 範例 IPython 筆記型電腦或 hello Python 指令碼檔案，hello 下列 Python 封裝所需。 如果您使用 hello AzureML IPython 筆記型電腦服務，已預先安裝這些套件。

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

hello AzureML 上建立進階分析解決方案，大型資料時，建議順序為 hello 下列：

* 在 hello 資料的小型範例讀入記憶體中的資料框架。
* 執行一些視覺效果，並使用瀏覽 hello 取樣的資料。
* 實驗功能使用 hello 取樣資料的工程團隊。
* 對於較大的資料瀏覽、 資料操作和特徵設計使用 Python tooissue SQL 查詢，直接對 SQL DW hello。
* 決定 hello 範例大小 toobe 適用於 Azure 機器學習模型建立。

hello 以下是幾個資料探索、 資料視覺效果和功能工程範例。 Hello 範例 IPython 筆記型電腦與 hello 範例 Python 指令碼檔案中可以找到更多的資料瀏覽。

### <a name="initialize-database-credentials"></a>初始化資料庫認證
初始化 hello 下列變數中的資料庫連線設定：

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>建立資料庫連接
以下是 hello 建立 hello 連線 toohello 資料庫的連接字串。

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>報告資料表 <nyctaxi_trip> 中資料列和資料行的數目
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* 資料列總數 = 173179759  
* 資料行總數 = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>報告資料表 <nyctaxi_fare> 中資料列和資料行的數目
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* 資料列總數 = 173179759  
* 資料行總數 = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>讀取在小型資料中的範例 hello SQL 資料倉儲資料庫
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

時間 tooread hello 範例資料表為 14.096495 秒。  
擷取的資料列和資料行數目 = (1000, 21)。

### <a name="descriptive-statistics"></a>描述性統計資料
現在您已準備好 tooexplore hello 取樣資料。 我們以查看一些描述性統計資料的 hello 開頭**路線\_距離**（或任何其他欄位選擇 toospecify）。

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>視覺效果：盒狀圖範例
我們會審視 hello 盒狀圖 hello 旅行距離 toovisualize hello 分位數下一步。

    df1.boxplot(column='trip_distance',return_type='dict')

![圖 #1][1]

### <a name="visualization-distribution-plot-example"></a>視覺效果：分佈的盒狀圖範例
視覺化 hello 發佈和 hello 長條圖的繪圖取樣旅行距離。

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![圖 #2][2]

### <a name="visualization-bar-and-line-plots"></a>視覺效果：長條圖和折線圖
在此範例中，我們可以分類收納成五個分類收納 hello 旅行距離和視覺化 hello 分類收納的結果。

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

我們可以繪製 hello 上方列中的分類收納發佈或線條繪圖與：

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![圖 #3][3]

和

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![圖 #4][4]

### <a name="visualization-scatterplot-examples"></a>視覺效果：散佈圖範例
我們顯示散佈圖之間**路線\_時間\_中\_秒**和**路線\_距離**toosee 如果有任何相互關聯

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![圖 #6][6]

同樣地，我們可以檢查 hello 之間的關聯性**速率\_程式碼**和**路線\_距離**。

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![圖 #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>在 IPython Notebook 中使用 SQL 查詢對取樣資料進行資料探索
在本節中，我們會探討使用保存 hello 前面所建立的新資料表中的 hello 取樣資料的資料分佈。 請注意，可以使用 hello 原始資料表執行類似的瀏覽。

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>瀏覽： 報表數目資料列和資料行中 hello 取樣的資料表
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>探索：已支付小費/未支付小費的分佈
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>探索：小費類別分佈
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>瀏覽： 繪製 hello 提示發佈由類別
    tip_class_dist['tip_freq'].plot(kind='bar')

![圖 #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>探索：車程的每日分佈
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>探索：根據 medallion 的車程分佈
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>探索：依據計程車牌照和計程車駕照的車程分佈
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>探索：車程時間分佈
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>探索：車程距離分佈
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>探索：付款類型分佈
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>確認 hello 最終格式的 hello 特徵化資料表
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>在 Azure Machine Learning 中建置模型
現在，我們已準備好 tooproceed toomodel 建置和中的模型部署[Azure Machine Learning](https://studio.azureml.net)。 hello 資料是用在 hello 預測問題，也就是先前定義的任何準備好 toobe:

1. **二元分類**: toopredict 提示是否支付路線。
2. **多級分類**: toopredict hello 範圍的提示，根據 toohello 先前定義的類別。
3. **迴歸工作**: toopredict hello 數量提示支付路線。  

toobegin hello 模型練習中，登入 tooyour **Azure Machine Learning**工作區。 如果您尚未建立機器學習服務工作區，請參閱「 [建立 Azure ML 工作區](machine-learning-create-workspace.md)」。

1. tooget 開始使用 Azure Machine Learning 中，請參閱[什麼是 Azure Machine Learning Studio？](machine-learning-what-is-ml-studio.md)
2. 登入太[Azure Machine Learning Studio](https://studio.azureml.net)。
3. hello Studio 首頁上提供豐富的資訊、 視訊、 教學課程中，連結 toohello 模組參考和其他資源。 如需有關 Azure Machine Learning 的詳細資訊，請參閱 hello [Azure 機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。

典型的訓練實驗組成 hello 下列步驟：

1. 建立 **+NEW** 實驗。
2. 進入 Azure ML hello 資料。
3. 前置處理、 轉換和視需要處理 hello 資料。
4. 視需要產生功能。
5. Hello 資料分割為訓練/驗證/測試資料集 (或有個別的資料集的每個)。
6. 選取一或多個機器學習演算法根據學習問題 toosolve hello。 例如，二進位分類、多類別分類、迴歸。
7. 培訓使用 hello 定型資料集的一或多個模型。
8. 得分 hello 驗證資料集使用 hello 定型的模型。
9. 評估 hello 模型 toocompute hello 相關的度量 hello 學習問題。
10. 微調 hello 模型和選取 hello 最佳模型 toodeploy。

在此練習中，我們已經瀏覽和工程 hello SQL 資料倉儲中的資料，並在 Azure ML hello 範例大小 tooingest 決定。 一或多個 hello 預測模型，以下是 hello 程序 toobuild:

1. Hello 資料送入使用 hello Azure ML[匯入資料][ import-data]模組，用於 hello**資料輸入和輸出**> 一節。 如需詳細資訊，請參閱 hello[匯入資料][ import-data]模組參考頁面。
   
    ![Azure ML 匯入資料][17]
2. 選取**Azure SQL Database**為 hello**資料來源**在 hello**屬性**面板。
3. 輸入 hello 資料庫 DNS 名稱在 hello**資料庫伺服器名稱**欄位。 格式： `tcp:<your_virtual_machine_DNS_name>,1433`
4. 輸入 hello**資料庫名稱**hello 對應欄位中。
5. 輸入 hello *SQL 使用者名稱*在 hello**伺服器使用者帳戶名稱**，和 hello*密碼*在 hello**伺服器使用者帳戶密碼**。
6. 檢查 hello**接受任何伺服器憑證**選項。
7. 在 hello**資料庫查詢**編輯文字區域中，貼上 hello 查詢 hello 必要資料庫欄位 （包括任何計算的欄位，例如 hello 標籤） 和向下會擷取範例 hello 資料所需的 toohello 取樣大小。

二元分類實驗，直接從 hello SQL 資料倉儲資料庫讀取資料的範例是在 hello 圖中 (請記住 tooreplace hello 資料表名稱 nyctaxi_trip 及 nyctaxi_fare hello 結構描述名稱和 hello 資料表名稱中使用程式逐步解說）。 您可以針對多類別分類和迴歸問題建構類似的實驗。

![Azure ML 訓練][10]

> [!IMPORTANT]
> 在 hello 模型化資料擷取和取樣的查詢範例提供上一節， **hello 三個模型練習的所有標籤都包含在 hello 查詢**。 （必要） 的重要步驟，在每個模型化練習 hello 太**排除**hello hello 不必要的標籤，其他兩個問題，以及任何其他**目標遺漏**。 當使用二元分類，例如，使用 hello 標籤**傾斜**和排除 hello 欄位**提示\_類別**，**提示\_量**，和**總\_量**。 hello 後者目標流失，因為它們意指 hello 提示付費。
> 
> tooexclude 任何不必要的資料行或目標流失，您可以使用 hello[資料集中選取的資料行][ select-columns]模組或 hello[編輯中繼資料][ edit-metadata]. 如需詳細資訊，請參閱[選取資料集中的資料行][select-columns]和[編輯中繼資料][edit-metadata]參考頁面。
> 
> 

## <a name="mldeploy"></a>在 Azure Machine Learning 中部署模型
準備您的模型時，可以輕鬆地將它部署為 web 服務，直接從 hello 實驗。 如需關於部署 Azure ML Web 服務的詳細資訊，請參閱 [部署 Azure 機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

toodeploy 新的 web 服務，您要：

1. 建立計分實驗。
2. 部署 hello web 服務。

從計分實驗的 toocreate**已經完成**定型實驗，按一下**建立計分實驗**hello 較低的動作列中。

![Azure 評分][18]

Azure Machine Learning 會嘗試 toocreate hello 定型實驗 hello 元件為基礎的計分實驗。 特別是，它將：

1. 儲存 hello 定型的模型，並移除 hello 模型定型模組。
2. 找出邏輯**輸入連接埠**toorepresent hello 預期輸入的資料結構描述。
3. 找出邏輯**輸出連接埠**toorepresent hello 預期的 web 服務輸出結構描述。

建立 hello 計分實驗時，檢閱它，並進行視需要調整。 因為這些不會使用呼叫 hello 服務時，一般調整是 tooreplace hello 輸入資料集和 （或） 查詢，其中包含一個排除標籤欄位。 它也是很好的作法 tooreduce hello 大小 hello 的輸入資料集和 （或) 查詢 tooa 少數的記錄，剛好足夠 tooindicate hello 輸入結構描述。 Hello 輸出連接埠，它是一般 tooexclude 所有輸入的欄位，只包含 hello**計分標籤**和**計分機率**中輸出使用 hello hello[資料集中選取的資料行] [ select-columns]模組。

在 hello 圖中有提供範例計分實驗。 一切就緒後 toodeploy，按一下 hello**發佈 WEB 服務**hello 較低的動作列中按鈕。

![Azure ML 發佈][11]

## <a name="summary"></a>摘要
toorecap 我們已完成此逐步解說的教學課程中，您已建立的 Azure 資料科學環境中，使用過大的公用資料集，使其透過 hello 小組資料科學程序，從資料擷取 toomodel 定型，所有的 hello 方法，然後在 Azure Machine Learning web 服務的 toohello 部署。

### <a name="license-information"></a>授權資訊
此範例逐步解說，以及其隨附的指令碼和 IPython notebook(s) 共用的 Microsoft hello MIT 授權。 請 hello 目錄中的 hello 範例程式碼在 GitHub 上如需詳細資訊，在檢查 hello LICENSE.txt 檔。

## <a name="references"></a>參考
•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)  
•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
