---
title: ASP.NET Core での統合テスト
author: guardrex
description: 学習方法、統合テストでは、インフラストラクチャ レベル、データベース、ファイル システム、ネットワークなど、アプリのコンポーネントが正しく動作することを確認します。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/30/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: test/integration-tests
ms.openlocfilehash: a402c3f5f6a75917eba4058e6cc6926f25b214d4
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "35217685"
---
# <a name="integration-tests-in-aspnet-core"></a><span data-ttu-id="85239-103">ASP.NET Core での統合テスト</span><span class="sxs-lookup"><span data-stu-id="85239-103">Integration tests in ASP.NET Core</span></span>

<span data-ttu-id="85239-104">によって[Luke Latham](https://github.com/guardrex)と[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="85239-104">By [Luke Latham](https://github.com/guardrex) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="85239-105">統合テストをアプリのサポートなどのインフラストラクチャ、データベース、ファイル システム、およびネットワークを含むレベルで、アプリのコンポーネントが正しく動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="85239-105">Integration tests ensure that an app's components function correctly at a level that includes the app's supporting infrastructure, such as the database, file system, and network.</span></span> <span data-ttu-id="85239-106">ASP.NET Core では、テストの web ホストとメモリ内のテスト サーバーを単体テスト フレームワークを使用して統合テストをサポートします。</span><span class="sxs-lookup"><span data-stu-id="85239-106">ASP.NET Core supports integration tests using a unit test framework with a test web host and an in-memory test server.</span></span>

<span data-ttu-id="85239-107">このトピックは、単体テストの基本的な知識を前提とします。</span><span class="sxs-lookup"><span data-stu-id="85239-107">This topic assumes a basic understanding of unit tests.</span></span> <span data-ttu-id="85239-108">場合テストの概念についてよく知らないを参照してください、[単体テストを .NET Core と .NET Standard](/dotnet/core/testing/)トピックとそのリンクのコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="85239-108">If unfamiliar with test concepts, see the [Unit Testing in .NET Core and .NET Standard](/dotnet/core/testing/) topic and its linked content.</span></span>

<span data-ttu-id="85239-109">[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)します ([ダウンロード方法](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="85239-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="85239-110">サンプル アプリは、Razor ページのアプリで Razor ページの基本的な知識を前提としています。</span><span class="sxs-lookup"><span data-stu-id="85239-110">The sample app is a Razor Pages app and assumes a basic understanding of Razor Pages.</span></span> <span data-ttu-id="85239-111">Razor ページに慣れていないの場合は、次のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="85239-111">If unfamiliar with Razor Pages, see the following topics:</span></span>

* [<span data-ttu-id="85239-112">Razor ページを始める</span><span class="sxs-lookup"><span data-stu-id="85239-112">Introduction to Razor Pages</span></span>](xref:mvc/razor-pages/index)
* [<span data-ttu-id="85239-113">Razor ページの概要</span><span class="sxs-lookup"><span data-stu-id="85239-113">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="85239-114">Razor ページの単体テスト</span><span class="sxs-lookup"><span data-stu-id="85239-114">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)

## <a name="introduction-to-integration-tests"></a><span data-ttu-id="85239-115">統合テストの概要</span><span class="sxs-lookup"><span data-stu-id="85239-115">Introduction to integration tests</span></span>

<span data-ttu-id="85239-116">統合テストがより広範なレベルでのアプリのコンポーネントを評価[単体テスト](/dotnet/core/testing/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-116">Integration tests evaluate an app's components on a broader level than [unit tests](/dotnet/core/testing/).</span></span> <span data-ttu-id="85239-117">単体テストは、個々 のクラスのメソッドなど、隔離されたソフトウェア コンポーネントをテストに使用されます。</span><span class="sxs-lookup"><span data-stu-id="85239-117">Unit tests are used to test isolated software components, such as individual class methods.</span></span> <span data-ttu-id="85239-118">統合テストでは、可能性のある要求を完全に処理するために必要なすべてのコンポーネントを含む、予期される結果を生成するために 2 つ以上のアプリ コンポーネントを一緒に使用することを確認します。</span><span class="sxs-lookup"><span data-stu-id="85239-118">Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.</span></span>

<span data-ttu-id="85239-119">このようなより広範なテストは、アプリのインフラストラクチャと、次のコンポーネントを含む多くの場合、フレームワーク全体をテストに使用されます。</span><span class="sxs-lookup"><span data-stu-id="85239-119">These broader tests are used to test the app's infrastructure and whole framework, often including the following components:</span></span>

* <span data-ttu-id="85239-120">データベース</span><span class="sxs-lookup"><span data-stu-id="85239-120">Database</span></span>
* <span data-ttu-id="85239-121">ファイル システム</span><span class="sxs-lookup"><span data-stu-id="85239-121">File system</span></span>
* <span data-ttu-id="85239-122">ネットワーク アプライアンス</span><span class="sxs-lookup"><span data-stu-id="85239-122">Network appliances</span></span>
* <span data-ttu-id="85239-123">要求-応答のパイプライン</span><span class="sxs-lookup"><span data-stu-id="85239-123">Request-response pipeline</span></span>

<span data-ttu-id="85239-124">単体テストの作成を使用するコンポーネントと呼ばれる*fakes*または*オブジェクトをモック*インフラストラクチャのコンポーネントの代わりにします。</span><span class="sxs-lookup"><span data-stu-id="85239-124">Unit tests use fabricated components, known as *fakes* or *mock objects*, in place of infrastructure components.</span></span>

<span data-ttu-id="85239-125">単体テストとは対照的統合をテストします。</span><span class="sxs-lookup"><span data-stu-id="85239-125">In contrast to unit tests, integration tests:</span></span>

* <span data-ttu-id="85239-126">アプリを実稼働環境で使用する実際のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-126">Use the actual components that the app uses in production.</span></span>
* <span data-ttu-id="85239-127">多くのコードとデータ処理が必要です。</span><span class="sxs-lookup"><span data-stu-id="85239-127">Require more code and data processing.</span></span>
* <span data-ttu-id="85239-128">実行時間長くなります。</span><span class="sxs-lookup"><span data-stu-id="85239-128">Take longer to run.</span></span>

<span data-ttu-id="85239-129">したがって、最も重要なインフラストラクチャのシナリオに統合テストの使用を制限します。</span><span class="sxs-lookup"><span data-stu-id="85239-129">Therefore, limit the use of integration tests to the most important infrastructure scenarios.</span></span> <span data-ttu-id="85239-130">場合は、動作をテストするには、単体テストまたは統合テストを使用して、単体テストを選択します。</span><span class="sxs-lookup"><span data-stu-id="85239-130">If a behavior can be tested using either a unit test or an integration test, choose the unit test.</span></span>

> [!TIP]
> <span data-ttu-id="85239-131">データベースおよびファイル システムでのデータとファイルのアクセスの可能な各順列の統合テストを記述しません。</span><span class="sxs-lookup"><span data-stu-id="85239-131">Don't write integration tests for every possible permutation of data and file access with databases and file systems.</span></span> <span data-ttu-id="85239-132">アプリ間でどのくらいの配置に関係なくデータベースおよびファイル システム、フォーカスのある一連の読み取り、書き込み、更新、および削除の統合テストは、十分にテスト データベースのことし、ファイル システムのコンポーネントと対話します。</span><span class="sxs-lookup"><span data-stu-id="85239-132">Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components.</span></span> <span data-ttu-id="85239-133">これらのコンポーネントと対話するメソッドのロジックのルーチンのテスト テスト単位を使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-133">Use unit tests for routine tests of method logic that interact with these components.</span></span> <span data-ttu-id="85239-134">単体テストでインフラストラクチャを使用して fakes/モック テスト実行の速さで結果。</span><span class="sxs-lookup"><span data-stu-id="85239-134">In unit tests, the use of infrastructure fakes/mocks result in faster test execution.</span></span>

> [!NOTE]
> <span data-ttu-id="85239-135">統合テストのディスカッションにテスト対象のプロジェクトは頻繁に呼び出される、*テスト対象のシステム*、または略して"SUT"です。</span><span class="sxs-lookup"><span data-stu-id="85239-135">In discussions of integration tests, the tested project is frequently called the *system under test*, or "SUT" for short.</span></span>

## <a name="aspnet-core-integration-tests"></a><span data-ttu-id="85239-136">ASP.NET Core 統合テスト</span><span class="sxs-lookup"><span data-stu-id="85239-136">ASP.NET Core integration tests</span></span>

<span data-ttu-id="85239-137">ASP.NET Core での統合テストには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-137">Integration tests in ASP.NET Core require the following:</span></span>

* <span data-ttu-id="85239-138">テスト プロジェクトを含めるし、テストを実行するのに使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-138">A test project is used to contain and execute the tests.</span></span> <span data-ttu-id="85239-139">テスト プロジェクトと呼ばれる、テスト対象の ASP.NET Core プロジェクトへの参照では、*テスト対象のシステム*(SUT)。</span><span class="sxs-lookup"><span data-stu-id="85239-139">The test project has a reference to the tested ASP.NET Core project, called the *system under test* (SUT).</span></span> <span data-ttu-id="85239-140">_このトピック全体では、"SUT"を使用してテスト済みのアプリを参照してください。_</span><span class="sxs-lookup"><span data-stu-id="85239-140">_"SUT" is used throughout this topic to refer to the tested app._</span></span>
* <span data-ttu-id="85239-141">テスト プロジェクトでは、SUT のテストの web ホストを作成し、テスト サーバーのクライアントを使用して要求と SUT への応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="85239-141">The test project creates a test web host for the SUT and uses a test server client to handle requests and responses to the SUT.</span></span>
* <span data-ttu-id="85239-142">テスト ランナーを使用して、テスト結果、テストとレポートを実行できます。</span><span class="sxs-lookup"><span data-stu-id="85239-142">A test runner is used to execute the tests and report the test results.</span></span>

<span data-ttu-id="85239-143">統合テストを含む通常のイベントのシーケンスの実行*配置*、 *Act*、および*Assert*テスト ステップ。</span><span class="sxs-lookup"><span data-stu-id="85239-143">Integration tests follow a sequence of events that include the usual *Arrange*, *Act*, and *Assert* test steps:</span></span>

1. <span data-ttu-id="85239-144">SUT の web ホストが構成されています。</span><span class="sxs-lookup"><span data-stu-id="85239-144">The SUT's web host is configured.</span></span>
1. <span data-ttu-id="85239-145">アプリへの要求を送信するには、テスト サーバーのクライアントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="85239-145">A test server client is created to submit requests to the app.</span></span>
1. <span data-ttu-id="85239-146">*配置*テスト ステップが実行された: テスト アプリケーションが要求を準備します。</span><span class="sxs-lookup"><span data-stu-id="85239-146">The *Arrange* test step is executed: The test app prepares a request.</span></span>
1. <span data-ttu-id="85239-147">*Act*テスト ステップが実行された: クライアント要求を送信し、応答を受信します。</span><span class="sxs-lookup"><span data-stu-id="85239-147">The *Act* test step is executed: The client submits the request and receives the response.</span></span>
1. <span data-ttu-id="85239-148">*Assert*テスト ステップが実行された:*実際*応答が検証された、*渡す*または*失敗*に基づいて、*が必要です*応答します。</span><span class="sxs-lookup"><span data-stu-id="85239-148">The *Assert* test step is executed: The *actual* response is validated as a *pass* or *fail* based on an *expected* response.</span></span>
1. <span data-ttu-id="85239-149">プロセスは、すべてのテストが実行されるまで続行します。</span><span class="sxs-lookup"><span data-stu-id="85239-149">The process continues until all of the tests are executed.</span></span>
1. <span data-ttu-id="85239-150">テスト結果が報告されます。</span><span class="sxs-lookup"><span data-stu-id="85239-150">The test results are reported.</span></span>

<span data-ttu-id="85239-151">通常、テストの web ホストではテスト用のアプリの標準的な web ホストの実行よりも構成が異なる。</span><span class="sxs-lookup"><span data-stu-id="85239-151">Usually, the test web host is configured differently than the app's normal web host for the test runs.</span></span> <span data-ttu-id="85239-152">たとえば、別のデータベースまたは別のアプリの設定は、テストに使用可能性があります。</span><span class="sxs-lookup"><span data-stu-id="85239-152">For example, a different database or different app settings might be used for the tests.</span></span>

<span data-ttu-id="85239-153">テストの web ホストとメモリ内のテスト サーバーなどのインフラストラクチャ コンポーネント ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)) が提供されるかによって管理される、 [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)パッケージです。</span><span class="sxs-lookup"><span data-stu-id="85239-153">Infrastructure components, such as the test web host and in-memory test server ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)), are provided or managed by the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package.</span></span> <span data-ttu-id="85239-154">このパッケージの使用には、テストの作成と実行が簡略化します。</span><span class="sxs-lookup"><span data-stu-id="85239-154">Use of this package streamlines test creation and execution.</span></span>

