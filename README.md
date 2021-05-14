# Dll-Test
Dll-Test


subject：JNA throw Exception
content：

JNA version:jna-5.7.0.jar
JDK: 1.8.0_271 32bit
Windows10 64bit
CPU:i5-7500 3.40GHz
After invoke the native method a few times, it will throw Exception:java.lang.Error: Invalid memory access
Steps to reproduce
dll method : function initParams(url :PAnsiChar; appid : PAnsiChar;appkey : PAnsiChar) : Integer ; stdcall ;
java method : int initParams(String url, String appid, String appkey);

method implementation:
~~~
public interface Agency3intfc extends Library {
    public Agency3intfc ag = (Agency3intfc) Native.load("agency3intfc", Agency3intfc.class);

    int initParams(String url, String appid, String appkey);
    
    Integer callagency3intfc(String inParams , String outParams);
}

~~~

method main test:
~~~
public class Agency3intfcTestT {
	public static void main(String[] args) {
		Agency3intfc a = Agency3intfc.ag;
		String url = "url";
		String appid = "appid";
		String appkey = "appkey";
		int stdcall = a.initParams(url, appid, appkey);
		System.out.println(a);
		System.out.println("init stdcall :" + stdcall);
	}
}
~~~

~~~
Connected to the target VM, address: '127.0.0.1:60308', transport: 'socket'
Exception in thread "main" java.lang.Error: Invalid memory access
	at com.sun.jna.Native.invokeInt(Native Method)
	at com.sun.jna.Function.invoke(Function.java:426)
	at com.sun.jna.Function.invoke(Function.java:361)
	at com.sun.jna.Library$Handler.invoke(Library.java:265)
	at com.sun.proxy.$Proxy0.initParams(Unknown Source)
	at dd.Agency3intfcTest.main(Agency3intfcTest.java:12)
~~~
