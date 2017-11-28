### <a name="prerequisites"></a><span data-ttu-id="663c0-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="663c0-101">Prerequisites</span></span>
* <span data-ttu-id="663c0-102">[Trello](http://trello.com) 帳戶</span><span class="sxs-lookup"><span data-stu-id="663c0-102">A [Trello](http://trello.com) account</span></span> 

<span data-ttu-id="663c0-103">您必須先授與邏輯應用程式連接到 Trello 帳戶的權限，之後才能在邏輯應用程式中使用您的 Trello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="663c0-103">Before you can use your Trello account in a Logic app, you must authorize the Logic app to connect to your Trello account.</span></span> <span data-ttu-id="663c0-104">所幸，您可以使用 Azure 入口網站在邏輯應用程式內輕易達成這項作業。</span><span class="sxs-lookup"><span data-stu-id="663c0-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="663c0-105">若要授與邏輯應用程式連接到 Trello 帳戶的權限，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="663c0-105">Here are the steps to authorize your Logic app to connect to your Trello account:</span></span>

1. <span data-ttu-id="663c0-106">若要建立 Trello 連線，請在邏輯應用程式設計工具中，選取下拉式清單的 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「Trello」。</span><span class="sxs-lookup"><span data-stu-id="663c0-106">To create a connection to Trello, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Trello* in the search box.</span></span> <span data-ttu-id="663c0-107">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="663c0-107">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-trello/trello-1.png)
2. <span data-ttu-id="663c0-108">如果您之前尚未建立任何 Trello 連線，系統會提示您提供 Trello 認證。</span><span class="sxs-lookup"><span data-stu-id="663c0-108">If you haven't created any connections to Trello before, you'll get prompted to provide your Trello credentials.</span></span> <span data-ttu-id="663c0-109">這些認證會用來授與邏輯應用程式連接並存取 Trello 帳戶資料的權限：</span><span class="sxs-lookup"><span data-stu-id="663c0-109">These credentials will be used to authorize your Logic app to connect to, and access your Trello account's data:</span></span>  
   ![](./media/connectors-create-api-trello/trello-2.png) 
3. <span data-ttu-id="663c0-110">現在即可連接至 Trello：</span><span class="sxs-lookup"><span data-stu-id="663c0-110">Allow us to connect to Trello:</span></span>  
   ![](./media/connectors-create-api-trello/trello-3.png)   
4. <span data-ttu-id="663c0-111">提供您的 Trello 使用者名稱和密碼以授與邏輯應用程式權限：</span><span class="sxs-lookup"><span data-stu-id="663c0-111">Provide your Trello user name and password to authorize your Logic app:</span></span>  
   ![](./media/connectors-create-api-trello/trello-4.png)  
5. <span data-ttu-id="663c0-112">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="663c0-112">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-trello/trello-5.png)