<span data-ttu-id="85239-155">`Microsoft.AspNetCore.Mvc.Testing`パッケージは、次のタスクを処理します。</span><span class="sxs-lookup"><span data-stu-id="85239-155">The `Microsoft.AspNetCore.Mvc.Testing` package handles the following tasks:</span></span>

* <span data-ttu-id="85239-156">依存関係ファイルにコピー (*\*.deps*) にテスト プロジェクトの SUT から*bin*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="85239-156">Copies the dependencies file (*\*.deps*) from the SUT into the test project's *bin* folder.</span></span>
* <span data-ttu-id="85239-157">静的なファイルおよびページ/ビューは、テストを実行するときに検出できるようにするには、コンテンツのルート SUT のプロジェクトのルートを設定します。</span><span class="sxs-lookup"><span data-stu-id="85239-157">Sets the content root to the SUT's project root so that static files and pages/views are found when the tests are executed.</span></span>
* <span data-ttu-id="85239-158">提供、 [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)で SUT のブートス トラップを効率化するクラス`TestServer`です。</span><span class="sxs-lookup"><span data-stu-id="85239-158">Provides the [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) class to streamline bootstrapping the SUT with `TestServer`.</span></span>

<span data-ttu-id="85239-159">[単体テスト](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)テスト プロジェクトとテスト ランナー、と共に名前テストにテストおよび方法に関する推奨事項を実行し、クラスをテストする方法の詳細な説明を設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="85239-159">The [unit tests](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) documentation describes how to set up a test project and test runner, along with detailed instructions on how to run tests and recommendations for how to name tests and test classes.</span></span>

