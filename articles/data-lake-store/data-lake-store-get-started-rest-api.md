---
title: "開始使用 Data Lake Store 的 aaaUse hello REST API tooget |Microsoft 文件"
description: "您可以使用 Data Lake store WebHDFS REST Api tooperform 作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>使用 REST API 開始使用 Azure Data Lake Store
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

在本文中，您將學習如何 toouse WebHDFS REST Api 和資料湖存放區 REST Api tooperform 帳戶管理，以及 Azure Data Lake Store 上的檔案系統作業。 Azure Data Lake Store 會公開自己的 REST API 以進行帳戶管理作業。 不過，因為 Data Lake Store 與 HDFS 和 Hadoop 生態系統相容，所以它支援使用 WebHDFS REST API 進行檔案系統作業。

> [!NOTE]
> Data Lake Store 的 hello REST API 支援的詳細資訊，請參閱[Azure 資料湖存放區 REST API 參考](https://msdn.microsoft.com/library/mt693424.aspx)。
> 
> 

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **建立 Azure Active Directory 應用程式**。 您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。 有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。
* [cURL](http://curl.haxx.se/)。 本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 Data Lake Store 帳戶。

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>如何使用 Azure Active Directory 驗證？
您可以使用兩個方法 tooauthenticate 使用 Azure Active Directory。

### <a name="end-user-authentication-interactive"></a>使用者驗證 (互動式)
在此案例中，hello 應用程式會提示中的 hello 使用者 toolog 和 hello hello 使用者內容中執行所有的 hello 作業。 執行 hello 互動式驗證步驟。

1. 您的應用程式，透過重新導向 hello 使用者 toohello 下列 URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<重新導向 URI > 需要 toobe 編碼 URL 中使用。 因此，針對 https://localhost，使用 `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    為了 hello 本教學課程，您可以取代上述 hello URL 中的 hello 預留位置值，並將它貼在網頁瀏覽器的網址列中。 您將會重新導向的 tooauthenticate 使用您的 Azure 登入。 一旦您已成功登入，hello 回應會顯示 hello 瀏覽器的網址列中。 hello 回應 hello 遵循格式會是：
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. 擷取 hello 回應 hello 授權碼。 此教學課程中，您可以複製 hello hello web 瀏覽器網址列中的 hello 授權碼，並將它傳遞 hello POST 要求 toohello 權杖端點，在如下所示：
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > 在此情況下，hello\<重新導向 URI > 不需要進行編碼。
   > 
   > 
3. hello 回應是包含存取權杖的 JSON 物件 (例如`"access_token": "<ACCESS_TOKEN>"`) 和重新整理權杖 (例如`"refresh_token": "<REFRESH_TOKEN>"`)。 您的應用程式使用 hello 存取權杖時存取 Azure 資料湖存放區和 hello 重新整理語彙基元 tooget 另一個存取權杖的存取權杖到期時。
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Hello 存取權杖過期時，您可以要求新的存取權杖使用 hello 重新整理權杖，如下所示：
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

如需互動使用者驗證的詳細資料，請參閱 [授權碼授與流程](https://msdn.microsoft.com/library/azure/dn645542.aspx)。

### <a name="service-to-service-authentication-non-interactive"></a>服務對服務驗證 (非互動式)
在此案例中，hello hello 應用程式會提供自己的認證 tooperform hello 作業。 這麼做，您必須發出 POST 要求像 hello 一個如下所示。 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

這項要求的 hello 輸出將包括授權權杖 (表示`access-token`hello 以下的輸出中)，您接下來將會傳遞 REST API 呼叫。 將此驗證權杖儲存在文字檔中；您將在本文稍後需要此權杖。

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

本文使用 hello**非互動式**方法。 如需有關非互動式 （服務對服務呼叫） 的詳細資訊，請參閱[服務會使用認證 tooservice 呼叫](https://msdn.microsoft.com/library/azure/dn645543.aspx)。

## <a name="create-a-data-lake-store-account"></a>建立 Data Lake Store 帳戶
這項作業根據定義的 hello REST API 呼叫[這裡](https://msdn.microsoft.com/library/mt694078.aspx)。

使用下列 cURL 命令 hello。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。 此命令的 hello 要求承載包含在 hello **input.json**提供 hello 檔案`-d`上述的參數。 hello hello input.json 檔內容看起來像下列 hello:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>在 Data Lake Store 帳戶中建立資料夾
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory)。

使用下列 cURL 命令 hello。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。 此命令會建立名為目錄**mytempdir** hello 的 Data Lake Store 帳戶的根資料夾下。

如果 hello 作業順利完成，您會看到如下的回應：

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>在 Data Lake Store 帳戶中列入資料夾
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory)。

使用下列 cURL 命令 hello。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。

如果 hello 作業順利完成，您會看到如下的回應：

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>將資料上傳至 Data Lake Store 帳戶
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File)。

使用下列 cURL 命令 hello。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

在上述語法 hello **-T**參數是您要上傳的 hello 檔案 hello 位置。

hello 輸出是類似 toohello 下列：
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>從 Data Lake Store 帳戶讀取資料
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File)。

從 Data Lake Store 帳戶讀取資料是兩個步驟的程序。

* 您第一次提交的 GET 要求針對 hello 端點`https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`。 這會傳回要求的位置 toosubmit hello 下一個 GET 要求。
* 然後送出 hello GET 要求，針對 hello 端點`https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`。 這會顯示 hello hello 檔案內容。

不過，因為沒有任何差異在 hello hello 個輸入的參數先和 hello 的第二個步驟，您可以使用 hello`-L`參數 toosubmit hello 第一個要求。 `-L`選項基本上結合成一個兩個要求，並將 cURL 重做 hello hello 新位置上的要求。 最後，hello hello 之所有要求呼叫就會顯示輸出，例如如下所示。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

您應該會看到類似 toohello 下列輸出：

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>在 Data Lake Store 帳戶中重新命名檔案
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory)。

使用 hello 下列 cURL 命令 toorename 檔案。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

您應該會看到類似 toohello 下列輸出：

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>從 Data Lake Store 帳戶刪除檔案
這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory)。

使用 hello 下列 cURL 命令 toodelete 檔案。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

您應該會看到類似 hello 下列輸出：

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>刪除 Data Lake Store 帳戶
這項作業根據定義的 hello REST API 呼叫[這裡](https://msdn.microsoft.com/library/mt694075.aspx)。

使用 hello 下列 cURL 命令 toodelete Data Lake Store 帳戶。 以 Data Lake Store 名稱取代 **\<yourstorename>**。

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

您應該會看到類似 hello 下列輸出：

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>另請參閱
* [與 Azure Data Lake Store 相容的開放原始碼巨量資料應用程式](data-lake-store-compatible-oss-other-applications.md)

