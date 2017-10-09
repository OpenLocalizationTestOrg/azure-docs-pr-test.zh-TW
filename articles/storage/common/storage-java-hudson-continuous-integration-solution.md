---
title: "使用 Blob 儲存體 aaaHow toouse Hudson |Microsoft 文件"
description: "描述如何使用 Azure Blob 儲存體為組建成品儲存機制的 toouse Hudson。"
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 196b5d014b0318c5972a052f7822b568cfcc23df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>使用 Azure 儲存體與 Hudson 連續整合解決方案
## <a name="overview"></a>概觀
hello 下列資訊會顯示 toouse Blob 儲存體做為儲存機制的組建成品建立 Hudson 連續整合 (CI) 解決方案，或將來源 toobe 可下載檔案的建置流程中的使用方式。 Hello 案例，您會發現這很有用的其中一個是當您的撰寫語言敏捷式開發環境 （使用 Java 或其他語言） 中，組建正在根據持續的整合，而您需要您的組建成品儲存機制，讓您可以例如，與其他組織的成員，您的客戶分享，或保存。  另一種情況時，您的組建工作本身需要其他檔案，比方說，相依性 toodownload 做為部分 hello 建置輸入。

在本教學課程中您將使用 hello Azure 儲存體外掛程式 Hudson CI Microsoft 所提供的。

## <a name="introduction-toohudson"></a>簡介 tooHudson
Hudson 的軟體專案藉由允許開發人員 tooeasily 整合其程式碼變更和已啟用持續整合組建產生自動和常見問題，藉此增加 hello hello 開發人員的產能。 組建具有版本設定，而且組建的成品可以上傳的 toovarious 儲存機制。 這篇文章會顯示如何 toouse 為 hello 儲存機制的 hello Azure Blob 儲存體建立成品。 它也會顯示如何從 Azure Blob 儲存體 toodownload 相依性。

您可以在 [認識 Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)(英文) 中找到有關 Hudson 的詳細資訊。

## <a name="benefits-of-using-hello-blob-service"></a>使用 hello Blob 服務的優點
使用 hello Blob 服務 toohost 的優點包括您靈活的開發組建成品：

* 組建成品和/或可下載相依性項目的高可用性。
* Hudson CI 解決方案上傳組建成品時的效能。
* 在您的客戶和合作夥伴下載組建成品時提供良好的效能。
* 提供使用者存取原則控制，可以選擇匿名存取、期限型共用存取簽章存取、私用存取等。

## <a name="prerequisites"></a>必要條件
您將需要 hello toouse hello 下列 Blob 服務與 Hudson CI 解決方案：

* Hudson 連續整合解決方案。
  
    如果您目前沒有 Hudson CI 解決方案，您可以執行使用下列技巧 hello Hudson CI 解決方案：
  
  1. 啟用 Java 功能的電腦上下載 hello 從 Hudson WAR <http://hudson-ci.org/>。
  2. 在命令提示字元中，這是包含執行 hello Hudson WAR hello Hudson WAR 開啟的 toohello 資料夾。 例如，如果您已下載 3.1.2 版：
     
      `java -jar hudson-3.1.2.war`

  3. 在瀏覽器中開啟 `http://localhost:8080/`。 這會開啟 hello Hudson 儀表板。
  4. 第一次使用 Hudson，完成 hello 必須在初始安裝`http://localhost:8080/`。
  5. Hello 初始安裝完成之後，取消執行個體的 hello Hudson WAR hello，請啟動 hello Hudson WAR 一次，並重新開啟 hello Hudson 儀表板， `http://localhost:8080/`，而您將使用 tooinstall 並設定 hello Azure 儲存體外掛程式。
     
      雖然一般 Hudson CI 解決方案會設定為服務 toorun，在 hello 命令列執行 hello Hudson war 將足以說明此教學課程。
