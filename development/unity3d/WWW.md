[== Mono Compatibility ==]
http://docs.unity3d.com/Documentation/ScriptReference/MonoCompatibility.html

mono 2.0
Class: HttpWebRequestElement (namespace System.Net.Configuration, assembly System)
HttpWebRequestElement ()
HttpWebRequestElement HttpWebRequest { get; } 
 
Response���� Web player ���� ��������.

 
[== WWW Ŭ���� - Unity3d ==]
http://docs.unity3d.com/Documentation/ScriptReference/WWW.html
 Note: http://, https:// and file:// protocols are supported on iPhone. ftp:// protocol support is limited to anonymous downloads only. Other protocols are not supported. 
 
standard alone��
���� : 
http   : ����
https  : ����
cookie : http://plyoung.wordpress.com/2011/08/05/unity-3d-and-session-cookies/

webplayer��
http://docs.unity3d.com/Documentation/Manual/SecuritySandbox.html

[== HttpWebRequest Ŭ���� - msdn ==]
http://msdn.microsoft.com/ko-kr/library/system.net.httpwebrequest%28v=vs.80%29.aspx
http   : ����
https  : ���� (standardalone������ ���� ������ �ʿ��� - Security����)
cookie :
 httpWebRequest.CookieContainer = new CookieContainer();
 httpWebResponse.Cookies


[==  WebRequest.Create ("https://www.anywhere.com"); throws an exception ==] 

http://www.mono-project.com/FAQ:_Security

There are three alternatives to solve this problem:

    Implement a ICertificatePolicy class. By doing this you can override the normal results of the certificate validation (e.g. accepting an untrusted certificate). However you are now responsible of applying your own trust rules for your application. Further suggestions and source code are available in the UsingTrustedRootsRespectfully article. 
    Use the certmgr.exe tool (included in Mono) to add the root certificates into the Mono Trust store. Every SSL certificate signed from this root will then be accepted (i.e. no exception will be thrown) for SSL usage (for all Mono applications running for the user or the computer - depending on the certificate store where the certificate was installed). 
    Use the mozroots.exe tool (included in Mono 1.1.10 and later) to download and install all Mozilla's root certificates (i.e. the ones used in FireFox and other Mozilla's softwares). It's easier than finding a specific root but it's also less granular to make a decision about which one(s) you install or not. 
    
[== UsingTrustedRootsRespectfully ==]

http://www.mono-project.com/UsingTrustedRootsRespectfully

 Approach #-1: Actively ignore security concerns

using System.Net.Security;

using System.Security.Cryptography.X509Certificates;


[== Unityweb ==]

http://code.google.com/p/unityweb/
The WWW class in Unity3D is deficient in many ways.
Unity3D WebPlayer and iOS builds cannot use System.Net.WebRequest due to security concerns.
The solution? Write a HTTP class from scratch, based on plain old sockets. 



 HttpWebRequest �� �̿��Ͽ� Post�� �α��� �ϱ�
http://aja99.tistory.com/archive/20090119