1. <span data-ttu-id="d6265-101">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="d6265-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="d6265-102">如需有關登入的詳細資訊，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d6265-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="d6265-103">如果您有多個 Azure 訂用帳戶，列出 hello 訂閱 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6265-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="d6265-104">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6265-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```