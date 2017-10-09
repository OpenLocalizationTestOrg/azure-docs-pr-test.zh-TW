### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="2d00e-101">在 hello Azure 入口網站中建立新的邏輯 SQL server</span><span class="sxs-lookup"><span data-stu-id="2d00e-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="2d00e-102">按一下 [新增]，搜尋**邏輯伺服器**，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="2d00e-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![搜尋邏輯伺服器](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="2d00e-104">選取 [SQL Server (邏輯伺服器)]</span><span class="sxs-lookup"><span data-stu-id="2d00e-104">Select **SQL server (logical server)**</span></span> 

    ![選取邏輯伺服器](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="2d00e-106">按一下**建立**tooopen hello 新 SQL Server （邏輯伺服器） 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d00e-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="2d00e-107"><kbd>![開啟刀鋒視窗中的邏輯伺服器](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![邏輯伺服器刀鋒視窗](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="2d00e-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="2d00e-108">在 hello SQL Server （邏輯伺服器） 刀鋒視窗中的伺服器名稱 文字方塊中，提供新的邏輯伺服器 hello 的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="2d00e-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="2d00e-109">綠色核取記號指示您提供的名稱有效。</span><span class="sxs-lookup"><span data-stu-id="2d00e-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![新的伺服器名稱](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="2d00e-111">hello 適用於您的新伺服器的完整格式的名稱將會 < your_server_name >。.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="2d00e-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="2d00e-112">在 hello 伺服器系統管理員登入文字方塊中，提供此伺服器 hello SQL 驗證登入的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2d00e-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="2d00e-113">此登入稱為 hello 伺服器主體的登入。</span><span class="sxs-lookup"><span data-stu-id="2d00e-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="2d00e-114">綠色核取記號指示您提供的名稱有效。</span><span class="sxs-lookup"><span data-stu-id="2d00e-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL 管理員登入](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="2d00e-116">在 hello**密碼**和**確認密碼**文字方塊中，提供 hello 伺服器主體的登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="2d00e-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="2d00e-117">綠色核取記號指示您提供的密碼有效。</span><span class="sxs-lookup"><span data-stu-id="2d00e-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL 管理員密碼](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="2d00e-119">選取您擁有的權限 toocreate 物件的訂閱。</span><span class="sxs-lookup"><span data-stu-id="2d00e-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![訂用帳戶](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="2d00e-121">在 hello 資源群組 文字方塊中，選取 **建立新**然後，在 hello 資源群組 文字方塊中，提供 hello 新的資源群組 （您也可以使用現有的資源群組如果您已經建立自己的其中一個） 的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="2d00e-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="2d00e-122">綠色核取記號指示您提供的名稱有效。</span><span class="sxs-lookup"><span data-stu-id="2d00e-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![新的資源群組](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="2d00e-124">在 [hello**位置**] 文字方塊中，選取一個資料中心適當 tooyour 位置-例如"澳洲東部"。</span><span class="sxs-lookup"><span data-stu-id="2d00e-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![伺服器位置](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="2d00e-126">hello 核取方塊**允許 azure 服務 tooaccess 伺服器**此刀鋒視窗上不能變更。</span><span class="sxs-lookup"><span data-stu-id="2d00e-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="2d00e-127">您可以變更此設定在 hello 伺服器防火牆刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="2d00e-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="2d00e-128">如需詳細資訊，請參閱[安全性入門](../articles/sql-database/sql-database-manage-servers-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d00e-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="2d00e-129">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2d00e-129">Click **Create**.</span></span>

    ![建立按鈕](./media/sql-data-warehouse-create-logical-server/create.png)