> [!NOTE]
> <span data-ttu-id="85239-160">アプリのテスト プロジェクトを作成する場合は、別々 のプロジェクトに統合テストから単体テストを区切ります。</span><span class="sxs-lookup"><span data-stu-id="85239-160">When creating a test project for an app, separate the unit tests from the integration tests into different projects.</span></span> <span data-ttu-id="85239-161">こうことからインフラストラクチャのテストのコンポーネントの単体テストに含まれる誤っていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="85239-161">This helps ensure that infrastructure testing components aren't accidently included in the unit tests.</span></span> <span data-ttu-id="85239-162">単位との統合のテストの分離により、テストのセットでは実行を制御します。</span><span class="sxs-lookup"><span data-stu-id="85239-162">Separation of unit and integration tests also allows control over which set of tests are run.</span></span>

<span data-ttu-id="85239-163">事実上ない違いは Razor ページのアプリのテストの構成」および「MVC アプリです。</span><span class="sxs-lookup"><span data-stu-id="85239-163">There's virtually no difference between the configuration for tests of Razor Pages apps and MVC apps.</span></span> <span data-ttu-id="85239-164">唯一の違いは、テストの名前付け方法です。</span><span class="sxs-lookup"><span data-stu-id="85239-164">The only difference is in how the tests are named.</span></span> <span data-ttu-id="85239-165">Razor ページ アプリケーションでは、ページのエンドポイントのテストの名前は通常、ページのモデル クラス後 (たとえば、`IndexPageTests`インデックス ページのコンポーネントの統合をテストする)。</span><span class="sxs-lookup"><span data-stu-id="85239-165">In a Razor Pages app, tests of page endpoints are usually named after the page model class (for example, `IndexPageTests` to test component integration for the Index page).</span></span> <span data-ttu-id="85239-166">MVC アプリケーションでテスト通常コント ローラー クラス別に整理され、テスト コント ローラーにちなんだ名前 (たとえば、 `HomeControllerTests` Home コント ローラー用のコンポーネントの統合をテストする)。</span><span class="sxs-lookup"><span data-stu-id="85239-166">In an MVC app, tests are usually organized by controller classes and named after the controllers they test (for example, `HomeControllerTests` to test component integration for the Home controller).</span></span>

## <a name="test-app-prerequisites"></a><span data-ttu-id="85239-167">アプリの前提条件をテストします。</span><span class="sxs-lookup"><span data-stu-id="85239-167">Test app prerequisites</span></span>

<span data-ttu-id="85239-168">テスト プロジェクトである必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-168">The test project must:</span></span>

* <span data-ttu-id="85239-169">パッケージ参照を持つ[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-169">Have a package reference for [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/).</span></span>
* <span data-ttu-id="85239-170">Web SDK を使用して、プロジェクト ファイル (`<Project Sdk="Microsoft.NET.Sdk.Web">`)。</span><span class="sxs-lookup"><span data-stu-id="85239-170">Use the Web SDK in the project file (`<Project Sdk="Microsoft.NET.Sdk.Web">`).</span></span>

<span data-ttu-id="85239-171">これら prerequesities がわかるように、[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-171">These prerequesities can be seen in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/).</span></span> <span data-ttu-id="85239-172">検査、 *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj*ファイル。</span><span class="sxs-lookup"><span data-stu-id="85239-172">Inspect the *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj* file.</span></span>

## <a name="basic-tests-with-the-default-webapplicationfactory"></a><span data-ttu-id="85239-173">既定値 WebApplicationFactory の基本的なテスト</span><span class="sxs-lookup"><span data-stu-id="85239-173">Basic tests with the default WebApplicationFactory</span></span>

<span data-ttu-id="85239-174">[WebApplicationFactory&lt;TEntryPoint&gt; ](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)作成に使用される、 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)統合テストにします。</span><span class="sxs-lookup"><span data-stu-id="85239-174">[WebApplicationFactory&lt;TEntryPoint&gt;](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) is used to create a [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) for the integration tests.</span></span> <span data-ttu-id="85239-175">`TEntryPoint` SUT のエントリ ポイント クラスは、通常、`Startup`クラスです。</span><span class="sxs-lookup"><span data-stu-id="85239-175">`TEntryPoint` is the entry point class of the SUT, usually the `Startup` class.</span></span>

<span data-ttu-id="85239-176">テスト クラスで実装する*クラス フィクスチャ*インターフェイス (`IClassFixture`) を示し、クラス テストが含まれるクラス内のテストの間で共有されたオブジェクトのインスタンスを指定します。</span><span class="sxs-lookup"><span data-stu-id="85239-176">Test classes implement a *class fixture* interface (`IClassFixture`) to indicate the class contains tests and provide shared object instances across the tests in the class.</span></span>

### <a name="basic-test-of-app-endpoints"></a><span data-ttu-id="85239-177">アプリのエンドポイントの基本のテスト</span><span class="sxs-lookup"><span data-stu-id="85239-177">Basic test of app endpoints</span></span>

<span data-ttu-id="85239-178">次のテスト クラス、`BasicTests`を使用して、 `WebApplicationFactory` SUT をブートス トラップでき、 [HttpClient](/dotnet/api/system.net.http.httpclient)テスト メソッドに`Get_EndpointsReturnSuccessAndCorrectContentType`です。</span><span class="sxs-lookup"><span data-stu-id="85239-178">The following test class, `BasicTests`, uses the `WebApplicationFactory` to bootstrap the SUT and provide an [HttpClient](/dotnet/api/system.net.http.httpclient) to a test method, `Get_EndpointsReturnSuccessAndCorrectContentType`.</span></span> <span data-ttu-id="85239-179">チェックするメソッドが応答状態コードが成功したかどうか (状態コード 200 299 の範囲内で) および`Content-Type`ヘッダーが`text/html; charset=utf-8`のいくつかのアプリ ページ。</span><span class="sxs-lookup"><span data-stu-id="85239-179">The method checks if the response status code is successful (status codes in the range 200-299) and the `Content-Type` header is `text/html; charset=utf-8` for several app pages.</span></span>

<span data-ttu-id="85239-180">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)のインスタンスを作成`HttpClient`を自動的にリダイレクトに依存して cookie を処理します。</span><span class="sxs-lookup"><span data-stu-id="85239-180">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) creates an instance of `HttpClient` that automatically follows redirects and handles cookies.</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet1)]

### <a name="test-a-secure-endpoint"></a><span data-ttu-id="85239-181">セキュリティで保護されたエンドポイントをテストします。</span><span class="sxs-lookup"><span data-stu-id="85239-181">Test a secure endpoint</span></span>

<span data-ttu-id="85239-182">内の別のテスト、`BasicTests`クラスは、セキュリティで保護されたエンドポイントが、アプリのログイン ページに認証されていないユーザーをリダイレクトすることを確認します。</span><span class="sxs-lookup"><span data-stu-id="85239-182">Another test in the `BasicTests` class checks that a secure endpoint redirects an unauthenticated user to the app's Login page.</span></span>

