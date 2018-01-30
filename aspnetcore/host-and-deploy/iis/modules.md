---
title: "ASP.NET Core で IIS のモジュールの使用"
author: guardrex
description: "ASP.NET Core アプリケーションのアクティブおよび非アクティブの IIS モジュールを記述する参照ドキュメント。"
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 03/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: host-and-deploy/iis/modules
ms.openlocfilehash: 405297bdd1ceac390b995ed6e15ae8d95bb8501f
ms.sourcegitcommit: a3e88639a6bcf8fb4d634036dac93130c464a097
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2018
---
# <a name="using-iis-modules-with-aspnet-core"></a><span data-ttu-id="aabb3-103">ASP.NET Core で IIS のモジュールの使用</span><span class="sxs-lookup"><span data-stu-id="aabb3-103">Using IIS Modules with ASP.NET Core</span></span>

<span data-ttu-id="aabb3-104">作成者: [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="aabb3-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="aabb3-105">ASP.NET Core アプリケーションは、リバース プロキシの構成では IIS によってホストされます。</span><span class="sxs-lookup"><span data-stu-id="aabb3-105">ASP.NET Core applications are hosted by IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="aabb3-106">IIS のネイティブ モジュールの一部とすべての IIS 管理モジュールは、ASP.NET Core アプリケーションの要求の処理に使用できません。</span><span class="sxs-lookup"><span data-stu-id="aabb3-106">Some of the native IIS modules and all of the IIS managed modules aren't available to process requests for ASP.NET Core apps.</span></span> <span data-ttu-id="aabb3-107">多くの場合は、ASP.NET Core は、代わりに IIS のネイティブおよびマネージ モジュールの機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-107">In many cases, ASP.NET Core offers an alternative to the features of IIS native and managed modules.</span></span>

## <a name="native-modules"></a><span data-ttu-id="aabb3-108">ネイティブ モジュール</span><span class="sxs-lookup"><span data-stu-id="aabb3-108">Native Modules</span></span>

<span data-ttu-id="aabb3-109">Module</span><span class="sxs-lookup"><span data-stu-id="aabb3-109">Module</span></span> | <span data-ttu-id="aabb3-110">.NET Core Active</span><span class="sxs-lookup"><span data-stu-id="aabb3-110">.NET Core Active</span></span> | <span data-ttu-id="aabb3-111">ASP.NET Core Option</span><span class="sxs-lookup"><span data-stu-id="aabb3-111">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="aabb3-112">**匿名認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-112">**Anonymous Authentication**</span></span><br>`AnonymousAuthenticationModule` | <span data-ttu-id="aabb3-113">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-113">Yes</span></span> | 
<span data-ttu-id="aabb3-114">**基本認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-114">**Basic Authentication**</span></span><br>`BasicAuthenticationModule` | <span data-ttu-id="aabb3-115">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-115">Yes</span></span> | 
<span data-ttu-id="aabb3-116">**クライアント証明書マッピング認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-116">**Client Certification Mapping Authentication**</span></span><br>`CertificateMappingAuthenticationModule` | <span data-ttu-id="aabb3-117">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-117">Yes</span></span> | 
<span data-ttu-id="aabb3-118">**CGI**</span><span class="sxs-lookup"><span data-stu-id="aabb3-118">**CGI**</span></span><br>`CgiModule` | <span data-ttu-id="aabb3-119">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-119">No</span></span> | 
<span data-ttu-id="aabb3-120">**構成の検証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-120">**Configuration Validation**</span></span><br>`ConfigurationValidationModule` | <span data-ttu-id="aabb3-121">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-121">Yes</span></span> | 
<span data-ttu-id="aabb3-122">**HTTP エラー**</span><span class="sxs-lookup"><span data-stu-id="aabb3-122">**HTTP Errors**</span></span><br>`CustomErrorModule` | <span data-ttu-id="aabb3-123">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-123">No</span></span> | [<span data-ttu-id="aabb3-124">ステータス コード ページ ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-124">Status Code Pages Middleware</span></span>](xref:fundamentals/error-handling#configuring-status-code-pages)
<span data-ttu-id="aabb3-125">**カスタム ログ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-125">**Custom Logging**</span></span><br>`CustomLoggingModule` | <span data-ttu-id="aabb3-126">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-126">Yes</span></span> | 
<span data-ttu-id="aabb3-127">**既定のドキュメント**</span><span class="sxs-lookup"><span data-stu-id="aabb3-127">**Default Document**</span></span><br>`DefaultDocumentModule` | <span data-ttu-id="aabb3-128">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-128">No</span></span> | [<span data-ttu-id="aabb3-129">既定のファイルのミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-129">Default Files Middleware</span></span>](xref:fundamentals/static-files#serve-a-default-document)
<span data-ttu-id="aabb3-130">**ダイジェスト認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-130">**Digest Authentication**</span></span><br>`DigestAuthenticationModule` | <span data-ttu-id="aabb3-131">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-131">Yes</span></span> | 
<span data-ttu-id="aabb3-132">**ディレクトリの参照**</span><span class="sxs-lookup"><span data-stu-id="aabb3-132">**Directory Browsing**</span></span><br>`DirectoryListingModule` | <span data-ttu-id="aabb3-133">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-133">No</span></span> | [<span data-ttu-id="aabb3-134">ディレクトリ参照ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-134">Directory Browsing Middleware</span></span>](xref:fundamentals/static-files#enable-directory-browsing)
<span data-ttu-id="aabb3-135">**動的な圧縮**</span><span class="sxs-lookup"><span data-stu-id="aabb3-135">**Dynamic Compression**</span></span><br>`DynamicCompressionModule` | <span data-ttu-id="aabb3-136">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-136">Yes</span></span> | [<span data-ttu-id="aabb3-137">応答圧縮ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-137">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="aabb3-138">**トレース**</span><span class="sxs-lookup"><span data-stu-id="aabb3-138">**Tracing**</span></span><br>`FailedRequestsTracingModule` | <span data-ttu-id="aabb3-139">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-139">Yes</span></span> | [<span data-ttu-id="aabb3-140">ASP.NET Core のログ記録</span><span class="sxs-lookup"><span data-stu-id="aabb3-140">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index#the-tracesource-provider)
<span data-ttu-id="aabb3-141">**ファイルのキャッシュ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-141">**File Caching**</span></span><br>`FileCacheModule` | <span data-ttu-id="aabb3-142">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-142">No</span></span> | [<span data-ttu-id="aabb3-143">応答キャッシュ ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-143">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="aabb3-144">**HTTP キャッシュ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-144">**HTTP Caching**</span></span><br>`HttpCacheModule` | <span data-ttu-id="aabb3-145">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-145">No</span></span> | [<span data-ttu-id="aabb3-146">応答キャッシュ ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-146">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="aabb3-147">**HTTP ログ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-147">**HTTP Logging**</span></span><br>`HttpLoggingModule` | <span data-ttu-id="aabb3-148">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-148">Yes</span></span> | [<span data-ttu-id="aabb3-149">ASP.NET Core のログ記録</span><span class="sxs-lookup"><span data-stu-id="aabb3-149">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index)<br><span data-ttu-id="aabb3-150">実装: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging)、 [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)、 [NLog](https://github.com/NLog/NLog.Extensions.Logging)、 [Serilog](https://github.com/serilog/serilog-extensions-logging)</span><span class="sxs-lookup"><span data-stu-id="aabb3-150">Implementations: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span></span>
<span data-ttu-id="aabb3-151">**HTTP リダイレクト**</span><span class="sxs-lookup"><span data-stu-id="aabb3-151">**HTTP Redirection**</span></span><br>`HttpRedirectionModule` | <span data-ttu-id="aabb3-152">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-152">Yes</span></span> | [<span data-ttu-id="aabb3-153">URL リライト ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="aabb3-154">**IIS クライアント証明書マッピング認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-154">**IIS Client Certificate Mapping Authentication**</span></span><br>`IISCertificateMappingAuthenticationModule` | <span data-ttu-id="aabb3-155">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-155">Yes</span></span> | 
<span data-ttu-id="aabb3-156">**IP およびドメインの制限**</span><span class="sxs-lookup"><span data-stu-id="aabb3-156">**IP and Domain Restrictions**</span></span><br>`IpRestrictionModule` | <span data-ttu-id="aabb3-157">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-157">Yes</span></span> | 
<span data-ttu-id="aabb3-158">**ISAPI フィルター**</span><span class="sxs-lookup"><span data-stu-id="aabb3-158">**ISAPI Filters**</span></span><br>`IsapiFilterModule` | <span data-ttu-id="aabb3-159">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-159">Yes</span></span> | [<span data-ttu-id="aabb3-160">ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-160">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="aabb3-161">**ISAPI**</span><span class="sxs-lookup"><span data-stu-id="aabb3-161">**ISAPI**</span></span><br>`IsapiModule` | <span data-ttu-id="aabb3-162">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-162">Yes</span></span> | [<span data-ttu-id="aabb3-163">ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-163">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="aabb3-164">**プロトコルのサポート**</span><span class="sxs-lookup"><span data-stu-id="aabb3-164">**Protocol Support**</span></span><br>`ProtocolSupportModule` | <span data-ttu-id="aabb3-165">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-165">Yes</span></span> | 
<span data-ttu-id="aabb3-166">**要求のフィルタリング**</span><span class="sxs-lookup"><span data-stu-id="aabb3-166">**Request Filtering**</span></span><br>`RequestFilteringModule` | <span data-ttu-id="aabb3-167">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-167">Yes</span></span> | [<span data-ttu-id="aabb3-168">URL 書き換えミドルウェア`IRule`</span><span class="sxs-lookup"><span data-stu-id="aabb3-168">URL Rewriting Middleware `IRule`</span></span>](xref:fundamentals/url-rewriting#irule-based-rule)
<span data-ttu-id="aabb3-169">**要求監視**</span><span class="sxs-lookup"><span data-stu-id="aabb3-169">**Request Monitor**</span></span><br>`RequestMonitorModule` | <span data-ttu-id="aabb3-170">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-170">Yes</span></span> | 
<span data-ttu-id="aabb3-171">**URL 書き換え**</span><span class="sxs-lookup"><span data-stu-id="aabb3-171">**URL Rewriting**</span></span><br>`RewriteModule` | <span data-ttu-id="aabb3-172">Yes†</span><span class="sxs-lookup"><span data-stu-id="aabb3-172">Yes†</span></span> | [<span data-ttu-id="aabb3-173">URL リライト ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-173">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="aabb3-174">**サーバー側インクルード**</span><span class="sxs-lookup"><span data-stu-id="aabb3-174">**Server Side Includes**</span></span><br>`ServerSideIncludeModule` | <span data-ttu-id="aabb3-175">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-175">No</span></span> | 
<span data-ttu-id="aabb3-176">**静的な圧縮**</span><span class="sxs-lookup"><span data-stu-id="aabb3-176">**Static Compression**</span></span><br>`StaticCompressionModule` | <span data-ttu-id="aabb3-177">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-177">No</span></span> | [<span data-ttu-id="aabb3-178">応答圧縮ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-178">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="aabb3-179">**静的コンテンツ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-179">**Static Content**</span></span><br>`StaticFileModule` | <span data-ttu-id="aabb3-180">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-180">No</span></span> | [<span data-ttu-id="aabb3-181">静的ファイル ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-181">Static File Middleware</span></span>](xref:fundamentals/static-files)
<span data-ttu-id="aabb3-182">**トークンのキャッシュ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-182">**Token Caching**</span></span><br>`TokenCacheModule` | <span data-ttu-id="aabb3-183">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-183">Yes</span></span> | 
<span data-ttu-id="aabb3-184">**URI のキャッシュ**</span><span class="sxs-lookup"><span data-stu-id="aabb3-184">**URI Caching**</span></span><br>`UriCacheModule` | <span data-ttu-id="aabb3-185">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-185">Yes</span></span> | 
<span data-ttu-id="aabb3-186">**URL 認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-186">**URL Authorization**</span></span><br>`UrlAuthorizationModule` | <span data-ttu-id="aabb3-187">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-187">Yes</span></span> | [<span data-ttu-id="aabb3-188">ASP.NET Core Identity</span><span class="sxs-lookup"><span data-stu-id="aabb3-188">ASP.NET Core Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="aabb3-189">**Windows 認証**</span><span class="sxs-lookup"><span data-stu-id="aabb3-189">**Windows Authentication**</span></span><br>`WindowsAuthenticationModule` | <span data-ttu-id="aabb3-190">[はい]</span><span class="sxs-lookup"><span data-stu-id="aabb3-190">Yes</span></span> | 

<span data-ttu-id="aabb3-191">URL Rewrite Module を †The`isFile`と`isDirectory`の変更のための ASP.NET Core アプリケーションと連携しない[ディレクトリ構造](xref:host-and-deploy/directory-structure)です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-191">†The URL Rewrite Module's `isFile` and `isDirectory` don't work with ASP.NET Core apps due to the changes in [directory structure](xref:host-and-deploy/directory-structure).</span></span>

## <a name="managed-modules"></a><span data-ttu-id="aabb3-192">マネージ モジュール</span><span class="sxs-lookup"><span data-stu-id="aabb3-192">Managed Modules</span></span>

<span data-ttu-id="aabb3-193">Module</span><span class="sxs-lookup"><span data-stu-id="aabb3-193">Module</span></span> | <span data-ttu-id="aabb3-194">.NET Core Active</span><span class="sxs-lookup"><span data-stu-id="aabb3-194">.NET Core Active</span></span> | <span data-ttu-id="aabb3-195">ASP.NET Core Option</span><span class="sxs-lookup"><span data-stu-id="aabb3-195">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="aabb3-196">AnonymousIdentification</span><span class="sxs-lookup"><span data-stu-id="aabb3-196">AnonymousIdentification</span></span> | <span data-ttu-id="aabb3-197">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-197">No</span></span> | 
<span data-ttu-id="aabb3-198">DefaultAuthentication</span><span class="sxs-lookup"><span data-stu-id="aabb3-198">DefaultAuthentication</span></span> | <span data-ttu-id="aabb3-199">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-199">No</span></span> | 
<span data-ttu-id="aabb3-200">FileAuthorization</span><span class="sxs-lookup"><span data-stu-id="aabb3-200">FileAuthorization</span></span> | <span data-ttu-id="aabb3-201">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-201">No</span></span> | 
<span data-ttu-id="aabb3-202">FormsAuthentication</span><span class="sxs-lookup"><span data-stu-id="aabb3-202">FormsAuthentication</span></span> | <span data-ttu-id="aabb3-203">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-203">No</span></span> | [<span data-ttu-id="aabb3-204">Cookie 認証ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-204">Cookie Authentication Middleware</span></span>](xref:security/authentication/cookie)
<span data-ttu-id="aabb3-205">OutputCache</span><span class="sxs-lookup"><span data-stu-id="aabb3-205">OutputCache</span></span> | <span data-ttu-id="aabb3-206">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-206">No</span></span> | [<span data-ttu-id="aabb3-207">応答キャッシュ ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-207">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="aabb3-208">Profile</span><span class="sxs-lookup"><span data-stu-id="aabb3-208">Profile</span></span> | <span data-ttu-id="aabb3-209">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-209">No</span></span> | 
<span data-ttu-id="aabb3-210">RoleManager</span><span class="sxs-lookup"><span data-stu-id="aabb3-210">RoleManager</span></span> | <span data-ttu-id="aabb3-211">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-211">No</span></span> | 
<span data-ttu-id="aabb3-212">ScriptModule-4.0</span><span class="sxs-lookup"><span data-stu-id="aabb3-212">ScriptModule-4.0</span></span> | <span data-ttu-id="aabb3-213">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-213">No</span></span> | 
<span data-ttu-id="aabb3-214">セッション</span><span class="sxs-lookup"><span data-stu-id="aabb3-214">Session</span></span> | <span data-ttu-id="aabb3-215">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-215">No</span></span> | [<span data-ttu-id="aabb3-216">セッションのミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-216">Session Middleware</span></span>](xref:fundamentals/app-state)
<span data-ttu-id="aabb3-217">UrlAuthorization</span><span class="sxs-lookup"><span data-stu-id="aabb3-217">UrlAuthorization</span></span> | <span data-ttu-id="aabb3-218">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-218">No</span></span> | 
<span data-ttu-id="aabb3-219">UrlMappingsModule</span><span class="sxs-lookup"><span data-stu-id="aabb3-219">UrlMappingsModule</span></span> | <span data-ttu-id="aabb3-220">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-220">No</span></span> | [<span data-ttu-id="aabb3-221">URL リライト ミドルウェア</span><span class="sxs-lookup"><span data-stu-id="aabb3-221">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="aabb3-222">UrlRoutingModule-4.0</span><span class="sxs-lookup"><span data-stu-id="aabb3-222">UrlRoutingModule-4.0</span></span> | <span data-ttu-id="aabb3-223">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-223">No</span></span> | [<span data-ttu-id="aabb3-224">ASP.NET Core  Identity</span><span class="sxs-lookup"><span data-stu-id="aabb3-224">ASP.NET Core  Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="aabb3-225">WindowsAuthentication</span><span class="sxs-lookup"><span data-stu-id="aabb3-225">WindowsAuthentication</span></span> | <span data-ttu-id="aabb3-226">×</span><span class="sxs-lookup"><span data-stu-id="aabb3-226">No</span></span> | 

## <a name="iis-manager-application-changes"></a><span data-ttu-id="aabb3-227">IIS マネージャー アプリケーションの変更</span><span class="sxs-lookup"><span data-stu-id="aabb3-227">IIS Manager application changes</span></span>

<span data-ttu-id="aabb3-228">IIS マネージャーを使用して設定を構成する、 *web.config*アプリのファイルを変更します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-228">Using IIS Manager to configure settings, the *web.config* file of the app is changed.</span></span> <span data-ttu-id="aabb3-229">アプリを配置する場合と*web.config*、IIS マネージャーで行った変更は上書きして、デプロイされている*web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="aabb3-229">If deploying an app and including *web.config*, any changes made with IIS Manger are overwritten by the deployed *web.config* file.</span></span> <span data-ttu-id="aabb3-230">サーバーの変更が加えられた場合*web.config*ファイル、コピー、更新された*web.config*ファイルをローカルのプロジェクトをすぐにします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-230">If changes are made to the server's *web.config* file, copy the updated *web.config* file to the local project immediately.</span></span>

## <a name="disabling-iis-modules"></a><span data-ttu-id="aabb3-231">IIS モジュールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-231">Disabling IIS modules</span></span>

<span data-ttu-id="aabb3-232">IIS モジュールが、アプリでアプリへの追記を無効にする必要がありますサーバー レベルで構成されているかどうか*web.config*ファイルには、モジュールが無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="aabb3-232">If an IIS module is configured at the server level that must be disabled for an app, an addition to the app's *web.config* file can disable the module.</span></span> <span data-ttu-id="aabb3-233">モジュールをそのまま残す (使用可能な場合)、構成の設定を使用して、非アクティブか、アプリからモジュールを削除します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-233">Either leave the module in place and deactivate it using a configuration setting (if available) or remove the module from the app.</span></span>

### <a name="module-deactivation"></a><span data-ttu-id="aabb3-234">モジュールの非アクティブ化</span><span class="sxs-lookup"><span data-stu-id="aabb3-234">Module deactivation</span></span>

<span data-ttu-id="aabb3-235">多くのモジュールは、削除せずに、アプリから実行できるように構成の設定が無効に用意されています。</span><span class="sxs-lookup"><span data-stu-id="aabb3-235">Many modules offer a configuration setting that allows them to be disabled them without removing them from the app.</span></span> <span data-ttu-id="aabb3-236">これは、モジュールを非アクティブ化する最も簡単なと最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-236">This is the simplest and quickest way to deactivate a module.</span></span> <span data-ttu-id="aabb3-237">IIS URL Rewrite モジュールを無効にしたい場合など、使用、`<httpRedirect>`次に示すようにします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-237">For example if wishing to disable the IIS URL Rewrite Module, use the `<httpRedirect>` element as shown below.</span></span> <span data-ttu-id="aabb3-238">モジュールの構成設定を無効にする方法の詳細については、以下のリンク、*子要素*のセクション[IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/)です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-238">For more information on disabling modules with configuration settings, follow the links in the *Child Elements* section of [IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/).</span></span>

```xml
<configuration>
  <system.webServer>
     <httpRedirect enabled="false" />
  </system.webServer>
</configuration>
```

### <a name="module-removal"></a><span data-ttu-id="aabb3-239">モジュールの取り外し</span><span class="sxs-lookup"><span data-stu-id="aabb3-239">Module removal</span></span>

<span data-ttu-id="aabb3-240">設定と、モジュールを削除しなかった場合は*web.config*モジュールのロックを解除、およびロック解除、`<modules>`のセクション*web.config*最初。</span><span class="sxs-lookup"><span data-stu-id="aabb3-240">If opting to remove a module with a setting in *web.config*, unlock the module and unlock the `<modules>` section of *web.config* first.</span></span> <span data-ttu-id="aabb3-241">手順を次に説明します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-241">The steps are outlined below:</span></span>

1. <span data-ttu-id="aabb3-242">サーバー レベルのモジュールのロックを解除します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-242">Unlock the module at the server level.</span></span> <span data-ttu-id="aabb3-243">IIS サーバー、IIS マネージャーの **接続**サイドバーです。</span><span class="sxs-lookup"><span data-stu-id="aabb3-243">Click on the IIS server in the IIS Manager **Connections** sidebar.</span></span> <span data-ttu-id="aabb3-244">開く、**モジュール**で、 **IIS**領域。</span><span class="sxs-lookup"><span data-stu-id="aabb3-244">Open the **Modules** in the **IIS** area.</span></span> <span data-ttu-id="aabb3-245">リスト内のモジュールをクリックします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-245">Click on the module in the list.</span></span> <span data-ttu-id="aabb3-246">**アクション**、右側のサイド バーをクリックして**Unlock**です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-246">In the **Actions** sidebar on the right, click **Unlock**.</span></span> <span data-ttu-id="aabb3-247">削除する計画どおりに多くのモジュールのロックを解除*web.config*以降。</span><span class="sxs-lookup"><span data-stu-id="aabb3-247">Unlock as many modules as are planned to remove from *web.config* later.</span></span>

2. <span data-ttu-id="aabb3-248">アプリを展開することがなく、 `<modules>` 」の「 *web.config*です。アプリが展開された場合、 *web.config*を含む、`<modules>`セクションがロックを解除セクション最初、IIS マネージャーで、Configuration Manager なしは、セクションのロック解除しようとするときに例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-248">Deploy the app without a `<modules>` section in *web.config*. If an app is deployed with a *web.config* containing the `<modules>` section without having unlocked the section first in the IIS Manager, the Configuration Manager throws an exception when attempting to unlock the section.</span></span> <span data-ttu-id="aabb3-249">そのため、アプリを展開することがなく、`<modules>`セクションです。</span><span class="sxs-lookup"><span data-stu-id="aabb3-249">Therefore, deploy the app without a `<modules>` section.</span></span>

3. <span data-ttu-id="aabb3-250">ロックを解除、`<modules>`のセクション*web.config*です。**接続**をサイド バーに web サイトをクリックして**サイト**です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-250">Unlock the `<modules>` section of *web.config*. In the **Connections** sidebar, click the website in **Sites**.</span></span> <span data-ttu-id="aabb3-251">**管理**領域で、開く、**構成エディター**です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-251">In the **Management** area, open the **Configuration Editor**.</span></span> <span data-ttu-id="aabb3-252">ナビゲーション コントロールを使用して、`system.webServer/modules`セクションです。</span><span class="sxs-lookup"><span data-stu-id="aabb3-252">Use the navigation controls to select the `system.webServer/modules` section.</span></span> <span data-ttu-id="aabb3-253">**アクション**をクリックして、右側のサイドバー **Unlock**セクションです。</span><span class="sxs-lookup"><span data-stu-id="aabb3-253">In the **Actions** sidebar on the right, click to **Unlock** the section.</span></span>

4. <span data-ttu-id="aabb3-254">この時点で、`<modules>`セクションに追加できる、 *web.config*ファイルと、`<remove>`アプリからモジュールを削除する要素。</span><span class="sxs-lookup"><span data-stu-id="aabb3-254">At this point, a `<modules>` section can be added to the *web.config* file with a `<remove>` element to remove the module from the app.</span></span> <span data-ttu-id="aabb3-255">複数`<remove>`を複数のモジュールを削除する要素を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="aabb3-255">Multiple `<remove>` elements can be added to remove multiple modules.</span></span> <span data-ttu-id="aabb3-256">忘れずにいる場合*web.config*変更されるサーバーでプロジェクトをローカルにすぐに実行します。</span><span class="sxs-lookup"><span data-stu-id="aabb3-256">Don't forget that if *web.config* changes are made on the server to make them immediately in the project locally.</span></span> <span data-ttu-id="aabb3-257">こうすると、モジュールを削除すると、サーバー上の他のアプリを使用してモジュールの使用は影響しません。</span><span class="sxs-lookup"><span data-stu-id="aabb3-257">Removing a module this way won't affect the use of the module with other apps on the server.</span></span>

  ```xml
  <configuration> 
    <system.webServer> 
      <modules> 
        <remove name="MODULE_NAME" /> 
      </modules> 
    </system.webServer> 
  </configuration>
  ```

<span data-ttu-id="aabb3-258">IIS のインストールでインストールされている既定のモジュールには、次を使用して`<module>`を既定のモジュールを削除する」セクション。</span><span class="sxs-lookup"><span data-stu-id="aabb3-258">For an IIS installation with the default modules installed, use the following `<module>` section to remove the default modules.</span></span>

```xml
<modules>
  <remove name="CustomErrorModule" />
  <remove name="DefaultDocumentModule" />
  <remove name="DirectoryListingModule" />
  <remove name="HttpCacheModule" />
  <remove name="HttpLoggingModule" />
  <remove name="ProtocolSupportModule" />
  <remove name="RequestFilteringModule" />
  <remove name="StaticCompressionModule" /> 
  <remove name="StaticFileModule" /> 
</modules>
```

<span data-ttu-id="aabb3-259">IIS モジュールを削除することができますも*Appcmd.exe*です。</span><span class="sxs-lookup"><span data-stu-id="aabb3-259">An IIS module can also be removed with *Appcmd.exe*.</span></span> <span data-ttu-id="aabb3-260">提供、`MODULE_NAME`と`APPLICATION_NAME`次に示すコマンドで。</span><span class="sxs-lookup"><span data-stu-id="aabb3-260">Provide the `MODULE_NAME` and `APPLICATION_NAME` in the command shown below:</span></span>

```console
Appcmd.exe delete module MODULE_NAME /app.name:APPLICATION_NAME
```

<span data-ttu-id="aabb3-261">ここでは削除する方法、`DynamicCompressionModule`既定の Web サイトから。</span><span class="sxs-lookup"><span data-stu-id="aabb3-261">Here's how to remove the `DynamicCompressionModule` from the Default Web Site:</span></span>

```console
%windir%\system32\inetsrv\appcmd.exe delete module DynamicCompressionModule /app.name:"Default Web Site"
```

## <a name="minimum-module-configuration"></a><span data-ttu-id="aabb3-262">最小限のモジュールの構成</span><span class="sxs-lookup"><span data-stu-id="aabb3-262">Minimum module configuration</span></span>

<span data-ttu-id="aabb3-263">ASP.NET Core アプリケーションを実行するために必要なだけモジュールとは、匿名の認証モジュールおよび ASP.NET Core モジュールです。</span><span class="sxs-lookup"><span data-stu-id="aabb3-263">The only modules required to run an ASP.NET Core app are the Anonymous Authentication Module and the ASP.NET Core Module.</span></span>

![最小限のモジュールの構成とモジュールに IIS マネージャーを開く](modules/_static/modules.png)

## <a name="additional-resources"></a><span data-ttu-id="aabb3-265">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="aabb3-265">Additional resources</span></span>

* [<span data-ttu-id="aabb3-266">IIS による Windows 上のホスト</span><span class="sxs-lookup"><span data-stu-id="aabb3-266">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="aabb3-267">IIS のモジュールの概要</span><span class="sxs-lookup"><span data-stu-id="aabb3-267">IIS Modules Overview</span></span>](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
* [<span data-ttu-id="aabb3-268">IIS 7.0 ロール、およびモジュールをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="aabb3-268">Customizing IIS 7.0 Roles and Modules</span></span>](https://technet.microsoft.com/library/cc627313.aspx)
* [<span data-ttu-id="aabb3-269">IIS `<system.webServer>`</span><span class="sxs-lookup"><span data-stu-id="aabb3-269">IIS `<system.webServer>`</span></span>](https://docs.microsoft.com/iis/configuration/system.webServer/)