* 一個 Azure 帳戶。 您可以在 <http://www.azure.com> 註冊 Azure 帳戶。
* 一個 Azure 儲存體帳戶。 如果您還沒有儲存體帳戶，您可以建立一個使用 hello 步驟[建立儲存體帳戶](../common/storage-create-storage-account.md#create-a-storage-account)。
* Hello Hudson CI 解決方案的認識，建議使用但非必要、 hello 做為儲存機制使用 Hudson CI hello Blob 服務時所需步驟的基本範例 tooshow hello 下列內容將會使用組建成品。

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>Toouse hello 與 Hudson CI 的 Blob 服務的方式
toouse hello 與 Hudson 的 Blob 服務，您將需要 tooinstall hello Azure 儲存體外掛程式，設定 hello 外掛程式 toouse 儲存體帳戶，再建立建置後動作上傳組建成品 tooyour 儲存體帳戶。 在 hello 下列各節說明這些步驟。

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>如何 tooinstall hello Azure 儲存體外掛程式
1. 在 hello Hudson 儀表板，按一下**管理 Hudson**。
2. 在 hello**管理 Hudson**頁面上，按一下**管理外掛程式**。
3. 按一下 hello**可用** 索引標籤。
4. 按一下 [其他] 。
5. 在 hello**成品 Uploaders**區段中，選取**Microsoft Azure 儲存體外掛程式**。
6. 按一下 [Install] 。
7. Hello 安裝已完成之後，重新啟動 Hudson。

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>如何 tooconfigure 會 hello Azure 儲存體外掛程式 toouse 儲存體帳戶
1. 在 hello Hudson 儀表板，按一下**管理 Hudson**。
2. 在 hello**管理 Hudson**頁面上，按一下**設定系統**。
3. 在 hello **Microsoft Azure 儲存體帳戶設定**> 一節：
   
    a. 輸入您儲存體帳戶名稱，您可以從 hello 取得[Azure 入口網站](https://portal.azure.com)。
   
    b. 輸入儲存體帳戶金鑰，也可行，或是從 hello [Azure 入口網站](https://portal.azure.com)。
   
    c. 使用預設值 hello **Blob 服務端點 URL**如果您使用 hello 公用 Azure 雲端。 如果您使用不同的 Azure 雲端，做為 hello 端點中指定的 hello [Azure 入口網站](https://portal.azure.com)儲存體帳戶。
   
    d. 按一下**驗證儲存體認證**toovalidate 儲存體帳戶。
   
    e. [選用]如果您想要製作可用 tooyour Hudson CI 的其他儲存體帳戶，請按一下**新增更多的儲存體帳戶**。
   
    f. 按一下**儲存**toosave 您的設定。

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>如何 toocreate 上傳組建成品 tooyour 儲存體帳戶的建置後動作
基於指令，首先我們需要 toocreate 的作業，將會建立數個檔案，然後再加入 hello 建置後動作 tooupload hello 檔案 tooyour 儲存體帳戶。

1. 在 hello Hudson 儀表板，按一下**新工作**。
2. 名稱 hello 工作**存放至 MyJob**，按一下**組建可用樣式軟體工作**，然後按一下**確定**。
3. 在 hello**建置**> 一節的 hello 工作設定，請按一下**加入建置步驟**選擇**執行 Windows 的批次命令**。
4. 在**命令**，使用下列命令的 hello:

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. 在 hello**建置後動作**> 一節的 hello 工作設定，請按一下**上傳成品 tooMicrosoft Azure Blob 儲存體**。
6. 如**儲存體帳戶名稱**，選取 hello 儲存體帳戶 toouse。
7. 如**容器名稱**，指定 hello 容器名稱。 （hello 容器將會建立如果它不存在時 hello 組建成品都會上傳）。您可以使用環境變數，因此此範例中輸入**${JOB_NAME}**為 hello 容器名稱。
   
    **秘訣**
   
    以下 hello**命令**您用來輸入的指令碼的區段**執行 Windows 的批次命令**辨識 Hudson toohello 環境變數是一個連結。 按一下該連結 toolearn hello 環境變數名稱和描述。 請注意該環境變數包含特殊字元，例如 hello **BUILD_URL**環境變數，不允許做為容器名稱或一般的虛擬路徑。
8. 在此範例中，請按一下 [Make new container public by default]。 （如果您想 toouse 私人容器，您必須 toocreate 共用的存取簽章 tooallow 存取。 這已超出本文的 hello 範圍。 若要深入了解共用存取簽章，請參閱[使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md)。)
9. [選用]按一下**全新容器將上傳之前**如果您想 hello 容器 toobe 清理內容之前上傳組建成品 （它如果核取不想讓 hello 容器 tooclean hello 內容）。
10. 如**的成品清單 tooupload**，輸入**文字 /*.txt**。
11. 在 [Common virtual path for uploaded artifacts]，輸入 **${BUILD\_ID}/${BUILD\_NUMBER}**。
12. 按一下**儲存**toosave 您的設定。
13. 在 hello Hudson 儀表板，按一下 **現在建置**toorun**存放至 MyJob**。 檢查 hello 主控台輸出的狀態。 Hello 建置後動作啟動 tooupload 組建成品時，將 hello 主控台輸出中包含 Azure 儲存體的狀態訊息。
14. 成功完成時的 hello 作業，您可以藉由開啟 hello 公用 blob 檢查 hello 組建成品。
    
    a. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
    
    b. 按一下 [儲存體] 。
    
    c. 按一下您要用於 Hudson 的 hello 儲存體帳戶名稱。
    
    d. 按一下 [容器] 。
    
    e. 按一下名為 hello 容器**存放至 myjob**，hello hello 作業的名稱建立 hello Hudson 作業時，您指派小寫的版本。 在 Azure 儲存體中，容器名稱和 Blob 名稱皆為小寫 (並且區分大小寫)。 Hello hello 容器名稱的 blob 清單內**存放至 myjob**您應該會看到**hello.txt**和**date.txt**。 複製 hello URL 的任一項目，並在您的瀏覽器中開啟它。 組建成品，您會看到已上傳的 hello 文字檔案。

每個作業，您可以建立只有一個上傳成品 tooAzure Blob 儲存體的建置後動作。 請注意 hello 單一建置後動作 tooupload 成品 tooAzure Blob 儲存體，可以指定不同的檔案 （包括萬用字元） 及路徑 toofiles 內**的成品清單 tooupload**使用分號作為分隔符號。 例如，如果您 Hudson 建置會產生 JAR 檔案和工作區中的 TXT 檔案**建置**資料夾，而您想 tooupload 這兩個 tooAzure Blob 儲存體，用於 hello hello 下列**的成品清單 tooupload**值：**建置 /\*d，則為建置 /\*.txt**。 您也可以使用雙冒號語法 toospecify 路徑 toouse hello blob 名稱中。 例如，如果您想要上傳使用 hello （每瓶) tooget**二進位檔**hello blob 路徑和 hello TXT 檔案 tooget 中上傳使用**通知**hello blob 的路徑中，用於 hello 下列 hello **清單中的成品 tooupload**值：**建置 /\*。 jar::binaries; 建置 /\*。 txt::notices**。

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>如何 toocreate 的建置步驟，下載從 Azure Blob 儲存體
hello 下列步驟顯示如何 tooconfigure 組建從 Azure Blob 儲存體中逐步 toodownload 項目。 這會是很有用，如果要在您的組建，例如，您在 Azure Blob 儲存體中保留的 （每瓶） tooinclude 項目。

1. 在 hello**建置**> 一節的 hello 工作設定，請按一下**加入建置步驟**選擇**從 Azure Blob 儲存體下載**。
2. 如**儲存體帳戶名稱**，選取 hello 儲存體帳戶 toouse。
3. 如**容器名稱**，指定 hello hello 容器具有您想要 toodownload hello blob 名稱。 您可以使用環境變數。
4. 如**Blob 名稱**，指定 hello blob 名稱。 您可以使用環境變數。 此外，您可以使用星號，做為萬用字元指定 hello 初始代號的磁碟區的 hello blob 名稱之後。 例如，**project\*** 指定名稱開頭為 **project** 的所有 Blob。
5. [選用]如**下載路徑**，指定您要從 Azure Blob 儲存體 toodownload 檔案 Hudson 機器 hello 上 hello 路徑。 也可以使用環境變數 (如果您未提供的值**下載路徑**，從 Azure Blob 儲存體的 hello 檔案會下載的 toohello 作業的工作區。)

如果您想 toodownload 從 Azure Blob 儲存體的其他項目，您可以建立額外的建置步驟。

執行建置後，您可以檢查 hello 建置記錄主控台輸出，或查看您的下載位置，toosee 是否 hello 已成功下載您所預期的 blob。

## <a name="components-used-by-hello-blob-service"></a>Hello Blob 服務所使用的元件
hello 以下提供 hello Blob 服務元件的概觀。

* **儲存體帳戶**： 所有存取的 tooAzure 是儲存體透過儲存體帳戶。 這是用於存取 blob 的 hello 命名空間的 hello 最高等級。 帳戶可以包含不限數目的容器，只要它們的大小總計低於 100 TB 即可。
* **容器**：容器提供一組 Blob 的群組。 所有 Blob 都必須放在容器中。 一個帳戶可以包含的容器不限數量。 容器可以儲存無限制的 Blob。
* **Blob**：任何類型和大小的檔案。 Azure 儲存中可以儲存兩種 Blob：區塊 Blob 和分頁 Blob。 大部分檔案都是區塊 Blob。 單一區塊 blob 可以是 up too200 GB 的大小。 本教學課程使用區塊 Blob。 分頁 blob，另一種 blob 類型，可向上 too1 TB 大小，且更有效率的檔案中的位元組範圍經常修改。 如需關於 Blob 的詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 及分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。
* **URL 格式**： 使用 hello 下列 URL 格式來定址 Blob:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    （hello 上述格式，適用於 toohello 公用 Azure 雲端。 如果您使用不同的 Azure 雲端，使用 hello 端點內 hello [Azure 入口網站](https://portal.azure.com)toodetermine URL 端點。)
  
    上述的 hello 格式`storageaccount`代表 hello 您的儲存體帳戶名稱，`container_name`代表 hello 您的容器名稱，和`blob_name`代表 hello 您的 blob 名稱，分別。 內 hello 容器名稱，您可以有多個以正斜線，分隔的路徑 **/** 。 本教學課程中的 hello 範例容器名稱為**存放至 MyJob**，和**${建置\_識別碼} / ${建置\_數目}** hello 一般虛擬路徑，導致 hello blob 擁有使用Hello 下列表單的 URL:
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>後續步驟
* [認識 Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
* [Azure 儲存體用戶端 SDK 參考](http://dl.windowsazure.com/storage/javadoc/)
* [Azure 儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)

如需詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。