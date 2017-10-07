---
title: "aaaHow toouse hello Azure 從屬外掛程式與 Hudson 連續整合 |Microsoft 文件"
description: "描述如何 toouse hello Azure 從屬外掛程式與 Hudson 連續整合。"
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>如何 toouse hello Azure 從屬外掛程式與 Hudson 連續整合
hello Azure 從屬 Hudson 外掛程式可讓您在 Azure 上的 tooprovision 從屬節點時執行分散式組建。

## <a name="install-hello-azure-slave-plug-in"></a>安裝 hello Azure 從屬外掛程式
1. 在 hello Hudson 儀表板，按一下 **管理 Hudson**。
2. 在 hello**管理 Hudson**頁面上，按一下**管理外掛程式**。
3. 按一下 hello**可用** 索引標籤。
4. 按一下**搜尋**和型別**Azure** toolimit hello 清單 toorelevant 外掛程式。
   
    如果您選擇 tooscroll 透過 hello 可用的外掛程式清單，您會發現 hello Azure 從屬外掛程式在 hello**叢集管理和散佈建置**> 一節中 hello**其他** 索引標籤。
5. 選取 hello 核取方塊**Azure 從屬 Plugin**。
6. 按一下 [Install] 。
7. 重新啟動 Hudson。

現在已安裝該外掛程式的 hello，hello 下一個步驟是 tooconfigure hello 與您的 Azure 訂用帳戶設定檔的範本，可用於建立 hello 從屬節點的 VM hello toocreate 外掛程式。

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>使用您的訂用帳戶設定檔設定 hello Azure 從屬外掛程式
訂用帳戶設定檔，也參考的 tooas 發行設定，是包含安全認證，以及一些額外的資訊，您將需要使用 Azure toowork 開發環境中的 XML 檔案。 tooconfigure hello Azure 從屬外掛程式，您需要：

* 訂用帳戶 ID
* 訂用帳戶的管理憑證

您可以在 [訂用帳戶設定檔]中找到這些資訊。 以下是訂用帳戶設定檔的範例。

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

您的訂用帳戶設定檔之後，請遵循這些步驟 tooconfigure hello Azure 從屬外掛程式。

1. 在 hello Hudson 儀表板，按一下 **管理 Hudson**。
2. 按一下 [ **設定系統**]。
3. 捲動 hello 頁面 toofind hello**雲端**> 一節。
4. 按一下 [新增雲端 > Microsoft Azure]。
   
    ![新增雲端][add new cloud]
   
    這會顯示您的訂用帳戶詳細資料，您需要 tooenter hello 欄位。
   
    ![設定設定檔][configure profile]
5. 複製您的訂用帳戶設定檔中的 hello 訂用帳戶識別碼和管理憑證，並將它們貼 hello 適當的欄位。
   
    當複製 hello 訂用帳戶識別碼和管理憑證，**不**包含 hello 引號括住 hello 值。
6. 按一下 [ **驗證組態**]。
7. 當成功驗證 hello 的設定時，按一下 **儲存**。

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>設定虛擬機器範本的 hello Azure 從屬外掛程式
虛擬機器範本可定義 hello 參數 hello 外掛程式會在 Azure 上使用 toocreate 從屬節點。 在下列步驟的 hello 我們將建立範本的 Ubuntu vm。

1. 在 hello Hudson 儀表板，按一下 **管理 Hudson**。
2. 按一下 [ **設定系統**]。
3. 捲動 hello 頁面 toofind hello**雲端**> 一節。
4. Hello 內**雲端**區段中，尋找**加入 Azure 虛擬機器範本**按一下 hello**新增** 按鈕。
   
    ![新增 VM 範本][add vm template]
