---



copyright:
  years: 2015，2018
lastupdated: "2018-3-26"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}


If you are building a Node.js application, you can use {{site.data.keyword.Bluemix}} Live Sync to quickly update the application instance on {{site.data.keyword.Bluemix_notm}} and develop without manually redeploying.   
{: shortdesc}

When you make a change, you can see that change in your running {{site.data.keyword.Bluemix_notm}} application immediately. {{site.data.keyword.Bluemix_notm}} Live Sync works
<!--from both the command line and -->
in the Eclipse Orion Web IDE (Web IDE). You can debug applications that are written in Node.js by using {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync consists of two features.
<!--three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

You can edit a Node.js application that runs on {{site.data.keyword.Bluemix_notm}} and test it in your browser right away. Any changes that you make in the Web IDE are propagated to the application’s file system immediately.  

**Debug**  

While a Node.js application is in Live Edit mode, you can shell into it and debug it. You can edit code dynamically, insert breakpoints, step through code, restart the runtime, and more by using the Node Inspector debugger.  


##Live Edit
{: #live-edit}

If you are building a Node.js application that runs on {{site.data.keyword.Bluemix_notm}}, the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync can quickly update the application instance. Live Edit is available in the Web IDE only. Live Edit allows you to develop as you would on the desktop without redeploying.

Live Edit is supported for Node.js applications only.

In the Eclipse Orion Web IDE (Web IDE), in the run bar, click **Live Edit**.

![Image of Run bar with live edit](images/bluemix-live-sync-light.png)

Live Edit allows you to quickly preview changes to Node.js applications that run on {{site.data.keyword.Bluemix_notm}}. When you update your code with Live Edit turned on, you can refresh your web application's browser window to see those changes reflected seconds after you make them.

For a tutorial about using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see [Use {{site.data.keyword.Bluemix_notm}} Live Sync to develop, debug, and deploy your app ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/garage/tutorials/use-live-sync-to-develop-debug-and-deploy-your-app){:new_window}.

When you change the files in your Web IDE, they are automatically redeployed to your application instance on {{site.data.keyword.Bluemix_notm}}. If you need to restart the Node application, click the **Restart** button in the run bar.

**Note:** For a more consistent experience when you use the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, 256 MB of additional memory is required and is added.

## {{site.data.keyword.Bluemix_notm}} Live Debug
{: #live-debug}

{{site.data.keyword.Bluemix_notm}} Live Sync Debug uses
[Node Inspector ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/node-inspector/node-inspector){:new_window}
to provide debug features. You need to use version 4 of Node for the debugger to be available since later versions of Node.js do not include Node Inspector.

You can access {{site.data.keyword.Bluemix_notm}} Live Debug when {{site.data.keyword.Bluemix_notm}} Live Edit is enabled for your Node.js app.  

With debug, you can dynamically edit code, insert breakpoints, step through code, restart the runtime and more, all while your app is being served by {{site.data.keyword.Bluemix_notm}}. You can incrementally develop your app with agility while choosing from the large list of {{site.data.keyword.Bluemix_notm}} services.

{{site.data.keyword.Bluemix_notm}} Live Debug includes the following features:

* Application runtime control
* Debug by using [Node Inspector ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/node-inspector/node-inspector){:new_window}
* Shell access

### Application runtime control {: #app-runtime}

With the application runtime control, you can use Debug to inspect the app's state at start time. This capability is useful when you are troubleshooting an app that crashes on start.

While you are developing your app, you can select from the following actions:

* Perform a quick restart of the app
* Suspend the app before any app code runs

After you log in, the {{site.data.keyword.Bluemix_notm}} Live Debug page opens.

![Debug UI](images/live_sync_debug.png)


### Debug {: #debug}

**Restriction:** Google Chrome and Node 4 are required.

Debug includes the following capabilities:  
* Set breakpoints in the app code to pause execution at a specific line.
  **Note:** Breakpoints are not supported in the main program, but are supported in entry points.
* Edit breakpoint conditions to pause execution only when certain criteria are met.
* Inspect the state of local variables and fields.
* View debug output from `console.log()` calls immediately. This action is faster than monitoring cf logs.
* Use the built-in source code editor to make immediate, yet temporary, changes to the running app code.

### Shell {: #shell}

This tool gives you shell access to the container in which your app is running. By using this terminal, you can remotely run diagnostic shell commands to administer your app. All versions of Node.js support the Shell feature.

Monitor memory and CPU usage within the instance that uses standard Linux commands, such as **top**, **ps**, and **kill**.

### Configuring an app to enable {{site.data.keyword.Bluemix_notm}} Live Debug {: #configure_app_debug}

1. The {{site.data.keyword.Bluemix_notm}} Live Debugger uses Node Inspector. You need to use Node version 4. You also need to allow the buildpack to detect the app start command. The start command must be auto-detected by the buildpack, not set in the manifest.yml file.

   A `package.json` file that supports {{site.data.keyword.Bluemix_notm}} Live Debug is:

  ```
  {
      "scripts": {
         "start": "node app.js"
      },
      "engines": {
         "node": "4"
      }
  }
  ```

2. Increase the memory.  

    a. In the app `manifest.yml` file, add 128 MB or more to the value that is specified for the memory attribute.

After the {{site.data.keyword.Bluemix_notm}} Live Debug is installed, you can use the debug tools.

Push the app and then browse to `https://_app-host.mybluemix.net_/bluemix-debug/manage` to access the {{site.data.keyword.Bluemix_notm}} debug user interface. When you are prompted to authenticate, enter your IBM id username and password or a one-time passcode.    

**Note:** The Debugger might take a minute or so to initialize.

### Restoring app configurations and disabling {{site.data.keyword.Bluemix_notm}} Live Debug {: #restore_live_debug}

1. Restore the app's original Node.js version, start command, and memory value.

2. Push the app.

### For more information

* See [Eclipse tools for {{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
