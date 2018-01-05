---
title: "ASP.NET Core の概要"
author: rick-anderson
description: "ASP.NET Core の概要を提供する。"
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 12/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: index
ms.openlocfilehash: 3a18ed30819a3d395e9bfb5dba0547667a4425e8
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="7f18e-104">ASP.NET Core の概要</span><span class="sxs-lookup"><span data-stu-id="7f18e-104">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="7f18e-105">著者: [Daniel Roth](https://github.com/danroth27)、[Rick Anderson](https://twitter.com/RickAndMSFT)、[Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="7f18e-105">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="7f18e-106">ASP.NET Core は、インターネットに接続された最新のクラウド ベース アプリケーションを構築するための、クロス プラットフォームで高パフォーマンスの[オープン ソース](https://github.com/aspnet/home) フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="7f18e-106">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="7f18e-107">ASP.NET Core では次のことができます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-107">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="7f18e-108">Web アプリ、Web サービス、[IoT](https://www.microsoft.com/internet-of-things/) アプリ、モバイル バックエンドを構築する。</span><span class="sxs-lookup"><span data-stu-id="7f18e-108">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="7f18e-109">Windows、macOS、Linux で好みの開発ツールを使う。</span><span class="sxs-lookup"><span data-stu-id="7f18e-109">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7f18e-110">クラウドまたはオンプレミスに展開する。</span><span class="sxs-lookup"><span data-stu-id="7f18e-110">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="7f18e-111">[.NET Core または .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server) 上で実行する。</span><span class="sxs-lookup"><span data-stu-id="7f18e-111">Run on [.NET Core or .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="7f18e-112">ASP.NET Core を使う理由</span><span class="sxs-lookup"><span data-stu-id="7f18e-112">Why use ASP.NET Core?</span></span>

<span data-ttu-id="7f18e-113">何百万人もの開発者が、これまで、そして現在も、Web アプリの作成に [ASP.NET 4.x](https://docs.microsoft.com/en-us/aspnet/overview) を使っています。</span><span class="sxs-lookup"><span data-stu-id="7f18e-113">Millions of developers have used (and continue to use) [ASP.NET 4.x](https://docs.microsoft.com/en-us/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="7f18e-114">ASP.NET Core は ASP.NET 4.x を設計し直したものであり、無駄のないモジュール形式のフレームワークになるようにアーキテクチャが変更されています。</span><span class="sxs-lookup"><span data-stu-id="7f18e-114">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

<span data-ttu-id="7f18e-115">ASP.NET Core の利点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7f18e-115">ASP.NET Core provides the following benefits:</span></span>

* <span data-ttu-id="7f18e-116">Web UI と Web API を構築するプロセスの統一。</span><span class="sxs-lookup"><span data-stu-id="7f18e-116">A unified story for building web UI and web APIs.</span></span>
* <span data-ttu-id="7f18e-117">[最新のクライアント側フレームワーク](xref:client-side/index)と開発ワークフローの統合。</span><span class="sxs-lookup"><span data-stu-id="7f18e-117">Integration of [modern, client-side frameworks](xref:client-side/index) and development workflows.</span></span>
* <span data-ttu-id="7f18e-118">クラウド対応で環境ベースの[構成システム](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="7f18e-118">A cloud-ready, environment-based [configuration system](xref:fundamentals/configuration/index).</span></span>
* <span data-ttu-id="7f18e-119">組み込まれている[依存性の注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="7f18e-119">Built-in [dependency injection](xref:fundamentals/dependency-injection).</span></span>
* <span data-ttu-id="7f18e-120">軽量で[高パフォーマンス](https://github.com/aspnet/benchmarks)のモジュール化された HTTP 要求パイプライン。</span><span class="sxs-lookup"><span data-stu-id="7f18e-120">A lightweight, [high-performance](https://github.com/aspnet/benchmarks), and modular HTTP request pipeline.</span></span>
* <span data-ttu-id="7f18e-121">[IIS](xref:publishing/iis)、[Nginx](xref:publishing/linuxproduction)、[Apache](xref:publishing/apache-proxy)、[Docker](xref:publishing/docker) でホストする、または独自のプロセスで自己ホストする機能。</span><span class="sxs-lookup"><span data-stu-id="7f18e-121">Ability to host on [IIS](xref:publishing/iis), [Nginx](xref:publishing/linuxproduction), [Apache](xref:publishing/apache-proxy), [Docker](xref:publishing/docker), or self-host in your own process.</span></span>
* <span data-ttu-id="7f18e-122">[.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server) に対応する場合は、アプリのサイド バイ サイド バージョン管理をサポート。</span><span class="sxs-lookup"><span data-stu-id="7f18e-122">Side-by-side app versioning when targeting [.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
* <span data-ttu-id="7f18e-123">最新の Web 開発を簡単にするツール。</span><span class="sxs-lookup"><span data-stu-id="7f18e-123">Tooling that simplifies modern web development.</span></span>
* <span data-ttu-id="7f18e-124">Windows、macOS、Linux でビルドおよび実行する機能。</span><span class="sxs-lookup"><span data-stu-id="7f18e-124">Ability to build and run on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7f18e-125">オープン ソースで[コミュニティ重視](https://live.asp.net/)。</span><span class="sxs-lookup"><span data-stu-id="7f18e-125">Open-source and [community-focused](https://live.asp.net/).</span></span>

<span data-ttu-id="7f18e-126">ASP.NET Core は、[NuGet](https://www.nuget.org/) パッケージとして完全に提供されます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-126">ASP.NET Core ships entirely as [NuGet](https://www.nuget.org/) packages.</span></span> <span data-ttu-id="7f18e-127">これにより、必要な NuGet パッケージだけを含むようにアプリを最適化できます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-127">This allows you to optimize your app to include only the necessary NuGet packages.</span></span> <span data-ttu-id="7f18e-128">実際に、.NET Core に対応した ASP.NET Core 2.x アプリで必要なのは、[1 つの NuGet パッケージ](xref:fundamentals/metapackage)だけです。</span><span class="sxs-lookup"><span data-stu-id="7f18e-128">In fact, ASP.NET Core 2.x apps targeting .NET Core only require a [single NuGet package](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="7f18e-129">小さいアプリ領域の利点には、セキュリティの強化、サービスの削減、パフォーマンスの向上などがあります。</span><span class="sxs-lookup"><span data-stu-id="7f18e-129">The benefits of a smaller app surface area include tighter security, reduced servicing, and improved performance.</span></span>

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="7f18e-130">ASP.NET Core MVC を使って Web API と Web UI を構築する</span><span class="sxs-lookup"><span data-stu-id="7f18e-130">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="7f18e-131">ASP.NET Core MVC は、[Web API](xref:tutorials/index#building-web-apis) と [Web アプリ](xref:tutorials/index#building-web-applications)を構築する機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="7f18e-131">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/index#building-web-apis) and [web apps](xref:tutorials/index#building-web-applications):</span></span>

* <span data-ttu-id="7f18e-132">[モデル ビュー コントローラー (MVC) パターン](xref:mvc/overview)は、Web API と Web アプリを[テスト可能](testing/index.md)にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-132">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps [testable](testing/index.md).</span></span>
* <span data-ttu-id="7f18e-133">[Razor ページ](xref:mvc/razor-pages/index) (ASP.NET Core 2.0 の新機能) はページ ベースのプログラミング モデルであり、Web UI の開発を容易にし、生産性を高めます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-133">[Razor Pages](xref:mvc/razor-pages/index) (new in ASP.NET Core 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="7f18e-134">[Razor マークアップ](xref:mvc/views/razor)では、[Razor ページ](xref:mvc/razor-pages/index)および [MVC ビュー](xref:mvc/views/overview)用に生産性の高い構文が提供されます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-134">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:mvc/razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="7f18e-135">[タグ ヘルパー](xref:mvc/views/tag-helpers/intro)を使うと、Razor ファイルでの HTML 要素の作成とレンダリングに、サーバー側コードを組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-135">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="7f18e-136">[複数のデータ形式とコンテンツ ネゴシエーション](mvc/models/formatting.md)の組み込みサポートにより、Web API はブラウザーやモバイル デバイスなどのさまざまなクライアントと接続できます。</span><span class="sxs-lookup"><span data-stu-id="7f18e-136">Built-in support for [multiple data formats and content negotiation](mvc/models/formatting.md) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="7f18e-137">[モデル バインド](xref:mvc/models/model-binding)は、HTTP 要求からアクション メソッドのパラメーターにデータを自動的にマップします。</span><span class="sxs-lookup"><span data-stu-id="7f18e-137">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="7f18e-138">[モデル検証](xref:mvc/models/validation)は、クライアント側とサーバー側の検証を自動的に実行します。</span><span class="sxs-lookup"><span data-stu-id="7f18e-138">[Model validation](xref:mvc/models/validation) automatically performs client- and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="7f18e-139">クライアント側の開発</span><span class="sxs-lookup"><span data-stu-id="7f18e-139">Client-side development</span></span>

<span data-ttu-id="7f18e-140">ASP.NET Core は、人気のあるクライアント側のフレームワークとライブラリ ([Angular](xref:spa/angular)、[React](xref:spa/react)、[Bootstrap](xref:client-side/bootstrap) など) をシームレスに統合します。</span><span class="sxs-lookup"><span data-stu-id="7f18e-140">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](xref:client-side/bootstrap).</span></span> <span data-ttu-id="7f18e-141">詳しくは、「[クライアント側の開発](xref:client-side/index)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7f18e-141">See [Client-side development](xref:client-side/index) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f18e-142">次のステップ</span><span class="sxs-lookup"><span data-stu-id="7f18e-142">Next steps</span></span>

<span data-ttu-id="7f18e-143">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7f18e-143">For more information, see the following resources:</span></span>

* [<span data-ttu-id="7f18e-144">ASP.NET Core チュートリアル</span><span class="sxs-lookup"><span data-stu-id="7f18e-144">ASP.NET Core tutorials</span></span>](xref:tutorials/index)
* [<span data-ttu-id="7f18e-145">ASP.NET Core の基礎</span><span class="sxs-lookup"><span data-stu-id="7f18e-145">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="7f18e-146">[週 1 回の ASP.NET Community Standup](https://live.asp.net/) では、チームの進行状況とプランが報告され、</span><span class="sxs-lookup"><span data-stu-id="7f18e-146">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="7f18e-147">新しいブログやサード パーティ製ソフトウェアが取り上げられています。</span><span class="sxs-lookup"><span data-stu-id="7f18e-147">It features new blogs and third-party software.</span></span>