5. 指定雲端服務名稱在 hello**名稱**欄位。 如果您指定的 hello 名稱參考 tooan 現有雲端服務，hello VM 將會佈建該服務中。 否則，Azure 會建立一個新的。
6. 在 hello**描述**欄位中，輸入您要建立 hello 範本的描述文字。 此資訊僅供記錄之用，並不會用於佈建 VM。
7. 在 hello**標籤**欄位中，輸入**linux**。 此標籤是您要建立使用的 tooidentify hello 範本時，則後續使用的 tooreference hello 範本建立 Hudson 作業。
8. 選取建立 hello VM 所在的區域。
9. 選取 hello 適當的 VM 大小。
10. 指定 hello VM 將會建立儲存體帳戶。 請確定它是在 hello 與 hello 雲端服務，您將使用相同的區域。 如果您想建立新的儲存體 toobe，您可以將此欄位保留空白。
11. 保留時間指定 hello Hudson 刪除閒置的從屬版本之前的分鐘數。 將此設定保留 hello 預設值為 60。
12. 在**使用量**，將會使用這個從屬節點時，選取 hello 適當的條件。 就目前的情況，請選取 [ **盡可能利用此節點**]。
    
     此時，您的表單看起來可能有點像 toothis:
    
     ![範本設定][template config]
13. 在**映像系列或識別碼**您有 toospecify 哪些系統映像將會安裝在您的 VM。 您可以從映像系列清單中進行選取，或指定自訂映像。
    
     如果您想 tooselect 從映像系列的清單，請輸入 hello 第一個字元 （區分大小寫） 的 hello 映像系列名稱。 例如，輸入 **U** 將會顯示 Ubuntu Server 系列的清單。 一旦您選取從 hello 清單，Jenkins 將會使用該系統映像，從該系列 hello 最新版本，佈建 VM 時。
    
     ![作業系統系列清單][OS family list]
    
     如果您想 toouse 改用自訂影像，請輸入 hello 該自訂映像名稱。 自訂映像名稱不會顯示在清單中讓您擁有 hello 名稱的 tooensure 輸入正確。    
    
     此教學課程中，輸入**U** Ubuntu 映像，然後選取清單 toobring **Ubuntu Server 14.04 LTS**。
14. 在 [啟動方法] 中，選取 [SSH]。
15. 複製下列 hello 指令碼並貼上 hello**初始化指令碼**欄位。
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     hello**初始化指令碼**hello 建立 VM 之後將會執行。 在此範例中，hello 指令碼安裝 Java、 git、 以及 ant。
16. 在 hello **Username**和**密碼**欄位中，輸入您慣用的值會在您的 VM 中建立的 hello 系統管理員帳戶。
17. 按一下**驗證範本**toocheck，如果您指定的 hello 參數都有效。
18. 按一下 [儲存] 。

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>建立在 Azure 的從屬節點上執行的 Hudson 工作
在本節中，您將建立在 Azure 的從屬節點上執行的 Hudson 工作。

1. 在 hello Hudson 儀表板，按一下 **新工作**。
2. 輸入您要建立 hello 工作的名稱。
3. Hello 作業類型 選取**組建可用樣式軟體工作**。
4. 按一下 [確定] 。
5. 在 hello 工作組態頁面上，選取 **限制可以執行這個專案**。
6. 選取**節點和標籤功能表**選取**linux** （hello 上一節中建立 hello 虛擬機器範本時，我們指定此標籤）。
7. 在 hello**建置**區段中，按一下**加入建置步驟**選取**執行殼層**。
8. 編輯下列指令碼、 取代 hello **{您 github 帳戶名稱}**， **{project name}**，和**{您的專案目錄}**與適當的值，並貼上 hello編輯指令碼中出現的 hello 文字區域。
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. 按一下 [儲存] 。
10. 在 hello Hudson 儀表板，找出您剛才建立的 hello 作業，然後按一下 hello**排程組建**圖示。

Hudson 接著會建立使用 hello 範本建立 hello 前一節中的從屬節點，並執行這項工作中的 hello 建置步驟中所指定的 hello 指令碼。

## <a name="next-steps"></a>後續步驟
如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[訂用帳戶設定檔]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

