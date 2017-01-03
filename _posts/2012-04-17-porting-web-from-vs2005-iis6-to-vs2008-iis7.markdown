---
layout: post
title: "Porting Web from VS2005 IIS6 to VS2008 IIS7"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 31
tags: [Personal]
---
 I am porting a VS2005 web site from Visual Studio 2005 IIS6 to Visual
Studio 2008 (Beta 2) IIS7 on Vista and have encountered several issues.

I am doing this in several steps to ease the migration headaches.

1.  Move the web application project web site from IIS6 (Windows Server
    2003) to IIS7 (Vista Business).
2.  Bring up the web solution in VS2008 to do the conversion.
3.  Change each project in the solution to use Framework 3.0 (and verify
    functionality)
4.  Change each project in the solution to use Framework 3.5 (and verify
    functionality)
5.  Verify that debugging works

Some issues were identified in the various steps as expected.

**Issue \#1 - Web Config HttpHandler**

Use \<Handler\> instead of \<HttpHandler\>

**Issue \#2 - "Request is not available" in this context Trap**

I am getting this error in several places in my code. These are class
library methods that sometimes run with no Request object, perhaps from
a win form instead of a web app. They all test for the existence of the
Request by looking at HttpContext.Current and if null, skips the code
that uses HttpContext.Current.Request. It seems like in IIS7, this test
is no longer sufficient. It appears that HttpContext.Current may be
non-null but HttpContext.Current.Request references cause the above
trap.

For example, this traps in IIS7 and works fine in IIS6:

       if (HttpContext.Current != null)  // No HttpContext if entered
via RemovedCallback()

       {

              string host =
HttpContext.Current.Request.Url.Host.ToLower();

              if (host == "www.mydomain.com") return;

       }

     

To get this to work, I changed the IF to a TRY/CATCH. Is there a more
elegant way? I generally try to avoid TRY/CATCH.

     

       try

       {

              string host =
HttpContext.Current.Request.Url.Host.ToLower();

              if (host == "www.mydomain.com") return;

       }

       catch{}

 

Follow Up: This seems to work - check the Handler property for null:
       if (HttpContext.Current != null &&  // No HttpContext if entered
via RemovedCallback()

           HttpContext.Current.Handler != null)

       {      

              string host =
HttpContext.Current.Request.Url.Host.ToLower();

              if (host == "www.mydomain.com") return;

       }

 

**Issue \#3 - Asynchronous Calls to Web Service(s)**

The model changed from Framework 1.1 to 2.0. The auto-generated proxy to
call a web service no longer had two methods I was using called
begin\<websvcname\> and end\<websvcname\>.

The web service was used to clear the cache in each of the web farm
servers. I wanted to call each without waiting for a response to overlap
the request. When the responses finally came in, if there was an error,
it was logged.

There were too many issues in converting to the newer event-based model
(static method needed to be instance method, no way to have "Async=True"
on the @Page, unsure if the overlapped requests were supported, etc). So
the solution was to simply copy the old generated code for the begin and
end into the newly generated proxy.

       /// \<remarks/\>

       public System.IAsyncResult BeginCachePurge(CachePurgeType
cachePurgeType,

               string parameter, System.AsyncCallback callback, object
asyncState)

       {

              return this.BeginInvoke("CachePurge", new object[] {

                       cachePurgeType,

                       parameter}, callback, asyncState);

       }

 

       /// \<remarks/\>

       public bool EndCachePurge(System.IAsyncResult asyncResult)

       {

              object[] results = this.EndInvoke(asyncResult);

              return ((bool)(results[0]));

       }


 [This post is in progress - Gary] 



