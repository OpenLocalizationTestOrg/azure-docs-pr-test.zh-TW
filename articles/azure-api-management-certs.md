---
title: "Azure 管理 API 憑證 aaaUpload |Microsoft 文件"
description: "了解 tooupload 在管理 API 的 hello Azure 傳統入口網站的憑證。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>上傳 Azure 管理 API 管理憑證
管理憑證，讓 Azure 提供 tooauthenticate 與 hello 傳統部署模型。 許多程式和工具 （例如 Visual Studio 或 Azure SDK hello） 使用這些憑證 tooautomate 組態和各種 Azure 服務的部署。 

> [!WARNING]
> 請務必小心！ 這些憑證類型允許驗證它們的任何人 toomanage hello 訂用帳戶相關聯。
>
>

如果您想要深入了解 Azure 憑證 (包括如何建立自我簽署憑證)，請參閱 [Azure 雲端服務的憑證概觀](cloud-services/cloud-services-certs-create.md#what-are-management-certificates)。

您也可以使用[Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate 用戶端程式碼用於自動化用途。

## <a name="upload-a-management-certificate"></a>上傳管理憑證
一旦建立管理憑證、 （僅 hello 公開金鑰的.cer 檔案） 您可以將它上傳到 hello 入口網站。 Hello 憑證在 hello 入口網站時，使用相符的憑證 （私密金鑰） 的任何人都可以透過 hello 相關聯的訂用帳戶的 hello 管理 API 和存取 hello 資源與其連接。

1. 登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 按一下**更多服務**在 hello 下方的 Azure 服務清單，然後選取**訂閱**在 hello_一般_服務群組。

    ![[訂用帳戶] 功能表](./media/azure-api-management-certs/subscriptions_menu.png)

3. 請確定 tooselect hello 想 tooassociate hello 憑證與正確的訂用帳戶。     
4. 您已選取 hello 正確的訂用帳戶之後，請按**管理憑證**在 hello_設定_群組。

    ![設定](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. 按 hello**上傳** 按鈕。

    ![憑證頁面的 [上傳]](./media/azure-api-management-certs/certificates_page.png)
6. 填寫 [hello] 對話方塊的資訊，請按**上傳**。

    ![設定](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>後續步驟
有訂用帳戶相關聯的管理憑證之後，您可以 （您已安裝符合憑證在本機的 hello 之後） 以程式設計方式連接 toohello[傳統部署模型 REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx)和自動化hello 也會與該訂用帳戶相關聯的各種 Azure 資源。
