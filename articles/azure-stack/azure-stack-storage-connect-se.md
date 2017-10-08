---
title: "aaaConnect 存放裝置總管 tooan 堆疊 Azure 訂用帳戶"
description: "深入了解如何 tooconnect 儲存體 Exporer tooan 堆疊 Azure 訂用帳戶"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a>連接儲存體總管 tooan 堆疊 Azure 訂用帳戶

Azure 儲存體總管 （預覽） 是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 堆疊儲存體資料。 有數個工具相配 toomove 資料 tooand 從 Azure 堆疊儲存體。 如需詳細資訊，請參閱 [Azure Stack 儲存體適用的資料傳輸工具](azure-stack-storage-transfer.md)。

在本文中，您將學習如何 tooconnect tooyour 堆疊 Azure 儲存體帳戶使用儲存體總管。 

如果您尚未安裝儲存體總管，請[下載](http://www.storageexplorer.com/)並安裝它。

連接 tooyour 堆疊 Azure 訂用帳戶之後，您可以使用 hello [Azure 儲存體總管文章](../vs-azure-tools-storage-manage-with-storage-explorer.md)toowork 與您 Azure 堆疊的資料。 

## <a name="prepare-an-azure-stack-subscription"></a>準備 Azure Stack 訂用帳戶

您需要存取 toohello Azure 堆疊主機電腦的桌面] 或 [儲存體總管 tooaccess hello Azure 堆疊訂用帳戶的 VPN 連線。 如何 tooset 設定 VPN 連線 tooAzure 堆疊，請參閱的 toolearn[與 VPN 連線 tooAzure 堆疊](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。

Hello Azure 堆疊開發套件，您需要 tooexport hello Azure 堆疊授權單位的根憑證。

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a>tooexport 然後再匯入 hello Azure 堆疊憑證

1. 開啟`mmc.exe`Azure 堆疊主機電腦上或 VPN 連線 tooAzure 堆疊的本機電腦上。 

2. 在**檔案**，選取**新增/移除嵌入式管理單元**，然後再加入**憑證**toomanage**電腦帳戶**的**本機電腦**。



3. 在 **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** 之下尋找 **AzureStackSelfSignedRootCert**。

    ![透過 mmc.exe 負載 hello Azure 堆疊的根憑證][25]

4. 以滑鼠右鍵按一下 hello 憑證，請選取**所有工作** > **匯出**，然後依照與 hello 指示 tooexport hello 憑證**base-64 編碼 X.509 (。CER)**。  

    hello 匯出的憑證將用於 hello 下一個步驟。
5. 啟動儲存體總管 （預覽），而且如果您看到 hello**連接儲存體 tooAzure**對話方塊方塊中，請將它取消。

6. 在 hello**編輯**功能表上，點太**SSL 憑證**，然後按一下**匯入憑證**。 使用 hello 檔案選擇器對話方塊方塊 toofind 和您匯出 hello 上一個步驟中的 hello 開啟憑證。

    匯入之後，您將會提示的 toorestart 儲存體總管。

    ![Hello 憑證匯入到儲存體總管 （預覽）][27]

現在您已準備好 tooconnect 存放裝置總管 tooan 堆疊 Azure 訂用帳戶。

### <a name="tooconnect-an-azure-stack-subscription"></a>tooconnect 堆疊 Azure 訂用帳戶


1. 儲存體總管 （預覽） 重新啟動之後，請選取 hello**編輯**功能表，然後確定**目標 Azure 堆疊**已選取。 如果未選取，並加以選取，然後重新啟動後，儲存體總管 hello 變更 tootake 效果。 不需要進行此設定，即可相容於 Azure Stack 環境。

    ![確保已選取目標 Azure Stack][28]

7. Hello 左窗格中，選取**管理帳戶**。  
    您已登入 tooare 顯示所有 hello Microsoft 帳戶。

8. tooconnect toohello Azure 堆疊帳戶選取**將帳戶加入**。

    ![新增 Azure Stack 帳戶][29]

9. 在 hello**連接儲存體 tooAzure**對話方塊的  **Azure 環境**，選取**使用 Azure 堆疊環境**，然後按一下**下一步**.

10. toosign hello 與至少一個有效的 Azure 堆疊訂用帳戶相關聯的 Azure 堆疊帳戶，以填入 hello**登入 tooAzure 堆疊環境** 對話方塊。  

    每個欄位的 hello 詳細資料如下所示：

    * **環境名稱**: hello 欄位可以由使用者自訂。
    * **ARM 資源端點**: hello Azure 資源管理員資源端點的範例：

        * 若是雲端操作員：<br> https://adminmanagement.local.azurestack.external   
        * 若是租用戶：<br> https://management.local.azurestack.external
 
    * **租用戶識別碼**：選擇性。 必須指定 hello 目錄時，才指定 hello 值。

12. 您已成功的帳戶登入 Azure 堆疊之後，hello 左的窗格會填入該帳戶相關聯的 hello Azure 堆疊訂閱。 選取您要的 toowork，然後選取 hello Azure 堆疊訂閱**套用**。 (選取或清除 hello**所有訂用帳戶**核取方塊切換全部選取或列出任何 hello Azure 堆疊訂用帳戶。)

    ![選取後填寫 hello 自訂雲端環境 對話方塊中的 hello Azure 堆疊訂用帳戶][30]  
    hello 左的窗格會顯示 hello hello 選取堆疊 Azure 訂閱相關聯的儲存體帳戶。

    ![包含 Azure Stack 訂用帳戶的儲存體帳戶清單][31]

## <a name="next-steps"></a>後續步驟
* [開始使用儲存體總管 (預覽)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)


* toolearn 進一步了解 Azure 儲存體，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
