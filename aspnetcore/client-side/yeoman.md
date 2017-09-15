---
title: "ASP.NET Core で Yeoman でプロジェクトをビルドします。"
author: spboyer
description: "この記事の内容が ASP.NET Core、Yeoman を使用して web アプリケーションの作成過程 macos ジェネレーター。"
keywords: "ASP.NET Core、Yeoman、クロス プラットフォーム yo aspnet"
ms.author: spboyer
manager: wpickett
ms.date: 07/05/2017
ms.topic: article
ms.assetid: fda0c2a8-1743-4505-be1a-7f8ceeef8647
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/yeoman
ms.openlocfilehash: 61561b55774faf375090c92b574a64f1a12f9647
ms.sourcegitcommit: 9cdbfd0d670d70b9c354216aabee260c52dad5ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2017
---
# <a name="introduction-to-building-projects-with-yeoman-in-aspnet-core"></a><span data-ttu-id="e2332-104">ASP.NET Core で Yeoman とプロジェクトのビルドの概要</span><span class="sxs-lookup"><span data-stu-id="e2332-104">Introduction to building projects with Yeoman in ASP.NET Core</span></span>

<span data-ttu-id="e2332-105">[Yeoman](http://yeoman.io/)は、さまざまなアプリケーションを作成するためのプロジェクトのスキャフォールディング システムです。</span><span class="sxs-lookup"><span data-stu-id="e2332-105">[Yeoman](http://yeoman.io/) is a project scaffolding system for creating many kinds of applications.</span></span> <span data-ttu-id="e2332-106">Yeoman ASP.NET Core のジェネレーターには、さまざまな新しい web、MVC、またはコンソール アプリケーションを起動するためのプロジェクト テンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e2332-106">The Yeoman generator for ASP.NET Core contains a variety of project templates for starting a new web, MVC, or console application.</span></span>

## <a name="install-nodejs-npm-and-yeoman"></a><span data-ttu-id="e2332-107">Node.js、npm、および Yeoman をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e2332-107">Install Node.js, npm, and Yeoman</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e2332-108">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="e2332-108">Prerequisites</span></span>

<span data-ttu-id="e2332-109">Node.js と npm Yeoman に必要です。</span><span class="sxs-lookup"><span data-stu-id="e2332-109">Node.js and npm are required for Yeoman.</span></span> <span data-ttu-id="e2332-110">ダウンロード[Node.js](https://nodejs.org/)です。</span><span class="sxs-lookup"><span data-stu-id="e2332-110">Download from [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="e2332-111">インストーラーが含まれています[Node.js](https://nodejs.org/)と[npm](https://www.npmjs.com/)です。</span><span class="sxs-lookup"><span data-stu-id="e2332-111">The installer includes [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/).</span></span> <span data-ttu-id="e2332-112">Bower ものブートス トラップのような UI フレームワークのインストールに必要です。</span><span class="sxs-lookup"><span data-stu-id="e2332-112">Bower is also required for installing UI frameworks like Bootstrap.</span></span>

<span data-ttu-id="e2332-113">Yeoman と Bower をインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-113">To install Yeoman and Bower, run the following command:</span></span>

```console
npm install -g yo bower
```

>[!Note]
><span data-ttu-id="e2332-114">エラーが発生した場合`npm ERR! Please try running this command again as root/Administrator.`macOS などで、次のコマンドを使用して、実行[sudo](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man8/sudo.8.html):`sudo npm install -g yo bower`</span><span class="sxs-lookup"><span data-stu-id="e2332-114">If you get the error `npm ERR! Please try running this command again as root/Administrator.` on macOS, run the following command using [sudo](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man8/sudo.8.html): `sudo npm install -g yo bower`</span></span>

<span data-ttu-id="e2332-115">コマンド プロンプトから、ASP.NET コード ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e2332-115">From a command prompt, install the ASP.NET generator:</span></span>

```console
npm install -g generator-aspnet
```

> [!NOTE]
> <span data-ttu-id="e2332-116">アクセス許可のエラーが発生した場合は、下にあるコマンドを実行`sudo`前述のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e2332-116">If you get a permission error, run the command under `sudo` as described above.</span></span>

<span data-ttu-id="e2332-117">`–g`フラグ インストール ジェネレーター グローバルに、任意のパスから使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e2332-117">The `–g` flag installs the generator globally, so that it can be used from any path.</span></span>

## <a name="create-an-aspnet-app"></a><span data-ttu-id="e2332-118">ASP.NET アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="e2332-118">Create an ASP.NET app</span></span>

<span data-ttu-id="e2332-119">Yeoman ベースの ASP.NET コード ジェネレーターを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-119">Run the Yeoman-based ASP.NET generator:</span></span>

```console
yo aspnet
```

<span data-ttu-id="e2332-120">ジェネレーターには、メニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e2332-120">The generator displays a menu.</span></span> <span data-ttu-id="e2332-121">下にある矢印、 **Web アプリケーション基本 [せず、メンバーシップと承認]**プロジェクトの順にタップ**Enter**:</span><span class="sxs-lookup"><span data-stu-id="e2332-121">Arrow down to the **Web Application Basic [without Membership and Authorization]** project and tap **Enter**:</span></span>

![コマンド ウィンドウ: を作成するアプリケーションの種類か。](yeoman/_static/yeoman-yo-aspnet.png)

<span data-ttu-id="e2332-124">UI フレームワークとしてブートス トラップを選択し、タップ**Enter**です。</span><span class="sxs-lookup"><span data-stu-id="e2332-124">Select Bootstrap as the UI Framework and tap **Enter**.</span></span>

<span data-ttu-id="e2332-125">使用して"**MyWebApp**"アプリ名と順にタップ**Enter**です。</span><span class="sxs-lookup"><span data-stu-id="e2332-125">Use "**MyWebApp**" for the app name and then tap **Enter**.</span></span>

<span data-ttu-id="e2332-126">Yeoman には、プロジェクトとそのサポート ファイルがスキャフォールディングされます。</span><span class="sxs-lookup"><span data-stu-id="e2332-126">Yeoman will scaffold the project and its supporting files.</span></span> <span data-ttu-id="e2332-127">推奨される次の手順は、コマンドの形式でも提供されます。</span><span class="sxs-lookup"><span data-stu-id="e2332-127">Suggested next steps are also provided in the form of commands.</span></span>

![コマンド ウィンドウ: ASP.NET アプリケーションの名前は何ですか。](yeoman/_static/yeoman-yo-aspnet-created.png)

<span data-ttu-id="e2332-130">[ASP.NET ジェネレーター](https://www.npmjs.com/package/generator-aspnet) ASP.NET Core を Visual Studio のコードを Visual Studio に読み込まれることができますか、コマンドラインから実行するプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e2332-130">The [ASP.NET generator](https://www.npmjs.com/package/generator-aspnet) creates ASP.NET Core projects that can be loaded into Visual Studio Code, Visual Studio, or run from the command line.</span></span>

## <a name="restore-build-and-run"></a><span data-ttu-id="e2332-131">復元、ビルド、および実行</span><span class="sxs-lookup"><span data-stu-id="e2332-131">Restore, build, and run</span></span>

<span data-ttu-id="e2332-132">次のディレクトリを変更することで、推奨されるコマンド、`MyWebApp`ディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="e2332-132">Follow the suggested commands by changing directories to the `MyWebApp` directory.</span></span> <span data-ttu-id="e2332-133">実行して`dotnet restore`です。</span><span class="sxs-lookup"><span data-stu-id="e2332-133">Then run `dotnet restore`.</span></span>

![[コマンド] ウィンドウ](yeoman/_static/dotnet-restore.png)

<span data-ttu-id="e2332-135">ビルドおよび実行するアプリを使用して、`dotnet build`と`dotnet run`:</span><span class="sxs-lookup"><span data-stu-id="e2332-135">Build and run the app using `dotnet build` and `dotnet run`:</span></span>

![[コマンド] ウィンドウ](yeoman/_static/dotnet-build-run.png)

<span data-ttu-id="e2332-137">この時点では、アプリをテストする、新しく作成された ASP.NET Core 表示される URL に移動することができます。</span><span class="sxs-lookup"><span data-stu-id="e2332-137">At this point, you can navigate to the URL shown to test the newly-created ASP.NET Core app.</span></span>

## <a name="client-side-packages"></a><span data-ttu-id="e2332-138">クライアント側のパッケージ</span><span class="sxs-lookup"><span data-stu-id="e2332-138">Client-side packages</span></span>

<span data-ttu-id="e2332-139">フロント エンド サーバーのリソースは、Yeoman から、テンプレートによって提供されるジェネレーターを使用して、 [Bower](xref:client-side/bower)クライアント側のパッケージ マネージャーを追加する*bower.json*と*.bowerrc*Bower を使用してクライアント側のパッケージを復元するファイル。</span><span class="sxs-lookup"><span data-stu-id="e2332-139">The front-end resources are provided by the templates from the Yeoman generator using the [Bower](xref:client-side/bower) client-side package manager, adding *bower.json* and *.bowerrc* files to restore client-side packages using Bower.</span></span>

<span data-ttu-id="e2332-140">[BundlerMinifier](xref:client-side/bundling-and-minification)コンポーネントが既定では、使いやすさ (バンドル) を連結したものと CSS、JavaScript、および HTML の縮小も含まれています。</span><span class="sxs-lookup"><span data-stu-id="e2332-140">The [BundlerMinifier](xref:client-side/bundling-and-minification) component is also included by default for ease of concatenation (bundling) and minification of CSS, JavaScript, and HTML.</span></span>

## <a name="building-and-running-from-visual-studio"></a><span data-ttu-id="e2332-141">ビルドと Visual Studio から実行</span><span class="sxs-lookup"><span data-stu-id="e2332-141">Building and running from Visual Studio</span></span>

<span data-ttu-id="e2332-142">Visual Studio に直接生成された ASP.NET Core web プロジェクトを読み込むをビルドし、そこから、プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-142">You can load your generated ASP.NET Core web project directly into Visual Studio, then build and run your project from there.</span></span> <span data-ttu-id="e2332-143">Yeoman を使用して、新しい ASP.NET Core アプリケーションをスキャフォールディングするには、上記の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="e2332-143">Follow the instructions above to scaffold a new ASP.NET Core app using Yeoman.</span></span> <span data-ttu-id="e2332-144">このとき、選択**Web アプリケーション**メニューと、アプリの名前から`MyWebApp`です。</span><span class="sxs-lookup"><span data-stu-id="e2332-144">This time, choose **Web Application** from the menu and name the app `MyWebApp`.</span></span>

<span data-ttu-id="e2332-145">Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="e2332-145">Open Visual Studio.</span></span> <span data-ttu-id="e2332-146">[ファイル] メニューから開く ‣ プロジェクト/ソリューションを選択します。</span><span class="sxs-lookup"><span data-stu-id="e2332-146">From the File menu, select Open ‣ Project/Solution.</span></span>

<span data-ttu-id="e2332-147">プロジェクトを開くダイアログ ボックスに移動、 *.csproj*ファイルを選択し、をクリックして、**開く**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e2332-147">In the Open Project dialog, navigate to the *.csproj* file, select it, and click the **Open** button.</span></span> <span data-ttu-id="e2332-148">ソリューション エクスプ ローラーで、プロジェクトはようになります次のスクリーン ショット。</span><span class="sxs-lookup"><span data-stu-id="e2332-148">In the Solution Explorer, the project should look something like the screenshot below.</span></span>

![ソリューション エクスプ ローラーで新しいプロジェクトのファイルとフォルダー](yeoman/_static/yeoman-solution.png)

<span data-ttu-id="e2332-150">Yeoman scaffolds MVC web アプリケーション、両方を持つ完全なサーバー側とクライアント側のサポートを構築します。</span><span class="sxs-lookup"><span data-stu-id="e2332-150">Yeoman scaffolds a MVC web application, complete with both server- and client-side build support.</span></span> <span data-ttu-id="e2332-151">サーバー側の依存関係が表示されます、**の依存関係/NuGet**ノード、および内のクライアント側の依存関係、**の依存関係/Bower**ソリューション エクスプ ローラーのノードです。</span><span class="sxs-lookup"><span data-stu-id="e2332-151">Server-side dependencies are listed under the **Dependencies/NuGet** node, and client-side dependencies in the **Dependencies/Bower** node of Solution Explorer.</span></span> <span data-ttu-id="e2332-152">依存関係は、プロジェクトが読み込まれるときに自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="e2332-152">Dependencies are restored automatically when the project is loaded.</span></span>

![ソリューション エクスプ ローラーのツリー ビューの依存関係ノードの下、Bower が開いているその依存関係を一覧表示します。](yeoman/_static/yeoman-loading-dependencies.png)

<span data-ttu-id="e2332-154">すべての依存関係を復元すると、キーを押して**f5 キーを押して**プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-154">When all the dependencies are restored, press **F5** to run the project.</span></span> <span data-ttu-id="e2332-155">既定のホーム ページをブラウザーで表示します。</span><span class="sxs-lookup"><span data-stu-id="e2332-155">The default home page displays in the browser.</span></span>

![Microsoft Edge で開いている web アプリケーション](yeoman/_static/yeoman-home-page.png)

## <a name="restoring-building-and-hosting-from-a-command-line"></a><span data-ttu-id="e2332-157">復元する、ビルド、およびコマンド ラインからホスティング</span><span class="sxs-lookup"><span data-stu-id="e2332-157">Restoring, building, and hosting from a command line</span></span>

<span data-ttu-id="e2332-158">準備し、.NET Core CLI を使用して web アプリケーションをホストできます。</span><span class="sxs-lookup"><span data-stu-id="e2332-158">You can prepare and host your web application using the .NET Core CLI.</span></span>

<span data-ttu-id="e2332-159">コマンド プロンプトで、プロジェクトを含むフォルダーに現在のディレクトリを変更します (つまり、フォルダーを含む、 *.csproj*ファイル)。</span><span class="sxs-lookup"><span data-stu-id="e2332-159">At a command prompt, change the current directory to the folder containing the project (that is, the folder containing the *.csproj* file):</span></span>

```console
cd src\MyWebApp
```

<span data-ttu-id="e2332-160">プロジェクトの NuGet パッケージの依存関係を復元します。</span><span class="sxs-lookup"><span data-stu-id="e2332-160">Restore the project's NuGet package dependencies:</span></span>

```console
dotnet restore
```

<span data-ttu-id="e2332-161">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-161">Run the application:</span></span>

```console
dotnet run
```

<span data-ttu-id="e2332-162">クロス プラットフォーム[Kestrel](xref:fundamentals/servers/kestrel) 5000 のポートでリッスンしている web サーバーが開始されます。</span><span class="sxs-lookup"><span data-stu-id="e2332-162">The cross-platform [Kestrel](xref:fundamentals/servers/kestrel) web server will begin listening on port 5000.</span></span>

<span data-ttu-id="e2332-163">Web ブラウザーを開きに移動`http://localhost:5000`です。</span><span class="sxs-lookup"><span data-stu-id="e2332-163">Open a web browser, and navigate to `http://localhost:5000`.</span></span>

![Microsoft Edge で開いている web アプリケーション](yeoman/_static/yeoman-home-page_5000.png)

## <a name="adding-to-your-project-with-sub-generators"></a><span data-ttu-id="e2332-165">Sub ジェネレーターで、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="e2332-165">Adding to your project with sub generators</span></span>

<span data-ttu-id="e2332-166">Yeoman を使用して[ジェネレーターを sub](https://github.com/omnisharp/generator-aspnet)、いずれかを追加することができます、`nuget.config`または`web.config`プロジェクトを作成した後です。</span><span class="sxs-lookup"><span data-stu-id="e2332-166">Using Yeoman [sub generators](https://github.com/omnisharp/generator-aspnet), you can add either a `nuget.config` or a `web.config` after the project is created.</span></span> <span data-ttu-id="e2332-167">たとえば、ファイルを作成するディレクトリから次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e2332-167">For example, execute the following command from the directory in which the file should be created:</span></span>

```console
yo aspnet:nugetconfig
```

<span data-ttu-id="e2332-168">結果は、という名前の NuGet 構成ファイル`nuget.config`次の内容。</span><span class="sxs-lookup"><span data-stu-id="e2332-168">The result is a NuGet configuration file named `nuget.config` with the following content:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
 <packageSources>
    <!--To inherit the global NuGet package sources remove the <clear/> line below -->
    <clear />
 </packageSources>
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="e2332-169">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="e2332-169">Additional resources</span></span>

* [<span data-ttu-id="e2332-170">サーバー (Kestrel と WebListener)</span><span class="sxs-lookup"><span data-stu-id="e2332-170">Servers (Kestrel and WebListener)</span></span>](xref:fundamentals/servers/index)
* [<span data-ttu-id="e2332-171">基礎</span><span class="sxs-lookup"><span data-stu-id="e2332-171">Fundamentals</span></span>](xref:fundamentals/index)