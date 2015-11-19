ASP.NET MVC application thing to watch out for, especially after deploying the application (new release).

**Symptom:**

Rendering ASP.NET MVC page throws `System.ArgumentException: An item with the same key has already been added` (particularly across any / all views in app, not just a specific one)

**Likely cause:**

Race condition bug in older version of Telerik library

**Workaround:**

Manually recycle app domain or touch web.config (update it)

http://stackoverflow.com/questions/13321205/loading-any-mvc-page-fails-with-the-error-an-item-with-the-same-key-has-already

**Other Solutions:**

Remove/upgrade Telerik library


----
TLDR;

Example full stack trace:
```
System.ArgumentException: An item with the same key has already been added. at System.ThrowHelper.ThrowArgumentException(ExceptionResource resource) at 
System.Collections.Generic.Dictionary`2.Insert(TKey key, TValue value, Boolean add) at
System.Linq.Enumerable.ToDictionary[TSource,TKey,TElement](IEnumerable`1 source, Func`2 keySelector, Func`2 elementSelector, IEqualityComparer`1 comparer) at 
System.Web.WebPages.Scope.WebConfigScopeDictionary.<>c__DisplayClass4.<.ctor>b__0() at 
System.Lazy`1.CreateValue() 

-- End of stack trace from previous location where exception was thrown -- at 
System.Runtime.ExceptionServices.ExceptionDispatchInfo.Throw() at 
System.Lazy`1.get_Value() at 
System.Web.WebPages.Scope.WebConfigScopeDictionary.TryGetValue(Object key, Object& value) at 
System.Web.WebPages.Scope.ScopeStorageDictionary.TryGetValue(Object key, Object& value) at 
System.Web.WebPages.Scope.ScopeStorageDictionary.TryGetValue(Object key, Object& value) at
System.Web.Mvc.ViewContext.ScopeGet[TValue](IDictionary`2 scope, String name, TValue defaultValue) at 
System.Web.Mvc.ViewContext.ScopeCache..ctor(IDictionary`2 scope) at 
System.Web.Mvc.ViewContext.ScopeCache.Get(IDictionary`2 scope, HttpContextBase httpContext) at 
System.Web.Mvc.ViewContext.set_ClientValidationEnabled(Boolean value) at 
System.Web.Mvc.HtmlHelper.EnableClientValidation() at 
ASP._Page_Views_Orders_OrderManagement_cshtml.Execute() 
in e:\wwwroot\fswadmin\Views\Orders\OrderManagement.cshtml:line 6 at 
System.Web.WebPages.WebPageBase.ExecutePageHierarchy() at 
System.Web.Mvc.WebViewPage.ExecutePageHierarchy() at 
System.Web.WebPages.WebPageBase.ExecutePageHierarchy(WebPageContext pageContext, TextWriter writer, WebPageRenderingBase startPage) at 
System.Web.Mvc.RazorView.RenderView(ViewContext viewContext, TextWriter writer, Object instance) at 
System.Web.Mvc.BuildManagerCompiledView.Render(ViewContext viewContext, TextWriter writer) at 
System.Web.Mvc.ViewResultBase.ExecuteResult(ControllerContext context) at 
System.Web.Mvc.ControllerActionInvoker.InvokeActionResult(ControllerContext controllerContext, ActionResult actionResult) at 
System.Web.Mvc.ControllerActionInvoker.<>c__DisplayClass1a.b__17() at 
System.Web.Mvc.ControllerActionInvoker.InvokeActionResultFilter(IResultFilter filter, ResultExecutingContext preContext, Func`1 continuation) at 
System.Web.Mvc.ControllerActionInvoker.<>c__DisplayClass1a.<>c__DisplayClass1c.b__19() at 
System.Web.Mvc.ControllerActionInvoker.InvokeActionResultFilter(IResultFilter filter, ResultExecutingContext preContext, Func`1 continuation) at 
System.Web.Mvc.ControllerActionInvoker.<>c__DisplayClass1a.<>c__DisplayClass1c.b__19() at 
System.Web.Mvc.ControllerActionInvoker.InvokeActionResultWithFilters(ControllerContext controllerContext, IList`1 filters, ActionResult actionResult) at 
System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass25.<>c__DisplayClass2a.b__20() at 
System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass25.b__22(IAsyncResult asyncResult) at 
System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.End() at 
System.Web.Mvc.Async.AsyncControllerActionInvoker.EndInvokeAction(IAsyncResult asyncResult) at 
System.Web.Mvc.Controller.<>c__DisplayClass1d.b__18(IAsyncResult asyncResult) at 
System.Web.Mvc.Async.AsyncResultWrapper.<>c__DisplayClass4.b__3(IAsyncResult ar) at System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.End() at 
System.Web.Mvc.Controller.EndExecuteCore(IAsyncResult asyncResult) at 
System.Web.Mvc.Async.AsyncResultWrapper.<>c__DisplayClass4.b__3(IAsyncResult ar) at 
System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.End() at 
System.Web.Mvc.Controller.EndExecute(IAsyncResult asyncResult) at 
System.Web.Mvc.Controller.System.Web.Mvc.Async.IAsyncController.EndExecute(IAsyncResult asyncResult) at 
System.Web.Mvc.MvcHandler.<>c__DisplayClass8.b__3(IAsyncResult asyncResult) at 
System.Web.Mvc.Async.AsyncResultWrapper.<>c__DisplayClass4.b__3(IAsyncResult ar) at 
System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.End() at 
System.Web.Mvc.MvcHandler.EndProcessRequest(IAsyncResult asyncResult) at 
System.Web.Mvc.MvcHandler.System.Web.IHttpAsyncHandler.EndProcessRequest(IAsyncResult result) at 
System.Web.HttpApplication.CallHandlerExecutionStep.System.Web.HttpApplication.IExecutionStep.Execute() at 
System.Web.HttpApplication.ExecuteStep(IExecutionStep step, Boolean& completedSynchronously)
```