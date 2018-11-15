<!-- default file list -->
*Files to look at*:

* [ChangeDatabaseAtRuntimeViewController.cs](./CS/WinWebSolution.Module/ChangeDatabaseAtRuntimeViewController.cs) (VB: [ChangeDatabaseAtRuntimeViewController.vb](./VB/WinWebSolution.Module/ChangeDatabaseAtRuntimeViewController.vb))
* [ChangeDatabaseAtRuntimeViewController.Designer.cs](./CS/WinWebSolution.Module/ChangeDatabaseAtRuntimeViewController.Designer.cs) (VB: [ChangeDatabaseAtRuntimeViewController.Designer.vb](./VB/WinWebSolution.Module/ChangeDatabaseAtRuntimeViewController.Designer.vb))
* [ISupportChangeDatabaseAtRuntime.cs](./CS/WinWebSolution.Module/ISupportChangeDatabaseAtRuntime.cs) (VB: [ISupportChangeDatabaseAtRuntime.vb](./VB/WinWebSolution.Module/ISupportChangeDatabaseAtRuntime.vb))
* [WebApplicationE1344.cs](./CS/WinWebSolution.Web/ApplicationCode/WebApplicationE1344.cs) (VB: [WebApplicationE1344.vb](./VB/WinWebSolution.Web/ApplicationCode/WebApplicationE1344.vb))
* [WinApplicationE1344.cs](./CS/WinWebSolution.Win/WinApplicationE1344.cs) (VB: [WinApplicationE1344.vb](./VB/WinWebSolution.Win/WinApplicationE1344.vb))
<!-- default file list end -->
# How to change connection to the database at runtime


<p><strong>Scenario</strong></p>
<p>This example illustrates how to connect your application to another database after the application is already started. This can be required for a multi-tenant application where you need to associate a user or company with their own database of the same structure. You can choose a required database and user during the login procedure and also later in the application UI by using the specialized SingleChoiceAction (available for Admin only). The created databases will have the same structure, but can have a different predefined data set.</p>
<p><img src="https://raw.githubusercontent.com/DevExpress-Examples/how-to-change-connection-to-the-database-at-runtime-e1344/9.1.2+/media/ffd2a3d2-ae0a-11e5-80bf-00155d62480c.png"><br><br><strong>Steps to implement<br></strong></p>
<p>1. Using the XAF Solution Wizard, create a new XAF app named RuntimeDbChooser and that uses XPO for data access and the Security module with the Authentication = Standard and UI-level mode options.<br>2. Copy code that creates predefined security users for each database from the <em>RuntimeDbChooser.Module\DatabaseUpdate\Updater.xx</em> file into <em>YourSolutionName.Module/DatabaseUpdate/Updater.xx;</em><br>3. Copy and include the <em>RuntimeDbChooser.Module\BusinessObjects\CustomLogonParameters.xx</em> file into the <em>YourSolutionName.Module/BusinessObjects</em> folder; <strong>*</strong><br>4. Copy and include the <em>RuntimeDbChooser.Module.Web\WebChangeDatabaseController.xx</em> and <em>RuntimeDbChooser.Module.Web\WebCustomAuthentication.xx</em> files into the <em>YourSolutionName.Module.Web</em> project;<br>5. Copy and include the <em>RuntimeDbChooser.Module.Win\WinChangeDatabaseController.xx</em> and <em>RuntimeDbChooser.Module.Win\WinCustomAuthentication.xx</em> files into the <em>YourSolutionName.Module.Win</em> project;<br>6. Copy and include the <em>RuntimeDbChooser.Wxx\WxxApplicationEx.xx</em> files into the <em>YourSolutionName.Wxx</em> project;<br>7. Replace the line that instantiates your WinApplication descendant in the YourSolutionName.Win/Program.xx file with the CreateApplication method call as shown in the <em>RuntimeDbChooser.Win/Program.xx file.<br></em>8. In the Application Designer invoked for the YourSolutionName.Web/WebApplication.xx file, select the Authentication Standard component and set its LogonParametersType property to RuntimeDbChooser.Module.BusinessObjects.CustomLogonParametersForStandardAuthentication</p>
<p>You can learn more on the approaches used in points 2-4 from the <a href="https://documentation.devexpress.com/eXpressAppFramework/CustomDocument112670.aspx">eXpressApp Framework</a> > <a href="https://documentation.devexpress.com/eXpressAppFramework/CustomDocument112682.aspx">Task-Based Help</a> > <a href="https://documentation.devexpress.com/eXpressAppFramework/CustomDocument112982.aspx">How to: Use Custom Logon Parameters and Authentication</a> article.<br><strong>____<br>*</strong> In this example, the available database names are hard-coded in the MSSqlServerChangeDatabaseHelper class and supplied to the DatabaseName  property editor using the <a href="https://documentation.devexpress.com/#eXpressAppFramework/DevExpressExpressAppModelIModelCommonMemberViewItem_PredefinedValuestopic">PredefinedValues</a> model option. To populate the PredefinedValues list with names that will be known only at runtime, use the approach described in these articles (Win and Web specific):<br><a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113101">How to: Supply Predefined Values for the String Property Editor Dynamically (WinForms)</a><br><a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113116">How to: Supply Predefined Values for the String Property Editor Dynamically (ASP.NET)</a><br><br></p>
<p>A custom editor described in these articles can be assigned to the DatabaseName property using the <a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument112582">Model Editor</a>.</p>


<h3>Description</h3>

<p>This version of the example is intended for a simple scenario, in which XAF&#39;s Security System is NOT used. The work in a scenario in which XAF&#39;s Security System is used is not guaranteed, because when changing the database the Security System should be also re-configured, but it doesn&#39;t support such scenarios out-of-the-box. However, this problem can be bypassed if there will be a separate database for security classes that won&#39;t be changed. This scenario will be demonstrated in the latest versions of the example.</p>

<br/>