<span data-ttu-id="85239-183">SUT で、`/SecurePage`ページの使用、 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)規則を適用する、 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)ページにします。</span><span class="sxs-lookup"><span data-stu-id="85239-183">In the SUT, the `/SecurePage` page uses an [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention to apply an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page.</span></span> <span data-ttu-id="85239-184">詳細については、次を参照してください。 [Razor ページの承認規則](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page)です。</span><span class="sxs-lookup"><span data-stu-id="85239-184">For more information, see [Razor Pages authorization conventions](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page).</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet1)]

<span data-ttu-id="85239-185">`Get_SecurePageRequiresAnAuthenticatedUser`をテストする、 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)を設定してリダイレクトを許可しないように設定されている[AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect)に`false`:</span><span class="sxs-lookup"><span data-stu-id="85239-185">In the `Get_SecurePageRequiresAnAuthenticatedUser` test, a [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) is set to disallow redirects by setting [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) to `false`:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet2)]

<span data-ttu-id="85239-186">クライアントのリダイレクトに従うを禁止して、次のチェックを変更できます。</span><span class="sxs-lookup"><span data-stu-id="85239-186">By disallowing the client to follow the redirect, the following checks can be made:</span></span>

* <span data-ttu-id="85239-187">SUT によって返されるステータス コードをチェックして、予期されたに対して[HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode)結果であるログイン ページへのリダイレクトの後に最終的な状態コードではなく[HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span><span class="sxs-lookup"><span data-stu-id="85239-187">The status code returned by the SUT can be checked against the expected [HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode) result, not the final status code after the redirect to the Login page, which would be [HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span></span>
* <span data-ttu-id="85239-188">`Location`で始まっていることを確認する応答ヘッダーのヘッダーの値がチェックされて`http://localhost/Identity/Account/Login`、いない最終的なログイン ページの応答、場所、`Location`ヘッダーが存在するはありません。</span><span class="sxs-lookup"><span data-stu-id="85239-188">The `Location` header value in the response headers is checked to confirm that it starts with `http://localhost/Identity/Account/Login`, not the final Login page response, where the `Location` header wouldn't be present.</span></span>

<span data-ttu-id="85239-189">詳細については`WebApplicationFactoryClientOptions`を参照してください、[クライアント オプション](#client-options)セクションです。</span><span class="sxs-lookup"><span data-stu-id="85239-189">For more information on `WebApplicationFactoryClientOptions`, see the [Client options](#client-options) section.</span></span>

## <a name="customize-webapplicationfactory"></a><span data-ttu-id="85239-190">WebApplicationFactory をカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="85239-190">Customize WebApplicationFactory</span></span>

<span data-ttu-id="85239-191">継承することで、テスト クラスとは無関係に web ホストの構成を作成できます`WebApplicationFactory`を 1 つまたは複数のカスタム ファクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="85239-191">Web host configuration can be created independently of the test classes by inheriting from `WebApplicationFactory` to create one or more custom factories:</span></span>

1. <span data-ttu-id="85239-192">継承`WebApplicationFactory`オーバーライドと[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost)です。</span><span class="sxs-lookup"><span data-stu-id="85239-192">Inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost).</span></span> <span data-ttu-id="85239-193">[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)サービス コレクションの構成を許可[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span><span class="sxs-lookup"><span data-stu-id="85239-193">The [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) allows the configuration of the service collection with [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/CustomWebApplicationFactory.cs?name=snippet1)]

   <span data-ttu-id="85239-194">データベースのシード処理で、[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)äs ' í、`InitializeDbForTests`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="85239-194">Database seeding in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is performed by the `InitializeDbForTests` method.</span></span> <span data-ttu-id="85239-195">メソッドに記載されて、[統合サンプルをテストする: テスト アプリ組織](#test-app-organization)セクションです。</span><span class="sxs-lookup"><span data-stu-id="85239-195">The method is described in the [Integration tests sample: Test app organization](#test-app-organization) section.</span></span>

2. <span data-ttu-id="85239-196">ユーザー設定を使用して`CustomWebApplicationFactory`テスト クラスでします。</span><span class="sxs-lookup"><span data-stu-id="85239-196">Use the custom `CustomWebApplicationFactory` in test classes.</span></span> <span data-ttu-id="85239-197">次の例のファクトリを使用する、`IndexPageTests`クラス。</span><span class="sxs-lookup"><span data-stu-id="85239-197">The following example uses the factory in the `IndexPageTests` class:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet1)]

   <span data-ttu-id="85239-198">防ぐために、サンプル アプリのクライアントが構成されている、`HttpClient`次のリダイレクトから。</span><span class="sxs-lookup"><span data-stu-id="85239-198">The sample app's client is configured to prevent the `HttpClient` from following redirects.</span></span> <span data-ttu-id="85239-199">説明に従って、[セキュリティで保護されたエンドポイントをテスト](#test-a-secure-endpoint) セクションで、これにより、アプリの最初の応答の結果を確認するテストです。</span><span class="sxs-lookup"><span data-stu-id="85239-199">As explained in the [Test a secure endpoint](#test-a-secure-endpoint) section, this permits tests to check the result of the app's first response.</span></span> <span data-ttu-id="85239-200">最初の応答でこれらのテストの多くでリダイレクトを行うは、`Location`ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="85239-200">The first response is a redirect in many of these tests with a `Location` header.</span></span>

3. <span data-ttu-id="85239-201">一般的なテストを使用して、`HttpClient`と、要求と応答を処理するヘルパー メソッド。</span><span class="sxs-lookup"><span data-stu-id="85239-201">A typical test uses the `HttpClient` and helper methods to process the request and the response:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet2)]

