---
title: "aaaHow toouse Azure 函式中的 SendGrid |Microsoft 文件"
description: "示範如何 toouse SendGrid Azure 函式中"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>如何 toouse SendGrid Azure 函式中

## <a name="sendgrid-overview"></a>SendGrid 概觀

Azure 函式支援 SendGrid 輸出繫結 tooenable 幾行程式碼和 SendGrid 帳戶與您函式 toosend 電子郵件訊息。

在 Azure 函式 toouse hello SendGrid API，您必須擁有[SendGrid 帳戶](http://SendGrid.com)。 此外，您還必須有 SendGrid API 金鑰。 登入 tooyour SendGrid 帳戶，然後按一下 **設定**然後**API 金鑰**toogenerate API 金鑰。 請備妥此金鑰，在後續步驟中會用到。

現在您已經準備就緒 toocreate Azure 函式應用程式。

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式 

Azure Functions 應用程式是一或多個 Azure 函式的容器。 Azure Functions 就只是函式。 每個 Azure 函式是繫結的 tooone 觸發程序，這可能會導致 hello 函式 toorun 事件。
每個函式可以包含任意數目的輸入或輸出繫結。 繫結是您可以在函式中使用的服務。 SendGrid 是輸出繫結，您可以使用 toosend 電子郵件。 

1. 登入 Azure 入口網站 toohello 和[建立 Azure 函式應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)或開啟現有的函式應用程式。 
2. 建立 Azure 函式。 tookeep 簡單，它會選擇手動觸發程序和 C#。 

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>設定 SendGrid 供 Azure 函數應用程式中使用

您必須將您的 SendGrid API 金鑰儲存為應用程式設定 toouse 它的函式中。 hello ApiKey 欄位不是您實際的 SendGrid API 金鑰，但設定您的應用程式定義代表實際的 API 金鑰。 如此儲存金鑰是基於安全性，因為這樣會與任何可能簽入原始檔控制的程式碼或檔案分開。

- 在函式應用程式的 [應用程式設定] 中建立 **AppSettings**。

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>設定 SendGrid 輸出繫結

SendGrid 可做為 Azure 函式輸出繫結。 toocreate SendGrid 輸出繫結：

1. 移 toohello**整合**hello Azure 入口網站中的 hello 函式的索引標籤。
2. 按一下**新輸出**toocreate SendGrid 輸出繫結。
3. 填寫 hello **API 金鑰**和**訊息參數名稱**屬性。 如果您想，您可以輸入 hello 其他屬性，或改為將這些程式碼。 這些設定可用來當做預設值。

 ![設定 SendGrid 輸出繫結](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

加入繫結 tooa 函式會建立名為的檔案**function.json**函式的資料夾中。 這個檔案包含所有 hello 相同的資訊，您在看到 hello Azure 函式的**整合**索引標籤上，但採用 Json 格式。 設定 hello **ApiKey**，**訊息**，和**從**欄位建立下列項目在 hello hello **function.json**檔案： 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

想要的話，您可以自行直接修改這個檔案。

既然您已建立和設定 hello 函式應用程式和函式，您可以撰寫 hello 程式碼 toosend 電子郵件。

## <a name="write-code-that-creates-and-sends-email"></a>撰寫程式碼來建立和傳送電子郵件

hello SendGrid API 包含所有 hello 命令，您需要 toocreate 並傳送電子郵件。  

- 取代下列程式碼的 hello hello hello 函式中的程式碼：

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

請注意 hello 第一行包含 hello```#r```參考 hello SendGrid 組件的指示詞。 在這之後，您可以使用```using```陳述式 toomore 輕鬆地存取該命名空間中的 hello 物件。 在 hello 程式碼中建立的執行個體```Mail```， ```Personalization```，和```Content```從 hello SendGrid API 撰寫 hello 電子郵件的物件。 當您傳回 hello 訊息時，SendGrid 傳送該郵件。 

hello 函式的簽章也包含額外的 out 參數的型別```Mail```名為```message```。 輸入和輸出繫結本身在程式碼中以函式參數表示。 

2. 按一下以測試您的程式碼**測試**輸入 hello 訊息和**要求本文** 欄位中，然後按一下 hello**執行** 按鈕。

 ![測試您的程式碼](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. 請檢查電子郵件 tooverify SendGrid 傳送嗨電子郵件。 它應該從步驟 1 中，移至 toohello hello 程式碼中的位址，且包含從 hello hello 訊息**要求本文**。

## <a name="next-steps"></a>後續步驟
本文示範如何 toouse hello SendGrid 服務 toocreate 及傳送電子郵件。 toolearn 進一步了解使用 Azure 函式在您的應用程式，請參閱下列主題中的 hello: 

- [Azure 函式的最佳作法](functions-best-practices.md)列出一些最佳作法 toouse 時建立 Azure 函式。

- [Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。

- [測試 Azure Functions](functions-test-a-function.md) 說明可用於測試函式的各種工具和技巧。