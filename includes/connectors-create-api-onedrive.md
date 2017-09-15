#### <a name="prerequisites"></a><span data-ttu-id="fdcad-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="fdcad-101">Prerequisites</span></span>
* <span data-ttu-id="fdcad-102">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="fdcad-102">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="fdcad-103">[OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) 帳戶</span><span class="sxs-lookup"><span data-stu-id="fdcad-103">A [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) account</span></span> 

<span data-ttu-id="fdcad-104">您必須先授權邏輯應用程式連線到您的 OneDrive 帳戶，才能在該邏輯應用程式中使用您的 OneDrive 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdcad-104">Before you can use your OneDrive account in a logic app, authorize the logic app to connect to your OneDrive account.</span></span>  <span data-ttu-id="fdcad-105">您可以在 Azure 入口網站上，從邏輯應用程式內輕鬆完成此操作。</span><span class="sxs-lookup"><span data-stu-id="fdcad-105">You can do this easily within your logic app on the Azure portal.</span></span> 

<span data-ttu-id="fdcad-106">使用以下步驟授權邏輯應用程式連接到 OneDrive 帳戶的權限：</span><span class="sxs-lookup"><span data-stu-id="fdcad-106">Authorize your logic app to connect to your OneDrive account using the following steps:</span></span>

1. <span data-ttu-id="fdcad-107">建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdcad-107">Create a logic app.</span></span> <span data-ttu-id="fdcad-108">在 Logic Apps 設計工具中，從下拉式清單中選取 [顯示 Microsoft Managed API]，然後在搜尋方塊中輸入 "onedrive"。</span><span class="sxs-lookup"><span data-stu-id="fdcad-108">In the Logic Apps designer, select **Show Microsoft managed APIs** in the drop down list, and then enter "onedrive" in the search box.</span></span> <span data-ttu-id="fdcad-109">選取其中一個觸發程序或動作︰</span><span class="sxs-lookup"><span data-stu-id="fdcad-109">Select one of the triggers or actions:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="fdcad-110">如果您之前尚未對 OneDrive 建立任何連線，系統會提示您使用 OneDrive 認證來登入：</span><span class="sxs-lookup"><span data-stu-id="fdcad-110">If you haven't previously created any connections to OneDrive, you are prompted to sign in using your OneDrive credentials:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-2.png)
3. <span data-ttu-id="fdcad-111">選取 [登入]，然後輸入您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="fdcad-111">Select **Sign in**, and enter your user name and password.</span></span> <span data-ttu-id="fdcad-112">選取 [登入]：</span><span class="sxs-lookup"><span data-stu-id="fdcad-112">Select **Sign in**:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-3.png)   
   
    <span data-ttu-id="fdcad-113">這些認證會用來授權邏輯應用程式連線到您的 OneDrive 帳戶，以及存取該帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="fdcad-113">These credentials are used to authorize your logic app to connect to, and access the data in your OneDrive account.</span></span> 
4. <span data-ttu-id="fdcad-114">選取 [是] 以授權邏輯應用程式使用您的 OneDrive 帳戶︰</span><span class="sxs-lookup"><span data-stu-id="fdcad-114">Select **Yes** to authorize the logic app to use your OneDrive account:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-4.png)   
5. <span data-ttu-id="fdcad-115">請注意，已建立連線。</span><span class="sxs-lookup"><span data-stu-id="fdcad-115">Notice the connection has been created.</span></span> <span data-ttu-id="fdcad-116">現在，請繼續進行您邏輯應用程式中的其他步驟：</span><span class="sxs-lookup"><span data-stu-id="fdcad-116">Now, proceed with the other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-5.png)