<span data-ttu-id="85239-202">SUT に POST 要求は、アプリのによって自動的に行われた antiforgery チェックを満たす必要があります[データ保護 antiforgery システム](xref:security/data-protection/introduction)です。</span><span class="sxs-lookup"><span data-stu-id="85239-202">Any POST request to the SUT must satisfy the antiforgery check that's automatically made by the app's [data protection antiforgery system](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="85239-203">テストの POST 要求の配置、するために、アプリケーションをテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-203">In order to arrange for a test's POST request, the test app must:</span></span>

1. <span data-ttu-id="85239-204">ページの要求を行います。</span><span class="sxs-lookup"><span data-stu-id="85239-204">Make a request for the page.</span></span>
1. <span data-ttu-id="85239-205">Antiforgery cookie と、応答からの要求の検証トークンを解析します。</span><span class="sxs-lookup"><span data-stu-id="85239-205">Parse the antiforgery cookie and request validation token from the response.</span></span>
1. <span data-ttu-id="85239-206">インプレース antiforgery cookie と要求の検証の POST 要求トークンを作成します。</span><span class="sxs-lookup"><span data-stu-id="85239-206">Make the POST request with the antiforgery cookie and request validation token in place.</span></span>

<span data-ttu-id="85239-207">`SendAsync`ヘルパー拡張メソッド (*Helpers/HttpClientExtensions.cs*) および`GetDocumentAsync`ヘルパー メソッド (*Helpers/HtmlHelpers.cs*) で、 [のサンプルアプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)を使用して、 [AngleSharp](https://anglesharp.github.io/) antiforgery チェックを以下の方法で処理するためにパーサー。</span><span class="sxs-lookup"><span data-stu-id="85239-207">The `SendAsync` helper extension methods (*Helpers/HttpClientExtensions.cs*) and the `GetDocumentAsync` helper method (*Helpers/HtmlHelpers.cs*) in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/) use the [AngleSharp](https://anglesharp.github.io/) parser to handle the antiforgery check with the following methods:</span></span>

* <span data-ttu-id="85239-208">`GetDocumentAsync` &ndash; 受信、 [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage)を返します、`IHtmlDocument`です。</span><span class="sxs-lookup"><span data-stu-id="85239-208">`GetDocumentAsync` &ndash; Receives the [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) and returns an `IHtmlDocument`.</span></span> <span data-ttu-id="85239-209">`GetDocumentAsync` 準備するファクトリを使用する、*仮想応答*元に基づいて`HttpResponseMessage`です。</span><span class="sxs-lookup"><span data-stu-id="85239-209">`GetDocumentAsync` uses a factory that prepares a *virtual response* based on the original `HttpResponseMessage`.</span></span> <span data-ttu-id="85239-210">詳細については、次を参照してください。、 [AngleSharp ドキュメント](https://github.com/AngleSharp/AngleSharp#documentation)です。</span><span class="sxs-lookup"><span data-stu-id="85239-210">For more information, see the [AngleSharp documentation](https://github.com/AngleSharp/AngleSharp#documentation).</span></span>
* <span data-ttu-id="85239-211">`SendAsync` 拡張メソッドを`HttpClient`作成、 [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage)を呼び出すと[SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) SUT に要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="85239-211">`SendAsync` extension methods for the `HttpClient` compose an [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage) and call [SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) to submit requests to the SUT.</span></span> <span data-ttu-id="85239-212">オーバー ロード`SendAsync`HTML フォームを受け入れる (`IHtmlFormElement`) および次。</span><span class="sxs-lookup"><span data-stu-id="85239-212">Overloads for `SendAsync` accept the HTML form (`IHtmlFormElement`) and the following:</span></span>
  - <span data-ttu-id="85239-213">フォームのボタンの送信 (`IHtmlElement`)</span><span class="sxs-lookup"><span data-stu-id="85239-213">Submit button of the form (`IHtmlElement`)</span></span>
  - <span data-ttu-id="85239-214">フォーム値のコレクション (`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="85239-214">Form values collection (`IEnumerable<KeyValuePair<string, string>>`)</span></span>
  - <span data-ttu-id="85239-215">送信ボタン (`IHtmlElement`) の値を形成し、(`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="85239-215">Submit button (`IHtmlElement`) and form values (`IEnumerable<KeyValuePair<string, string>>`)</span></span>

> [!NOTE]
> <span data-ttu-id="85239-216">[AngleSharp](https://anglesharp.github.io/)サード パーティがこのトピックおよびサンプル アプリでのデモンストレーションのために使用されるライブラリに解析します。</span><span class="sxs-lookup"><span data-stu-id="85239-216">[AngleSharp](https://anglesharp.github.io/) is a third-party parsing library used for demonstration purposes in this topic and the sample app.</span></span> <span data-ttu-id="85239-217">AngleSharp が ASP.NET Core アプリケーションの統合のテストに必要なまたはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="85239-217">AngleSharp isn't supported or required for integration testing of ASP.NET Core apps.</span></span> <span data-ttu-id="85239-218">その他のパーサー使用できますが、ように、 [Html アジリティ パック (HAP)](http://html-agility-pack.net/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-218">Other parsers can be used, such as the [Html Agility Pack (HAP)](http://html-agility-pack.net/).</span></span> <span data-ttu-id="85239-219">別の方法では、antiforgery システムの検証トークンの要求と antiforgery cookie を直接処理するコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="85239-219">Another approach is to write code to handle the antiforgery system's request verification token and antiforgery cookie directly.</span></span>

## <a name="customize-the-client-with-withwebhostbuilder"></a><span data-ttu-id="85239-220">WithWebHostBuilder でクライアントをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="85239-220">Customize the client with WithWebHostBuilder</span></span>

<span data-ttu-id="85239-221">追加の構成が必要な場合、テスト メソッド内で[WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder)新たに作成`WebApplicationFactory`で、 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)ですが、構成でさらにカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="85239-221">When additional configuration is required within a test method, [WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder) creates a new `WebApplicationFactory` with an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) that is further customized by configuration.</span></span>

<span data-ttu-id="85239-222">`Post_DeleteMessageHandler_ReturnsRedirectToRoot`テストのメソッド、[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)の使用例を示します`WithWebHostBuilder`です。</span><span class="sxs-lookup"><span data-stu-id="85239-222">The `Post_DeleteMessageHandler_ReturnsRedirectToRoot` test method of the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) demonstrates the use of `WithWebHostBuilder`.</span></span> <span data-ttu-id="85239-223">このテストは、SUT にフォームの送信をトリガーすることによって、データベース内のレコードの削除を実行します。</span><span class="sxs-lookup"><span data-stu-id="85239-223">This test performs a record delete in the database by triggering a form submission in the SUT.</span></span>

<span data-ttu-id="85239-224">別のテストであるため、`IndexPageTests`クラスは、データベース内のレコードのすべてを削除し、前に実行する操作を実行、`Post_DeleteMessageHandler_ReturnsRedirectToRoot`メソッド、データベースは、レコードが削除 SUT に存在することを確認するには、このテスト メソッドのシードです。</span><span class="sxs-lookup"><span data-stu-id="85239-224">Because another test in the `IndexPageTests` class performs an operation that deletes all of the records in the database and may run before the `Post_DeleteMessageHandler_ReturnsRedirectToRoot` method, the database is seeded in this test method to ensure that a record is present for the SUT to delete.</span></span> <span data-ttu-id="85239-225">選択すると、`deleteBtn1`のボタン、 `messages` SUT への要求に SUT でフォームをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="85239-225">Selecting the `deleteBtn1` button of the `messages` form in the SUT is simulated in the request to the SUT:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet3)]

## <a name="client-options"></a><span data-ttu-id="85239-226">クライアントのオプション</span><span class="sxs-lookup"><span data-stu-id="85239-226">Client options</span></span>

<span data-ttu-id="85239-227">次の表は、既定値を示しています。 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)作成するときに使用可能な`HttpClient`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="85239-227">The following table shows the default [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) available when creating `HttpClient` instances.</span></span>

