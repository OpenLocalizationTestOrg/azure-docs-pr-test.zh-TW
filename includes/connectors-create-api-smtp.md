### <a name="prerequisites"></a><span data-ttu-id="3a635-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="3a635-101">Prerequisites</span></span>
* <span data-ttu-id="3a635-102">[SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) 帳戶</span><span class="sxs-lookup"><span data-stu-id="3a635-102">A [SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) account</span></span>  

<span data-ttu-id="3a635-103">您必須先授權邏輯應用程式連線到您的 SMTP 帳戶，才能在該邏輯應用程式中使用您的 SMTP 帳戶。幸運的是，您可以在「Azure 入口網站」上，從邏輯應用程式內輕鬆完成此操作。</span><span class="sxs-lookup"><span data-stu-id="3a635-103">Before you can use your SMTP account in a logic app, you must authorize the logic app to connect to your SMTP account.Fortunately, you can do this easily from within your logic app on the Azure Portal.</span></span>  

<span data-ttu-id="3a635-104">若要授權邏輯應用程式連線到您的 SMTP 帳戶，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="3a635-104">Here are the steps to authorize your logic app to connect to your SMTP account:</span></span>  

1. <span data-ttu-id="3a635-105">若要建立與 SMTP 的連線，請在邏輯應用程式設計工具中，從下拉式清單中選取 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「SMTP」。</span><span class="sxs-lookup"><span data-stu-id="3a635-105">To create a connection to SMTP, in the logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *SMTP* in the search box.</span></span> <span data-ttu-id="3a635-106">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="3a635-106">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-1.png)  
2. <span data-ttu-id="3a635-107">如果您之前尚未建立任何 SMTP 連線，系統會提示您提供 SMTP 認證。</span><span class="sxs-lookup"><span data-stu-id="3a635-107">If you haven't created any connections to SMTP before, you'll get prompted to provide your SMTP credentials.</span></span> <span data-ttu-id="3a635-108">這些認證將用來授權邏輯應用程式連線及存取您 SMTP 帳戶的資料：</span><span class="sxs-lookup"><span data-stu-id="3a635-108">These credentials will be used to authorize your logic app to connect to, and access your SMTP account's data:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-2.png)  
3. <span data-ttu-id="3a635-109">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="3a635-109">Notice the connection has been created and you are now free to proceed with the other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-3.png)  

