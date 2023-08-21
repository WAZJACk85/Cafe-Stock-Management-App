
<h1>Cafe Stock Management APP - Explanation [Line21] and Screenshots (also video rec at my website) (https://portfolio.buyshirtsandstuff.com/)</h1>

## I have coded a stock and place order application run on C#, winforms, xml and SQL for a hypothetical cafe.

In the Application you can: 
* Place orders and print bills for customers;
* Add new stock items via the admin login; 
* Add to the inventory (via SQL database);
* Also, you can Delete items and Update the details of the stock items via the application GUI which will send the commands to the SQL Database;

Please see the majority of the code housed in my repository folders, this is currently designed to work on my laptop and connect to my internal Relational MSSQL databases, however in the near future I will create a sister project, whereby the project runs from an external SQL source, to make the app more flexible and show knowledge of network data manipulation.

* Also in the future I will upgrade this application's looks(GUI) and the way the features are used, so the Hypothetical user may gain a better user experience.  Finally I will do A video live capture of using the application and post this onto my website (subdomain address) so that if anyone/ employers are interested in the knowledege and design they can see the app working and and an overview of each section and brief exposure to the code alongside the application video.

Current Video: https://portfolio.buyshirtsandstuff.com/

## Explanation of the Basic functions and main code structure with Screenshots


### START POINT  ###

**using**  :    

**using** is the library action to use and draw functions and mini frameworks (i.e complex linked functions)
In this app we are **using**  mainly  from System and  System.windows.forms  ; enabling drawing of graphics and form defined parameters and objects. System allows extra functions (elaborate in full build document) one of which is SQL commands and external parses and net commands.

**namespace** :  **namespace** is like a sub program name, used as a reference to export or import other files or functions.  It is also a space to keep 'names'. Names of functions, variables and all other sorts of code objects separate from other 'names' within the whole of the application scope.

In this case the main namespace is called       **Cafe_Menu4**    and within this namespace (think of it as a folder of linked files with linked functions)  it holds all of the functions and events in the first page of the application and interacts with the login input. It also holds the entry point to add other subprograms and libraries and the defined functions (glossary) for executing SQL commands to the Database.

It loads the buttons which link to other sections and sub-programs (built in csharp) and presents the first page of the Dashboard.

Files linked via namespace   Cafe_Menu4     :  dashboard.cs    program.cs function.cs  and 
form1.cs

dashboard.cs = opens main dashboard and loads section button links
program.cs = main entry point to run other main programs
function.cs = sets connection to server and db,  defines how to get data,  defines how to set data.

form1.cs= Is like a SQL glossary and defines how the SQL commands and functions work to get and set data.

(SUMMARY : load events, buttons , intializer, welcome screens, load section links/page links/ SQL Glossary)

Sub-namespaces / Sub-programs 

**List:-**

* Cafe_Menu4.AllUserControls

Sub-namespaces  :  are often folders built into the main namespaces they follow the namespace with a full stop  i.e   .AlluserControls

They can be used as there own namespaces, but it is useful to connect them to the main namespace in most cases.

**Partial-classes / Sub-class**

* UC_Additems.cs
* UC_PlaceOrder.cs
* UC_RemoveItem.cs
* UC_UpdateItems.cs
* UC_Welcome.cs

### Description of Partial-classes / Sub-classes ###

These sub classes (public partial class) above,  house within them,  a list of functions that interact when the user clicks action buttons housed in the  ## **.Designer.cs**   graphics program.  Each of the above sub-programs / classes links to a 'graphics file'  or csharp draw file (designer.cs)  this 'draws/paints' the graphics of each form page linked to the corresponding sub-programs above.  

When actions are clicked or values are entered in by the user (names of products to add or numbers)  it will parse these 'user entered values' into the connected database and will fill the boxes for the user to see.

The flow chart is as such:-

User entry =>  Designer.cs file  =>  talks to  UC_Additems.cs => talks to database adds values => reflects to UC_Additems.cs => reflects to Desgine.cs file  ( now the user can see change)