| <span data-ttu-id="85239-228">オプション</span><span class="sxs-lookup"><span data-stu-id="85239-228">Option</span></span> | <span data-ttu-id="85239-229">説明</span><span class="sxs-lookup"><span data-stu-id="85239-229">Description</span></span> | <span data-ttu-id="85239-230">既定値</span><span class="sxs-lookup"><span data-stu-id="85239-230">Default</span></span> |
| ------ | ----------- | ------- |
| [<span data-ttu-id="85239-231">AllowAutoRedirect</span><span class="sxs-lookup"><span data-stu-id="85239-231">AllowAutoRedirect</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) | <span data-ttu-id="85239-232">取得または設定するかどうか`HttpClient`インスタンスは、リダイレクト応答に自動的に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-232">Gets or sets whether or not `HttpClient` instances should automatically follow redirect responses.</span></span> | `true` |
| [<span data-ttu-id="85239-233">BaseAddress</span><span class="sxs-lookup"><span data-stu-id="85239-233">BaseAddress</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.baseaddress) | <span data-ttu-id="85239-234">取得または設定のベース アドレス`HttpClient`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="85239-234">Gets or sets the base address of `HttpClient` instances.</span></span> | `http://localhost` |
| [<span data-ttu-id="85239-235">HandleCookies</span><span class="sxs-lookup"><span data-stu-id="85239-235">HandleCookies</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.handlecookies) | <span data-ttu-id="85239-236">取得または設定するかどうか`HttpClient`インスタンスは、cookie を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-236">Gets or sets whether `HttpClient` instances should handle cookies.</span></span> | `true` |
| [<span data-ttu-id="85239-237">MaxAutomaticRedirections</span><span class="sxs-lookup"><span data-stu-id="85239-237">MaxAutomaticRedirections</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.maxautomaticredirections) | <span data-ttu-id="85239-238">リダイレクト応答の最大数の設定を取得または`HttpClient`インスタンスが従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="85239-238">Gets or sets the maximum number of redirect responses that `HttpClient` instances should follow.</span></span> | <span data-ttu-id="85239-239">7</span><span class="sxs-lookup"><span data-stu-id="85239-239">7</span></span> |

<span data-ttu-id="85239-240">作成、`WebApplicationFactoryClientOptions`クラスに渡すと、 [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)メソッド (既定値は、コード例で表示されます)。</span><span class="sxs-lookup"><span data-stu-id="85239-240">Create the `WebApplicationFactoryClientOptions` class and pass it to the [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) method (default values are shown in the code example):</span></span>

```csharp
// Default client option values are shown
var clientOptions = new WebApplicationFactoryClientOptions();
clientOptions.AllowAutoRedirect = true;
clientOptions.BaseAddress = new Uri("http://localhost");
clientOptions.HandleCookies = true;
clientOptions.MaxAutomaticRedirections = 7;

_client = _factory.CreateClient(clientOptions);
```

## <a name="how-the-test-infrastructure-infers-the-app-content-root-path"></a><span data-ttu-id="85239-241">テスト インフラストラクチャがアプリのコンテンツのルート パスを推論する方法</span><span class="sxs-lookup"><span data-stu-id="85239-241">How the test infrastructure infers the app content root path</span></span>

<span data-ttu-id="85239-242">`WebApplicationFactory`コンス トラクターを検索して、アプリのコンテンツのルート パスを推測する、 [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute)と等しいキーを使用して、統合テストを含むアセンブリを`TEntryPoint`アセンブリ`System.Reflection.Assembly.FullName`.</span><span class="sxs-lookup"><span data-stu-id="85239-242">The `WebApplicationFactory` constructor infers the app content root path by searching for a [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute) on the assembly containing the integration tests with a key equal to the `TEntryPoint` assembly `System.Reflection.Assembly.FullName`.</span></span> <span data-ttu-id="85239-243">正しいキーを持つ属性が見つからない場合に`WebApplicationFactory`ソリューション ファイルを検索するフォールバック (*\*.sln*) を追加し、`TEntryPoint`ソリューション ディレクトリにアセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="85239-243">In case an attribute with the correct key isn't found, `WebApplicationFactory` falls back to searching for a solution file (*\*.sln*) and appends the `TEntryPoint` assembly name to the solution directory.</span></span> <span data-ttu-id="85239-244">アプリケーションのルート ディレクトリ (コンテンツのルートのパス) を使用して、ビューとコンテンツ ファイルを検出します。</span><span class="sxs-lookup"><span data-stu-id="85239-244">The app root directory (the content root path) is used to discover views and content files.</span></span>

<span data-ttu-id="85239-245">ほとんどの場合、必要はありませんアプリ コンテンツのルートを明示的に設定するように検索ロジックは、実行時に正しいコンテンツのルートを検索する通常します。</span><span class="sxs-lookup"><span data-stu-id="85239-245">In most cases, it isn't necessary to explicitly set the app content root, as the search logic usually finds the correct content root at runtime.</span></span> <span data-ttu-id="85239-246">コンテンツのルートが見つからないの特殊なシナリオで明示的にまたはカスタム ロジックを使用して、ルートを指定できますコンテンツ アプリで、組み込みの検索アルゴリズムを使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-246">In special scenarios where the content root isn't found using the built-in search algorithm, the app content root can be specified explicitly or by using custom logic.</span></span> <span data-ttu-id="85239-247">そのようなシナリオでアプリのコンテンツのルートを設定するには、呼び出し、`UseSolutionRelativeContentRoot`から拡張メソッド、 [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost)パッケージです。</span><span class="sxs-lookup"><span data-stu-id="85239-247">To set the app content root in those scenarios, call the `UseSolutionRelativeContentRoot` extension method from the [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost) package.</span></span> <span data-ttu-id="85239-248">ソリューションの相対パスと省略可能なソリューション ファイルの名前または glob パターンを指定 (既定 = `*.sln`)。</span><span class="sxs-lookup"><span data-stu-id="85239-248">Supply the solution's relative path and optional solution file name or glob pattern (default = `*.sln`).</span></span>

<span data-ttu-id="85239-249">呼び出す、 [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot)メソッドを使用して拡張*1*次のどの方法。</span><span class="sxs-lookup"><span data-stu-id="85239-249">Call the [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot) extension method using *ONE* of the following approaches:</span></span>

