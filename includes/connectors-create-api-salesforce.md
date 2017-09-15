### <a name="prerequisites"></a><span data-ttu-id="80e7a-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="80e7a-101">Prerequisites</span></span>
* <span data-ttu-id="80e7a-102">[Salesforce](https://salesforce.com) 帳戶</span><span class="sxs-lookup"><span data-stu-id="80e7a-102">A [Salesforce](https://salesforce.com) account</span></span>  

<span data-ttu-id="80e7a-103">您必須先授權邏輯應用程式連線到您的 Salesforce 帳戶，才能在該邏輯應用程式中使用您的 Salesforce 帳戶。幸運的是，您可以在「Azure 入口網站」上，從邏輯應用程式內輕鬆完成此操作。</span><span class="sxs-lookup"><span data-stu-id="80e7a-103">Before you can use your Salesforce account in a logic app, you must authorize the logic app to connect to your Salesforce account.Fortunately, you can do this easily from within your logic app on the Azure Portal.</span></span>  

<span data-ttu-id="80e7a-104">若要授權邏輯應用程式連線到您的 Salesforce 帳戶，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="80e7a-104">Here are the steps to authorize your logic app to connect to your Salesforce account:</span></span>  

1. <span data-ttu-id="80e7a-105">若要建立與 Salesforce 的連線，請在邏輯應用程式設計工具中，從下拉式清單中選取 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「Salesforce」。</span><span class="sxs-lookup"><span data-stu-id="80e7a-105">To create a connection to Salesforce, in the logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Salesforce* in the search box.</span></span> <span data-ttu-id="80e7a-106">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="80e7a-106">Select the trigger or action you'll like to use:</span></span>  
   <span data-ttu-id="80e7a-107">![Salesforce 連線圖像 1](./media/connectors-create-api-salesforce/salesforce-1.png)</span><span class="sxs-lookup"><span data-stu-id="80e7a-107">![Salesforce connection image 1](./media/connectors-create-api-salesforce/salesforce-1.png)</span></span>  
2. <span data-ttu-id="80e7a-108">如果您之前尚未建立任何 Salesforce 連接，系統會提示您提供 Salesforce 認證。</span><span class="sxs-lookup"><span data-stu-id="80e7a-108">If you haven't created any connections to Salesforce before, you'll get prompted to provide your Salesforce credentials.</span></span> <span data-ttu-id="80e7a-109">這些認證將用來授權邏輯應用程式連線及存取您 Salesforce 帳戶的資料：</span><span class="sxs-lookup"><span data-stu-id="80e7a-109">These credentials will be used to authorize your logic app to connect to, and access your Salesforce account's data:</span></span>  
   ![Salesforce 連線圖像 2](./media/connectors-create-api-salesforce/salesforce-2.png)  
3. <span data-ttu-id="80e7a-111">提供您的 Salesforce 使用者名稱和密碼來授權邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="80e7a-111">Provide your Salesforce user name and password to authorize your logic app:</span></span>  
   ![Salesforce 連線圖像 3](./media/connectors-create-api-salesforce/salesforce-3.png)  
4. <span data-ttu-id="80e7a-113">允許我們連線到 Salesforce：</span><span class="sxs-lookup"><span data-stu-id="80e7a-113">Allow us to connect to Salesforce:</span></span>  
   ![Salesforce 連線圖像 4](./media/connectors-create-api-salesforce/salesforce-4.png)  
5. <span data-ttu-id="80e7a-115">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="80e7a-115">Notice the connection has been created and you are now free to proceed with the other steps in your logic app:</span></span>  
   ![Salesforce 連線圖像 5](./media/connectors-create-api-salesforce/salesforce-5.png)  

