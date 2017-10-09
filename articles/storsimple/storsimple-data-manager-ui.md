---
title: "Azure StorSimple Data Manager UI aaaMicrosoft |Microsoft 文件"
description: "描述如何 toouse StorSimple Data Manager 服務 UI （私人預覽中）"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>管理使用 hello StorSimple Data Manager 服務 UI （私人預覽中）

本文說明如何使用 hello StorSimple Data Manager UI tooperform 資料轉換，以及在 hello StorSimple 8000 系列裝置上的資料。 hello 已轉換的資料然後可供其他 Azure 服務，例如 Azure Media Services、 Azure HDInsight、 Azure Machine Learning 中，與 Azure 搜尋。 


## <a name="use-storsimple-data-transformation"></a>使用 StorSimple 資料轉換

hello StorSimple Data Manager 是 hello 資源內的資料轉換，才能執行個體化。 hello 資料轉換服務可讓您將資料從 Azure 儲存體中您 StorSimple 內部部署裝置 tooblobs 移。 因此，工作流程中您需要 toospecify hello 詳細資料有關的 toomove toohello 儲存體帳戶的感興趣的 StorSimple 裝置與 hello 資料。

### <a name="create-a-storsimple-data-manager-service"></a>建立 StorSimple Data Manager 服務

執行下列步驟 toocreate StorSimple Data Manager 服務的 hello。

1. toocreate StorSimple Data Manager 服務，跳過[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. 按一下 hello  **+** 圖示，並搜尋 StorSimple Data Manager。 按一下您的 StorSimple Data Manager 服務，然後按一下建立。

3. 如果您的訂用帳戶已啟用建立此服務，您會看到下列刀鋒視窗中的 hello。

    ![建立 StorSimple Data Managers 資源](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. 輸入 hello 輸入，然後按一下**建立**。 hello 指定位置應該在裝載您的儲存體帳戶和您的 StorSimple Manager 服務的其中一個 hello。 目前，僅支援美國西部和西歐區域。 因此，您的 StorSimple Manager 服務、 Data Manager 服務和 hello 相關聯儲存體帳戶應該都是在 hello 上述支援的地區。 它會每分鐘 toocreate hello 服務相關。

### <a name="create-a-data-transformation-job-definition"></a>建立資料轉換作業定義

在 StorSimple Data Manager 服務中，您需要 toocreate 資料轉換作業定義。 工作定義會指定您有興趣將移到 hello 原生格式的儲存體帳戶的 hello 資料的詳細資料。 

執行下列步驟 toocreate 新的資料轉換作業定義的 hello。

1.  瀏覽 toohello 您建立的服務。 按一下 [+ 作業定義]。

    ![按一下 [+ 作業定義]](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. hello 新工作定義 刀鋒視窗會開啟。 指定作業定義名稱，然後按一下 [來源]。 在 hello**設定資料來源**刀鋒視窗中，指定您的 StorSimple 裝置 hello 詳細資料和 hello 感興趣的資料。

    ![建立作業定義](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. 由於這是新的資料管理員服務，尚未設定任何資料儲存機制。 您的 StorSimple Manager 做為資料儲存機制中，按一下 tooadd**加入新**在 hello 資料儲存機制的下拉式清單中，然後按一下**新增資料儲存機制**。

4. 選擇**StorSimple 8000 系列管理員**hello 儲存機制為輸入，並輸入 hello 屬性您**StorSimple Manager**。 Hello**資源識別碼**欄位，您需要 tooenter hello 號碼之前 hello **:**在您的 StorSimple manager 的 hello 登錄機碼。

    ![建立資料來源](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  完成時按一下 [確定]。 這樣會儲存您的資料儲存機制，而且此 StorSimple Manager 可以重複使用在其他作業定義中，不需要再次輸入這些參數。 花幾秒後按一下**確定**hello 上的 StorSimple Manager tooshow hello 下拉式清單中。

6.  在 hello**設定資料來源**刀鋒視窗中，輸入 hello 裝置名稱和 hello 具有您感興趣的資料磁碟區名稱。

7.  在 hello**篩選**子區段中，輸入 hello 根目錄，其中包含您感興趣的資料 (此欄位的開頭應`\`)。 您也可以在這裡新增任何檔案篩選。

8.  hello 資料轉換服務適用於快照集透過推入總 toohello Azure 的 hello 資料。 當執行此作業，您可以選擇 tootake 備份每次執行此作業時 (toowork 上最新的資料) 或 toouse hello hello 雲端中的最後一個現有備份，（如果您正在針對某些封存的資料）。

    ![新增資料來源詳細資料](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. 接下來，hello 目標設定必須設定 toobe。 有 2 種支援的目標 – Azure 儲存體帳戶和 Azure 媒體服務帳戶。 選擇 儲存體帳戶 tooput 檔案中該帳戶的 blob。 選擇 media services 帳戶 tooput 檔案中該帳戶的資產。 同樣地，我們需要 tooadd 儲存機制。 在 hello 下拉式清單中，選取**新增**然後**設定**。

    ![建立資料接收](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. 在這裡，您可以選取您想要 tooadd 和 hello 與 hello 儲存機制相關聯的其他參數的儲存機制的 hello 類型。 在這兩種情況下，hello 工作執行時，會建立儲存體佇列。 此佇列中會填入已轉換的 blob 備妥時的相關訊息。 hello 這個佇列名稱是 hello 與 hello hello 工作定義名稱相同。 如果您選取**Media Services** hello 儲存機制類型，然後您也可以輸入儲存體帳戶認證建立 hello 佇列的位置。

    ![新增資料接收詳細資料](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. 在新增之後 hello 資料儲存機制 （這需要幾秒鐘），您會發現 hello 儲存機制中 hello hello 下拉式清單中**目標帳戶名稱**。  選擇您需要的 hello 目標。

12. 按一下**確定**toocreate hello 工作定義。 現在已設定作業定義。 您可以使用多次透過 hello UI 這個工作定義。

    ![新增作業定義](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>執行 hello 工作定義

每當您需要從 hello 工作定義中所指定的 StorSimple toohello 儲存體帳戶的 toomove 資料時，您將需要 tooinvoke 它。 在每次叫用 hello 作業變更 hello 參數沒有些許的彈性空間。 hello 步驟如下所示：

1. 選取您的 StorSimple Data Manager 服務，並移過**監視**。 按一下 [立即執行]。

    ![Trigger job definition](./media/storsimple-data-manager-ui/run-now.png)

2. 選擇 hello 工作定義您想 toorun。 按一下**回合設定**toomodify 您可能希望 toochange 執行此作業的任何設定。

    ![執行作業設定](./media/storsimple-data-manager-ui/run-settings.png)

3. 按一下**確定**，然後按一下**執行**toolaunch 您的工作。 toomonitor 此作業，請移 toohello**作業**頁面中您 StorSimple 資料管理員。

    ![作業清單及狀態](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. 在加法 toomonitoring 在 hello**作業**刀鋒視窗中，您也可以聆聽 hello 訊息加入每次從 StorSimple toohello 儲存體帳戶移動檔案的儲存體佇列上。


## <a name="next-steps"></a>後續步驟

[使用.NET SDK toolaunch StorSimple Data Manager 作業](storsimple-data-manager-dotnet-jobs.md)。
