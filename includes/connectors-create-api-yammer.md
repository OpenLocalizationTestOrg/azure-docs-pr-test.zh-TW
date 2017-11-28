### <a name="prerequisites"></a><span data-ttu-id="d34c4-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="d34c4-101">Prerequisites</span></span>
* <span data-ttu-id="d34c4-102">[Yammer](https://www.yammer.com/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="d34c4-102">A [Yammer](https://www.yammer.com/) account</span></span> 

<span data-ttu-id="d34c4-103">您必須先授與邏輯應用程式連接到 Yammer 帳戶的權限，之後才能在邏輯應用程式中使用您的 Yammer 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d34c4-103">Before you can use your Yammer account in a Logic app, you must authorize the Logic app to connect to your Yammer account.</span></span> <span data-ttu-id="d34c4-104">所幸，您可以使用 Azure 入口網站在邏輯應用程式內輕易達成這項作業。</span><span class="sxs-lookup"><span data-stu-id="d34c4-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="d34c4-105">若要授與邏輯應用程式連接到 Yammer 帳戶的權限，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="d34c4-105">Here are the steps to authorize your Logic app to connect to your Yammer account:</span></span>

1. <span data-ttu-id="d34c4-106">若要建立 Yammer 連線，請在邏輯應用程式設計工具中，選取下拉式清單的 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「Yammer」。</span><span class="sxs-lookup"><span data-stu-id="d34c4-106">To create a connection to Yammer, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Yammer* in the search box.</span></span> <span data-ttu-id="d34c4-107">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="d34c4-107">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-1.png)
2. <span data-ttu-id="d34c4-108">如果您之前尚未建立任何 Yammer 連線，系統會提示您提供 Yammer 認證。</span><span class="sxs-lookup"><span data-stu-id="d34c4-108">If you haven't created any connections to Yammer before, you'll get prompted to provide your Yammer credentials.</span></span> <span data-ttu-id="d34c4-109">這些認證會用來授與邏輯應用程式連接並存取 Yammer 帳戶資料的權限：</span><span class="sxs-lookup"><span data-stu-id="d34c4-109">These credentials will be used to authorize your Logic app to connect to, and access your Yammer account's data:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-2.png)
3. <span data-ttu-id="d34c4-110">提供您的 Yammer 使用者名稱和密碼以授與邏輯應用程式權限：</span><span class="sxs-lookup"><span data-stu-id="d34c4-110">Provide your Yammer user name and password to authorize your Logic app:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-3.png)   
4. <span data-ttu-id="d34c4-111">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="d34c4-111">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-4.png)   

