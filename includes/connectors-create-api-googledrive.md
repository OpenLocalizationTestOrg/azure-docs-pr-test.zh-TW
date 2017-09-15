### <a name="prerequisites"></a><span data-ttu-id="39a39-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="39a39-101">Prerequisites</span></span>
* <span data-ttu-id="39a39-102">[GoogleDrive](https://www.google.com/drive/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="39a39-102">A [GoogleDrive](https://www.google.com/drive/) account</span></span>  

<span data-ttu-id="39a39-103">您必須先授權邏輯應用程式連接到您的 GoogleDrive 帳戶，才可以在邏輯應用程式中使用您的 GoogleDrive 帳戶。幸運的是，您可以輕鬆地在 Azure 入口網站上從邏輯應用程式內完成。</span><span class="sxs-lookup"><span data-stu-id="39a39-103">Before you can use your GoogleDrive account in a Logic app, you must authorize the Logic app to connect to your GoogleDrive account.Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span>  

<span data-ttu-id="39a39-104">若要授與邏輯應用程式連接到 GoogleDrive 帳戶的權限，其步驟如下：</span><span class="sxs-lookup"><span data-stu-id="39a39-104">Here are the steps to authorize your Logic app to connect to your GoogleDrive account:</span></span>  

1. <span data-ttu-id="39a39-105">若要建立 GoogleDrive 連接，請在邏輯應用程式設計工具的下拉式清單中選取 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入「GoogleDrive」。</span><span class="sxs-lookup"><span data-stu-id="39a39-105">To create a connection to GoogleDrive, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *GoogleDrive* in the search box.</span></span> <span data-ttu-id="39a39-106">選取您要使用的觸發程序或動作：</span><span class="sxs-lookup"><span data-stu-id="39a39-106">Select the trigger or action you'll like to use:</span></span>  
   <span data-ttu-id="39a39-107">![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-1.png)</span><span class="sxs-lookup"><span data-stu-id="39a39-107">![GoogleDrive connection creation step](./media/connectors-create-api-googledrive/googledrive-1.png)</span></span>  
2. <span data-ttu-id="39a39-108">如果您之前尚未建立任何 GoogleDrive 連接，系統會提示您提供 GoogleDrive 認證。</span><span class="sxs-lookup"><span data-stu-id="39a39-108">If you haven't created any connections to GoogleDrive before, you'll get prompted to provide your GoogleDrive credentials.</span></span> <span data-ttu-id="39a39-109">這些認證會用來授與邏輯應用程式連接並存取 GoogleDrive 帳戶資料的權限：</span><span class="sxs-lookup"><span data-stu-id="39a39-109">These credentials will be used to authorize your Logic app to connect to, and access your GoogleDrive account's data:</span></span>  
   ![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-2.png)  
3. <span data-ttu-id="39a39-111">提供您的 GoogleDrive 電子郵件地址︰</span><span class="sxs-lookup"><span data-stu-id="39a39-111">Provide your GoogleDrive email address:</span></span>  
   ![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-3.png)  
4. <span data-ttu-id="39a39-113">提供您的 GoogleDrive 密碼以授與邏輯應用程式權限：</span><span class="sxs-lookup"><span data-stu-id="39a39-113">Provide your GoogleDrive password to authorize your Logic app:</span></span>  
   ![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-4.png)
5. <span data-ttu-id="39a39-115">允許連接至 GoogleDrive</span><span class="sxs-lookup"><span data-stu-id="39a39-115">Allow the connection to GoogleDrive</span></span>  
   ![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-5.png)  
6. <span data-ttu-id="39a39-117">請注意，此時已建立連接，您現可進行邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="39a39-117">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![GoogleDrive 連接的建立步驟](./media/connectors-create-api-googledrive/googledrive-6.png)  

