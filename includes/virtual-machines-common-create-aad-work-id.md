
<br>

> [!NOTE]
> <span data-ttu-id="e29b5-101">如果系統管理員已提供給您使用者名稱與密碼，很有可能您已經有工作或學校識別碼 (有時也稱做「組織識別碼」)。</span><span class="sxs-lookup"><span data-stu-id="e29b5-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="e29b5-102">如果是這樣，您可以立即開始 toouse 您的 Azure 帳戶 tooaccess 需要其中一個的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e29b5-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="e29b5-103">如果您發現您無法使用這些資源，您可能需要 tooreturn toothis 發行項的說明。</span><span class="sxs-lookup"><span data-stu-id="e29b5-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="e29b5-104">如需詳細資訊，請參閱[您可以使用的帳戶登入](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts)和[如何為 Azure 訂用帳戶已相關的 tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir)。</span><span class="sxs-lookup"><span data-stu-id="e29b5-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="e29b5-105">hello 步驟很簡單。</span><span class="sxs-lookup"><span data-stu-id="e29b5-105">hello steps are simple.</span></span> <span data-ttu-id="e29b5-106">您需要 toolocate 您帶正負號上 hello Azure 傳統入口網站中的身分識別，探索您的預設 Azure Active Directory 網域，並加入新的使用者 tooit 為 Azure 的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="e29b5-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="e29b5-107">在 hello Azure 傳統入口網站中尋找您的預設目錄</span><span class="sxs-lookup"><span data-stu-id="e29b5-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="e29b5-108">開始登入以 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)與您個人的 Microsoft 帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e29b5-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="e29b5-109">在登入後，捲動 hello 左邊的藍色 hello 面板，並按一下**ACTIVE DIRECTORY**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="e29b5-111">讓我們開始在 Azure 中找出您身分識別的部分資訊。</span><span class="sxs-lookup"><span data-stu-id="e29b5-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="e29b5-112">您應該會看到類似下 hello 遵循 hello 主窗格中，顯示您有一個預設目錄。</span><span class="sxs-lookup"><span data-stu-id="e29b5-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="e29b5-113">讓我們找到更多的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e29b5-113">Let's find out some more information about it.</span></span> <span data-ttu-id="e29b5-114">按一下 hello 預設目錄資料列，讓您回到成 hello 預設目錄屬性。</span><span class="sxs-lookup"><span data-stu-id="e29b5-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="e29b5-115">tooview hello 預設網域名稱，按一下 **網域**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="e29b5-116">這裡您應該要建立 hello Azure 帳戶後，Azure Active Directory 建立個人的預設網域的雜湊值 （從文字字串所產生的數字） 可以 toosee 您個人的 id 做為 onmicrosoft.com 的子網域。這是 hello 網域 toowhich 現在要加入新的使用者。</span><span class="sxs-lookup"><span data-stu-id="e29b5-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="e29b5-117">Hello 預設網域中建立新的使用者</span><span class="sxs-lookup"><span data-stu-id="e29b5-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="e29b5-118">按一下 [使用者]，然後尋找您的單一個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="e29b5-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="e29b5-119">您應該會看到在 hello**源自**資料行，它是**Microsoft 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="e29b5-120">我們希望 toocreate 中預設的使用者。 Azure Active Directory 的 onmicrosoft.com 網域。</span><span class="sxs-lookup"><span data-stu-id="e29b5-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="e29b5-121">我們會 toofollow[這些指示](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1)在 hello 接下來的步驟，但使用特定的範例。</span><span class="sxs-lookup"><span data-stu-id="e29b5-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="e29b5-122">在 hello hello 頁面底部，按一下**+ 新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="e29b5-123">在出現的 hello 頁面上，輸入 hello 新的使用者名稱，並讓 hello**使用者類型****您組織中的新使用者**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="e29b5-124">此範例中的 hello 新的使用者名稱是`ahmet`。</span><span class="sxs-lookup"><span data-stu-id="e29b5-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="e29b5-125">選取您所探索的 hello 預設網域先前做為 hello ahmet 的電子郵件地址的網域。</span><span class="sxs-lookup"><span data-stu-id="e29b5-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="e29b5-126">按一下 完成 hello 下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="e29b5-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="e29b5-127">Ahmet，加入更多詳細資料，但請確定 tooselect hello 適當**角色**值。</span><span class="sxs-lookup"><span data-stu-id="e29b5-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="e29b5-128">它是簡單 toouse**全域管理員**正在 toomake 確定項目，但如果您可以使用較小者的角色，這是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="e29b5-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="e29b5-129">這個範例會使用 hello**使用者**角色。</span><span class="sxs-lookup"><span data-stu-id="e29b5-129">This example uses hello **User** role.</span></span> <span data-ttu-id="e29b5-130">(在[依據角色的系統管理員權限](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)中取得更多資訊。)請勿啟用多重要素驗證，除非您想 toouse 多重要素驗證每個記錄檔中作業。</span><span class="sxs-lookup"><span data-stu-id="e29b5-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="e29b5-131">當您完成時，請按一下 hello 下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="e29b5-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="e29b5-132">按一下 hello**建立**按鈕 toogenerate 和 Ahmet 顯示暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="e29b5-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="e29b5-133">複製 hello 使用者名稱的電子郵件地址，或使用**傳送密碼在電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="e29b5-134">您稍後將需要 hello 資訊 toolog 上。</span><span class="sxs-lookup"><span data-stu-id="e29b5-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="e29b5-135">現在您應該會看到新的使用者，hello **Ahmet hello 開發人員**、 從 Azure Active Directory 來源。</span><span class="sxs-lookup"><span data-stu-id="e29b5-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="e29b5-136">您已建立 hello 新的工作或學校身分識別與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="e29b5-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="e29b5-137">不過，這個身分識別還沒有權限 toouse Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e29b5-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="e29b5-138">如果您使用**傳送密碼在電子郵件**，會傳送 hello 下列種類的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e29b5-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="e29b5-139">為訂用帳戶新增 Azure 的共同管理員權限</span><span class="sxs-lookup"><span data-stu-id="e29b5-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="e29b5-140">現在您需要 tooadd hello 新使用者訂用帳戶的共同管理員身分讓 hello 新的使用者可以登入 toohello 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="e29b5-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="e29b5-141">在 [hello] 面板左下方按一下的 toodo**設定**。</span><span class="sxs-lookup"><span data-stu-id="e29b5-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="e29b5-142">在 hello 主要設定 區域中，按一下 **管理員**在 hello 頂端，而且您應該會看到只有您個人 Microsoft 帳戶的身分識別。</span><span class="sxs-lookup"><span data-stu-id="e29b5-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="e29b5-143">在 hello hello 頁面底部，按一下**+ 加入**toospecify 共同管理員。</span><span class="sxs-lookup"><span data-stu-id="e29b5-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="e29b5-144">在這裡，輸入 hello hello 您建立，包括您的預設網域的新使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e29b5-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="e29b5-145">Hello 的下一個螢幕擷取畫面所示，綠色的核取記號會出現 下一步 toohello 使用者 hello 預設目錄。</span><span class="sxs-lookup"><span data-stu-id="e29b5-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="e29b5-146">請記住 tooselect 所有您想要此使用者 toobe 無法 tooadminister hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e29b5-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="e29b5-147">完成後，您現在應會看到兩個使用者，包括新的共同管理員身分識別。</span><span class="sxs-lookup"><span data-stu-id="e29b5-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="e29b5-148">登出 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e29b5-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="e29b5-149">登入並變更 hello 新使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="e29b5-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="e29b5-150">Hello 建立新的使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="e29b5-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="e29b5-151">您會立即提示的 toocreate 新密碼。</span><span class="sxs-lookup"><span data-stu-id="e29b5-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="e29b5-152">您應該看起來像下列 hello 的成功報償。</span><span class="sxs-lookup"><span data-stu-id="e29b5-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="e29b5-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e29b5-153">Next steps</span></span>
<span data-ttu-id="e29b5-154">您現在可以使用您新的 Azure Active Directory 身分識別 toouse [Azure 資源群組範本](../articles/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="e29b5-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
