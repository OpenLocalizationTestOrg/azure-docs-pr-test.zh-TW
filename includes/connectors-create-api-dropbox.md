### <a name="prerequisites"></a><span data-ttu-id="da66e-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="da66e-101">Prerequisites</span></span>
* <span data-ttu-id="da66e-102">[Dropbox](https://www.Dropbox.com/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="da66e-102">A [Dropbox](https://www.Dropbox.com/) account</span></span> 

<span data-ttu-id="da66e-103">您必須先授與邏輯應用程式連接到 Dropbox 帳戶的權限，之後才能在邏輯應用程式中使用您的 Dropbox 帳戶。</span><span class="sxs-lookup"><span data-stu-id="da66e-103">Before you can use your Dropbox account in a Logic app, you must authorize the Logic app to connect to your Dropbox account.</span></span> <span data-ttu-id="da66e-104">所幸，您可以使用 Azure 入口網站在邏輯應用程式內輕易達成這項作業。</span><span class="sxs-lookup"><span data-stu-id="da66e-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="da66e-105">若要授與邏輯應用程式連接到 Dropbox 帳戶的權限，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="da66e-105">Here are the steps to authorize your Logic app to connect to your Dropbox account:</span></span>

1. <span data-ttu-id="da66e-106">若要建立 Dropbox 連線，請在邏輯應用程式設計工具中，選取下拉式清單的 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「Dropbox」。</span><span class="sxs-lookup"><span data-stu-id="da66e-106">To create a connection to Dropbox, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Dropbox* in the search box.</span></span> <span data-ttu-id="da66e-107">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="da66e-107">Select the trigger or action you'll like to use:</span></span>  
   <span data-ttu-id="da66e-108">![Dropbox 步驟 1](./media/connectors-create-api-dropbox/dropbox-1.png)</span><span class="sxs-lookup"><span data-stu-id="da66e-108">![Dropbox step 1](./media/connectors-create-api-dropbox/dropbox-1.png)</span></span>
2. <span data-ttu-id="da66e-109">如果您之前尚未建立任何 Dropbox 連線，系統會提示您提供 Dropbox 認證。</span><span class="sxs-lookup"><span data-stu-id="da66e-109">If you haven't created any connections to Dropbox before, you'll get prompted to provide your Dropbox credentials.</span></span> <span data-ttu-id="da66e-110">這些認證會用來授與邏輯應用程式連接並存取 Dropbox 帳戶資料的權限：</span><span class="sxs-lookup"><span data-stu-id="da66e-110">These credentials will be used to authorize your Logic app to connect to, and access your Dropbox account's data:</span></span>  
   ![Dropbox 步驟 2](./media/connectors-create-api-dropbox/dropbox-2.png)
3. <span data-ttu-id="da66e-112">提供您的 Dropbox 使用者名稱和密碼以授與邏輯應用程式權限：</span><span class="sxs-lookup"><span data-stu-id="da66e-112">Provide your Dropbox user name and password to authorize your Logic app:</span></span>  
   ![Dropbox 步驟 3](./media/connectors-create-api-dropbox/dropbox-3.png)   
4. <span data-ttu-id="da66e-114">授與邏輯應用程式使用 Dropbox 帳戶的權限：</span><span class="sxs-lookup"><span data-stu-id="da66e-114">Authorize the Logic app to use your Dropbox account:</span></span>  
   ![Dropbox 步驟 4](./media/connectors-create-api-dropbox/dropbox-4.png)
5. <span data-ttu-id="da66e-116">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="da66e-116">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![Dropbox 步驟 5](./media/connectors-create-api-dropbox/dropbox-5.png)   

