# Android开发 HTTP POST 与 Get 请求

><font color=#0099ff >@author Gust <br>
>@Date 2016-7-16 </font>

######介绍
&emsp;&emsp;自己做了个小项目，Android，网页，Node 开发，一个关于美食的，之前只学过基础的网页＋PHP，Android 和 Node 都是从零开始，因为是小组项目，我负责的是Android部分，网页和 Node 的知识，我会在后面补上的。
&emsp;&emsp;今天介绍一下今天学习的HTTP 请求，Android 之前学到的东西，会在之后补上。

>背景

&emsp;&emsp;Android 端要链接 Node 创建的服务端，需要通过发送 HTTP 请求，来提交和获取数据，通过 POST 提交， GET 获取。 <br>
&emsp;&emsp;Android 发送请求，用了Java 的 URLConnection 类。

>main 方法

<tab>
	
	public class main {
		public static void main(String[] args) {
	        //发送 GET 请求
	        String s=UrlHttp.sendGet("http://127.0.0.1:8001/wregister", "key=123&v=456");
	        System.out.println(s);
	        
	        //发送 POST 请求
	        String sr=UrlHttp.sendPost("http://127.0.0.1:8001/wregister", "key=123&v=456");
	        System.out.println(sr);
	    }
	}
</tab>

>UrlHttp 类
<tab>
	
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.PrintWriter;
	import java.net.URL;
	import java.net.URLConnection;
	import java.util.List;
	import java.util.Map;

	public class UrlHttp {
	    /**
	     * 向指定URL发送GET方法的请求
	     * 
	     * @param url
	     *            发送请求的URL
	     * @param param
	     *            请求参数，请求参数应该是 name1=value1&name2=value2 的形式。
	     * @return URL 所代表远程资源的响应结果
	     */
	    public static String sendGet(String url, String param) {
	        String result = "";
	        BufferedReader in = null;
	        try {
	            String urlNameString = url + "?" + param;
	            URL realUrl = new URL(urlNameString);
	            // 打开和URL之间的连接
	            URLConnection connection = realUrl.openConnection();
	            // 设置通用的请求属性
	            connection.setRequestProperty("accept", "*/*");
	            connection.setRequestProperty("connection", "Keep-Alive");
	            connection.setRequestProperty("user-agent",
	                    "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1;SV1)");
	            // 建立实际的连接
	            connection.connect();
	            // 获取所有响应头字段
	            Map<String, List<String>> map = connection.getHeaderFields();
	            // 遍历所有的响应头字段
	            for (String key : map.keySet()) {
	                System.out.println(key + "--->" + map.get(key));
	            }
	            // 定义 BufferedReader输入流来读取URL的响应
	            in = new BufferedReader(new InputStreamReader(
	                    connection.getInputStream()));
	            String line;
	            while ((line = in.readLine()) != null) {
	                result += line;
	            }
	        } catch (Exception e) {
	            System.out.println("发送GET请求出现异常！" + e);
	            e.printStackTrace();
	        }
	        // 使用finally块来关闭输入流
	        finally {
	            try {
	                if (in != null) {
	                    in.close();
	                }
	            } catch (Exception e2) {
	                e2.printStackTrace();
	            }
	        }
	        return result;
	    }
	
	    /**
	     * 向指定 URL 发送POST方法的请求
	     * 
	     * @param url    发送请求的 URL
	     * @param param  请求参数，请求参数应该是 								name1=value1&name2=value2 的形式。
	     * @return 所代表远程资源的响应结果
	     */
	    public static String sendPost(String url, String param) {
	        PrintWriter out = null;
	        BufferedReader in = null;
	        String result = "";
	        try {
	            URL realUrl = new URL(url);
	            // 打开和URL之间的连接
	            URLConnection conn = realUrl.openConnection();
	            // 设置通用的请求属性
	            conn.setRequestProperty("accept", "*/*");
	            conn.setRequestProperty("connection", "Keep-Alive");
	            conn.setRequestProperty("user-agent",
	                    "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1;SV1)");
	            // 发送POST请求必须设置如下两行
	            conn.setDoOutput(true);
	            conn.setDoInput(true);
	            // 获取URLConnection对象对应的输出流
	            out = new PrintWriter(conn.getOutputStream());
	            // 发送请求参数
	            out.print(param);
	            // flush输出流的缓冲
	            out.flush();
	            // 定义BufferedReader输入流来读取URL的响应
	            in = new BufferedReader(
	                    new InputStreamReader(conn.getInputStream()));
	            String line;
	            while ((line = in.readLine()) != null) {
	                result += line;
	            }
	        } catch (Exception e) {
	            System.out.println("发送 POST 请求出现异常！"+e);
	            e.printStackTrace();
	        }
	        //使用finally块来关闭输出流、输入流
	        finally{
	            try{
	                if(out!=null){
	                    out.close();
	                }
	                if(in!=null){
	                    in.close();
	                }
	            }
	            catch(IOException ex){
	                ex.printStackTrace();
	            }
	        }
	        return result;
	    }    
	}
</tab>


>注

&emsp;&emsp;自己今天也查了好多资料，看了很多大神的博客，自己也尝试了很多，最终这个是我尝试成功了的，也是用了很多别人的东西，当时的网页们都已经找不回来了，在这里也没有办法列出来，还请各位大神原谅，后续若还有其他的方法，也会一直更新出来的。