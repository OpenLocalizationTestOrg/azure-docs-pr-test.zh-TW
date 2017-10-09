
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="5286a-101">登入 toohello [Azure 入口網站](https://portal.azure.com/)http://portal.azure.com/ 在。</span><span class="sxs-lookup"><span data-stu-id="5286a-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="5286a-102">在 hello 左邊的橫幅中，按一下 **瀏覽所有**。</span><span class="sxs-lookup"><span data-stu-id="5286a-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="5286a-103">hello**瀏覽**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="5286a-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="5286a-104">捲動並按一下 [SQL Server] 。</span><span class="sxs-lookup"><span data-stu-id="5286a-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="5286a-105">hello **SQL 伺服器**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="5286a-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Hello 入口網站中尋找您的 Azure SQL Database 伺服器][b21-FindServerInPortal]
4. <span data-ttu-id="5286a-107">為了方便起見，按一下 hello 控制項上稍早 hello 最小化**瀏覽**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5286a-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="5286a-108">在 hello 篩選文字方塊中，開始輸入 hello 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="5286a-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="5286a-109">即會顯示您的資料列。</span><span class="sxs-lookup"><span data-stu-id="5286a-109">Your row is displayed.</span></span>
6. <span data-ttu-id="5286a-110">按一下您的伺服器 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="5286a-110">Click hello row for your server.</span></span> <span data-ttu-id="5286a-111">即會顯示您伺服器的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5286a-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="5286a-112">在伺服器刀鋒視窗中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="5286a-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="5286a-113">hello**設定**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="5286a-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="5286a-114">按一下 [防火牆] 。</span><span class="sxs-lookup"><span data-stu-id="5286a-114">Click **Firewall**.</span></span> <span data-ttu-id="5286a-115">hello**防火牆設定**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="5286a-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![按一下 [設定] > [防火牆]。][b31-SettingsFirewallNavig]
9. <span data-ttu-id="5286a-117">按一下 [加入用戶端 IP] 。</span><span class="sxs-lookup"><span data-stu-id="5286a-117">Click **Add Client IP**.</span></span> <span data-ttu-id="5286a-118">Hello 第一個文字方塊中輸入新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="5286a-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="5286a-119">型別在 hello 低和高 IP 位址，針對您想要的 hello 範圍值 tooenable。</span><span class="sxs-lookup"><span data-stu-id="5286a-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="5286a-120">它可以是很方便 toohave hello 低值結尾為**.0**和 hello 與高**.255**。</span><span class="sxs-lookup"><span data-stu-id="5286a-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![新增 IP 位址範圍 tooallow][b41-AddRange]
11. <span data-ttu-id="5286a-122">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5286a-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
