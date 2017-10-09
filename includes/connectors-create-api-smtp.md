### <a name="prerequisites"></a><span data-ttu-id="b1c15-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="b1c15-101">Prerequisites</span></span>
* <span data-ttu-id="b1c15-102">[SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) 帳戶</span><span class="sxs-lookup"><span data-stu-id="b1c15-102">A [SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) account</span></span>  

<span data-ttu-id="b1c15-103">您可以在邏輯應用程式中使用您的 SMTP 帳戶之前，您必須授權 hello 邏輯應用程式 tooconnect tooyour SMTP 帳戶。幸運的是，您可以輕鬆地在 hello Azure 入口網站上的應用程式邏輯中。</span><span class="sxs-lookup"><span data-stu-id="b1c15-103">Before you can use your SMTP account in a logic app, you must authorize hello logic app tooconnect tooyour SMTP account.Fortunately, you can do this easily from within your logic app on hello Azure Portal.</span></span>  

<span data-ttu-id="b1c15-104">以下是 hello 步驟 tooauthorize 邏輯應用程式 tooconnect tooyour SMTP 帳戶：</span><span class="sxs-lookup"><span data-stu-id="b1c15-104">Here are hello steps tooauthorize your logic app tooconnect tooyour SMTP account:</span></span>  

1. <span data-ttu-id="b1c15-105">toocreate 連接 tooSMTP，在 hello 邏輯應用程式設計師中，選取**顯示 Microsoft managed Api** hello 在下拉式清單，然後輸入*SMTP* hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="b1c15-105">toocreate a connection tooSMTP, in hello logic app designer, select **Show Microsoft managed APIs** in hello drop down list then enter *SMTP* in hello search box.</span></span> <span data-ttu-id="b1c15-106">選取 hello 觸發程序或您一定會喜歡 toouse 的動作：</span><span class="sxs-lookup"><span data-stu-id="b1c15-106">Select hello trigger or action you'll like toouse:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-1.png)  
2. <span data-ttu-id="b1c15-107">如果您尚未建立任何連線 tooSMTP 之前，您會取得提示的 tooprovide SMTP 認證。</span><span class="sxs-lookup"><span data-stu-id="b1c15-107">If you haven't created any connections tooSMTP before, you'll get prompted tooprovide your SMTP credentials.</span></span> <span data-ttu-id="b1c15-108">這些認證會使用的 tooauthorize，您的邏輯應用程式 tooconnect 並存取您的 SMTP 帳戶資料：</span><span class="sxs-lookup"><span data-stu-id="b1c15-108">These credentials will be used tooauthorize your logic app tooconnect to, and access your SMTP account's data:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-2.png)  
3. <span data-ttu-id="b1c15-109">請注意，已經建立 hello 連接，而且現在可用以 hello 其他 tooproceed 邏輯應用程式中的步驟：</span><span class="sxs-lookup"><span data-stu-id="b1c15-109">Notice hello connection has been created and you are now free tooproceed with hello other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-3.png)  