* <span data-ttu-id="85239-250">テスト クラスを構成するときに`WebApplicationFactory`でのカスタム構成を指定して、 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span><span class="sxs-lookup"><span data-stu-id="85239-250">When configuring test classes with `WebApplicationFactory`, provide a custom configuration with the [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span></span>

   ```csharp
   public IndexPageTests(
       WebApplicationFactory<RazorPagesProject.Startup> factory)
   {
       var _factory = factory.WithWebHostBuilder(builder =>
       {
           builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

           ...
       });
   }
   ```

* <span data-ttu-id="85239-251">カスタムのテスト クラスを構成するときに`WebApplicationFactory`から継承`WebApplicationFactory`オーバーライドと[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span><span class="sxs-lookup"><span data-stu-id="85239-251">When configuring test classes with a custom `WebApplicationFactory`, inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span></span>

   ```csharp
   public class CustomWebApplicationFactory<TStartup>
       : WebApplicationFactory<RazorPagesProject.Startup>
   {
       protected override void ConfigureWebHost(IWebHostBuilder builder)
       {
           builder.ConfigureServices(services =>
           {
               builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

               ...
           });
       }
   }
   ```

## <a name="disable-shadow-copying"></a><span data-ttu-id="85239-252">シャドウ コピーを無効にします。</span><span class="sxs-lookup"><span data-stu-id="85239-252">Disable shadow copying</span></span>

<span data-ttu-id="85239-253">シャドウ コピーすると、出力フォルダーとは異なるフォルダーで実行するテストが発生します。</span><span class="sxs-lookup"><span data-stu-id="85239-253">Shadow copying causes the tests to execute in a different folder than the output folder.</span></span> <span data-ttu-id="85239-254">正常に動作するテストでは、シャドウ コピーする必要があります無効になります。</span><span class="sxs-lookup"><span data-stu-id="85239-254">For tests to work properly, shadow copying must be disabled.</span></span> <span data-ttu-id="85239-255">[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)xUnit を使用し、シャドウ コピー xUnit などによって無効になります、 *xunit.runner.json*適切な構成設定を持つファイルです。</span><span class="sxs-lookup"><span data-stu-id="85239-255">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) uses xUnit and disables shadow copying for xUnit by including an *xunit.runner.json* file with the correct configuration setting.</span></span> <span data-ttu-id="85239-256">詳細については、次を参照してください。 [xUnit.net を構成する JSON で](https://xunit.github.io/docs/configuring-with-json.html)です。</span><span class="sxs-lookup"><span data-stu-id="85239-256">For more information, see [Configuring xUnit.net with JSON](https://xunit.github.io/docs/configuring-with-json.html).</span></span>

<span data-ttu-id="85239-257">追加、 *xunit.runner.json*次のコンテンツを含むテスト プロジェクトのルートにファイル。</span><span class="sxs-lookup"><span data-stu-id="85239-257">Add the *xunit.runner.json* file to root of the test project with the following content:</span></span>

```json
{
  "shadowCopy": false
}
```

## <a name="integration-tests-sample"></a><span data-ttu-id="85239-258">統合テストのサンプル</span><span class="sxs-lookup"><span data-stu-id="85239-258">Integration tests sample</span></span>

<span data-ttu-id="85239-259">[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)は 2 個のアプリで構成されます。</span><span class="sxs-lookup"><span data-stu-id="85239-259">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is composed of two apps:</span></span>

| <span data-ttu-id="85239-260">アプリ</span><span class="sxs-lookup"><span data-stu-id="85239-260">App</span></span> | <span data-ttu-id="85239-261">プロジェクト フォルダー</span><span class="sxs-lookup"><span data-stu-id="85239-261">Project folder</span></span> | <span data-ttu-id="85239-262">説明</span><span class="sxs-lookup"><span data-stu-id="85239-262">Description</span></span> |
| --- | -------------- | ----------- |
| <span data-ttu-id="85239-263">メッセージ アプリ (SUT)</span><span class="sxs-lookup"><span data-stu-id="85239-263">Message app (the SUT)</span></span> | <span data-ttu-id="85239-264">*src/RazorPagesProject*</span><span class="sxs-lookup"><span data-stu-id="85239-264">*src/RazorPagesProject*</span></span> | <span data-ttu-id="85239-265">ユーザーを追加、1 つを削除、削除、およびメッセージを分析できます。</span><span class="sxs-lookup"><span data-stu-id="85239-265">Allows a user to add, delete one, delete all, and analyze messages.</span></span> |
| <span data-ttu-id="85239-266">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="85239-266">Test app</span></span> | <span data-ttu-id="85239-267">*tests/RazorPagesProject.Tests*</span><span class="sxs-lookup"><span data-stu-id="85239-267">*tests/RazorPagesProject.Tests*</span></span> | <span data-ttu-id="85239-268">統合テスト SUT するために使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-268">Used to integration test the SUT.</span></span> |

<span data-ttu-id="85239-269">などの IDE の組み込みのテスト機能を使用してテストを実行できる[Visual Studio](https://www.visualstudio.com/vs/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-269">The tests can be run using the built-in test features of an IDE, such as [Visual Studio](https://www.visualstudio.com/vs/).</span></span> <span data-ttu-id="85239-270">使用して場合[Visual Studio Code](https://code.visualstudio.com/)またはコマンド プロンプトで次のコマンドを実行、コマンドライン、 *tests/RazorPagesProject.Tests*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="85239-270">If using [Visual Studio Code](https://code.visualstudio.com/) or the command line, execute the following command at a command prompt in the *tests/RazorPagesProject.Tests* folder:</span></span>

```console
dotnet test
```

### <a name="message-app-sut-organization"></a><span data-ttu-id="85239-271">メッセージ アプリ (SUT) 組織</span><span class="sxs-lookup"><span data-stu-id="85239-271">Message app (SUT) organization</span></span>

<span data-ttu-id="85239-272">SUT は、次の特性を持つ Razor ページ メッセージ システムを示します。</span><span class="sxs-lookup"><span data-stu-id="85239-272">The SUT is a Razor Pages message system with the following characteristics:</span></span>

* <span data-ttu-id="85239-273">アプリのインデックス ページ (*Pages/Index.cshtml*と*Pages/Index.cshtml.cs*) UI とページを追加、削除、およびメッセージ (メッセージあたりの平均ワード) の分析を制御するモデルのメソッドを提供.</span><span class="sxs-lookup"><span data-stu-id="85239-273">The Index page of the app (*Pages/Index.cshtml* and *Pages/Index.cshtml.cs*) provides a UI and page model methods to control the addition, deletion, and analysis of messages (average words per message).</span></span>
* <span data-ttu-id="85239-274">メッセージは、`Message`クラス (*Data/Message.cs*) 2 つのプロパティを持つ: `Id` (キー) と`Text`(メッセージ)。</span><span class="sxs-lookup"><span data-stu-id="85239-274">A message is described by the `Message` class (*Data/Message.cs*) with two properties: `Id` (key) and `Text` (message).</span></span> <span data-ttu-id="85239-275">`Text`プロパティは必須であり 200 文字までに制限されます。</span><span class="sxs-lookup"><span data-stu-id="85239-275">The `Text` property is required and limited to 200 characters.</span></span>
* <span data-ttu-id="85239-276">使用してメッセージが格納される[Entity Framework のメモリ内のデータベース](/ef/core/providers/in-memory/)&#8224;。</span><span class="sxs-lookup"><span data-stu-id="85239-276">Messages are stored using [Entity Framework's in-memory database](/ef/core/providers/in-memory/)&#8224;.</span></span>
* <span data-ttu-id="85239-277">アプリには、データベース コンテキスト クラスのデータ アクセス層 (DAL) が含まれています`AppDbContext`(*Data/AppDbContext.cs*)。</span><span class="sxs-lookup"><span data-stu-id="85239-277">The app contains a data access layer (DAL) in its database context class, `AppDbContext` (*Data/AppDbContext.cs*).</span></span>
* <span data-ttu-id="85239-278">データベースがアプリの起動時に空の場合、メッセージ ストアは、3 つのメッセージで初期化されます。</span><span class="sxs-lookup"><span data-stu-id="85239-278">If the database is empty on app startup, the message store is initialized with three messages.</span></span>
* <span data-ttu-id="85239-279">アプリが含まれています、`/SecurePage`認証済みユーザーによってのみアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="85239-279">The app includes a `/SecurePage` that can only be accessed by an authenticated user.</span></span>

<span data-ttu-id="85239-280">&#8224;EF トピック[InMemory を伴うテスト](/ef/core/miscellaneous/testing/in-memory)MSTest でテストにメモリ内のデータベースを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="85239-280">&#8224;The EF topic, [Test with InMemory](/ef/core/miscellaneous/testing/in-memory), explains how to use an in-memory database for tests with MSTest.</span></span> <span data-ttu-id="85239-281">このトピックでは、 [xUnit](https://xunit.github.io/)テスト フレームワーク。</span><span class="sxs-lookup"><span data-stu-id="85239-281">This topic uses the [xUnit](https://xunit.github.io/) test framework.</span></span> <span data-ttu-id="85239-282">テストの概念と別のテスト フレームワークの間でのテストの実装は、似ているが同一でです。</span><span class="sxs-lookup"><span data-stu-id="85239-282">Test concepts and test implementations across different test frameworks are similar but not identical.</span></span>

<span data-ttu-id="85239-283">アプリを使用していないが、[リポジトリ パターン](http://martinfowler.com/eaaCatalog/repository.html)の有効な例が表示されない、[作業単位 (UoW) パターン](https://martinfowler.com/eaaCatalog/unitOfWork.html)、Razor ページには、開発のこれらのパターンがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="85239-283">Although the app doesn't use the [repository pattern](http://martinfowler.com/eaaCatalog/repository.html) and isn't an effective example of the [Unit of Work (UoW) pattern](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor Pages supports these patterns of development.</span></span> <span data-ttu-id="85239-284">詳細については、次を参照してください[インフラストラクチャの永続性レイヤーをデザイン](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design)、 [ASP.NET MVC アプリケーションでリポジトリおよび単位の作業パターンを実装する](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)、および[テスト コント ローラー。ロジック](/aspnet/core/mvc/controllers/testing)(このサンプルは、リポジトリ パターンを実装)。</span><span class="sxs-lookup"><span data-stu-id="85239-284">For more information, see [Designing the infrastructure persistence layer](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), and [Test controller logic](/aspnet/core/mvc/controllers/testing) (the sample implements the repository pattern).</span></span>

### <a name="test-app-organization"></a><span data-ttu-id="85239-285">組織のアプリをテストします。</span><span class="sxs-lookup"><span data-stu-id="85239-285">Test app organization</span></span>

<span data-ttu-id="85239-286">テスト アプリケーションは、コンソール アプリケーション内、 *tests/RazorPagesProject.Tests*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="85239-286">The test app is a console app inside the *tests/RazorPagesProject.Tests* folder.</span></span>

| <span data-ttu-id="85239-287">App フォルダーのテスト</span><span class="sxs-lookup"><span data-stu-id="85239-287">Test app folder</span></span> | <span data-ttu-id="85239-288">説明</span><span class="sxs-lookup"><span data-stu-id="85239-288">Description</span></span> |
| --------------- | ----------- |
| <span data-ttu-id="85239-289">*BasicTests*</span><span class="sxs-lookup"><span data-stu-id="85239-289">*BasicTests*</span></span> | <span data-ttu-id="85239-290">*BasicTests.cs*ルーティング、認証されていないユーザー、セキュリティで保護されたページにアクセスして取得 GitHub ユーザー プロファイル、およびプロファイルのユーザーのログインを確認用のテスト メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="85239-290">*BasicTests.cs* contains test methods for routing, accessing a secure page by an unauthenticated user, and obtaining a GitHub user profile and checking the profile's user login.</span></span> |
| <span data-ttu-id="85239-291">*IntegrationTests*</span><span class="sxs-lookup"><span data-stu-id="85239-291">*IntegrationTests*</span></span> | <span data-ttu-id="85239-292">*IndexPageTests.cs*ユーザー設定を使用して、インデックス ページの統合テストを含む`WebApplicationFactory`クラスです。</span><span class="sxs-lookup"><span data-stu-id="85239-292">*IndexPageTests.cs* contains the integration tests for the Index page using custom `WebApplicationFactory` class.</span></span> |
| <span data-ttu-id="85239-293">*ヘルパー/ユーティリティ*</span><span class="sxs-lookup"><span data-stu-id="85239-293">*Helpers/Utilities*</span></span> | <ul><li><span data-ttu-id="85239-294">*Utilities.cs*が含まれています、`InitializeDbForTests`メソッドでテスト データとデータベースのシードに使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-294">*Utilities.cs* contains the `InitializeDbForTests` method used to seed the database with test data.</span></span></li><li><span data-ttu-id="85239-295">*HtmlHelpers.cs* 、AngleSharp を返すメソッドを提供`IHtmlDocument`テスト メソッドで使用します。</span><span class="sxs-lookup"><span data-stu-id="85239-295">*HtmlHelpers.cs* provides a method to return an AngleSharp `IHtmlDocument` for use by the test methods.</span></span></li><li><span data-ttu-id="85239-296">*HttpClientExtensions.cs*のオーバー ロードを用意`SendAsync`SUT に要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="85239-296">*HttpClientExtensions.cs* provide overloads for `SendAsync` to submit requests to the SUT.</span></span></li></ul> |

<span data-ttu-id="85239-297">テスト フレームワークが[xUnit](https://xunit.github.io/)です。</span><span class="sxs-lookup"><span data-stu-id="85239-297">The test framework is [xUnit](https://xunit.github.io/).</span></span> <span data-ttu-id="85239-298">使用して統合テストが実施、 [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost)が含まれている、 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)です。</span><span class="sxs-lookup"><span data-stu-id="85239-298">Integration tests are conducted using the [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost), which includes the [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver).</span></span> <span data-ttu-id="85239-299">[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)テスト ホストとテスト サーバーを構成するパッケージが使用される、`TestHost`と`TestServer`パッケージは、テスト アプリのプロジェクト ファイルで直接パッケージ参照を必要としない、またはテスト アプリケーションの開発者用の構成。</span><span class="sxs-lookup"><span data-stu-id="85239-299">Because the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package is used to configure the test host and test server, the `TestHost` and `TestServer` packages don't require direct package references in the test app's project file or developer configuration in the test app.</span></span>

<span data-ttu-id="85239-300">**テスト用データベースのシード**</span><span class="sxs-lookup"><span data-stu-id="85239-300">**Seeding the database for testing**</span></span>

<span data-ttu-id="85239-301">通常、統合テストには、テストの実行前にデータベース内の小さなデータセットが必要です。</span><span class="sxs-lookup"><span data-stu-id="85239-301">Integration tests usually require a small dataset in the database prior to the test execution.</span></span> <span data-ttu-id="85239-302">たとえば、削除は、データベースが正常に削除要求の少なくとも 1 つのレコードをいる必要がありますのでデータベース レコードの削除の呼び出しをテストします。</span><span class="sxs-lookup"><span data-stu-id="85239-302">For example, a delete test calls for a database record deletion, so the database must have at least one record for the delete request to succeed.</span></span>

<span data-ttu-id="85239-303">サンプル アプリで次の 3 つのメッセージと共にデータベースがシード処理*Utilities.cs*テストが実行したときに使用できること。</span><span class="sxs-lookup"><span data-stu-id="85239-303">The sample app seeds the database with three messages in *Utilities.cs* that tests can use when they execute:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/Helpers/Utilities.cs?name=snippet1)]

## <a name="additional-resources"></a><span data-ttu-id="85239-304">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="85239-304">Additional resources</span></span>

* [<span data-ttu-id="85239-305">単体テスト</span><span class="sxs-lookup"><span data-stu-id="85239-305">Unit tests</span></span>](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [<span data-ttu-id="85239-306">Razor ページの単体テスト</span><span class="sxs-lookup"><span data-stu-id="85239-306">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)
* [<span data-ttu-id="85239-307">ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="85239-307">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="85239-308">テスト コントローラー</span><span class="sxs-lookup"><span data-stu-id="85239-308">Test controllers</span></span>](xref:mvc/controllers/testing)