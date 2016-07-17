#Android 开发 Java解析Json字符串

><font color=#0099ff>@author Gust <br>
>@Date 2016-07-17


###介绍
&emsp;&emsp;Android 开发请求服务器，得到了自己想要的数据，然而却是Json 格式的，并不能直接拿来使用，百度，查阅资料，还有在朋友的帮助下，学会了怎么用Java 处理Json 字符串。如果是Android 开发的话，好像不需要导入jar 包（我的Android Studio 里可以直接用），Java 需要导入一个叫 ``` json.org.jar ``` 包

>代码（ Java 测试时的代码）

```java
	
import org.json.JSONArray;
import org.json.JSONObject;

public class main {
	public static void main(String arg[]) {
		String sJson = "[{'id':'1','name':'hei'},{'id':'2','name':'ha'}]";
		new main().JSONSolve(sJson);
	}
	
	public void JSONSolve(String str) {

        try {
            JSONArray jsonArray = new JSONArray(str);
            for (int i = 0; i < jsonArray.length(); i++) {
                
                JSONObject job = jsonArray.getJSONObject(i);
                
                System.out.println("id = " + job.getInt("id") + "  name = " + job.getString("name"));

            }
        }catch (Exception e) {
            e.printStackTrace();
        }
    }


```

>附


&emsp;&emsp;在此感谢 ```StormMaybin``` 提供的资料及资源 <br>
&emsp;&emsp;[jar包下载](http://download.csdn.net/detail/hashgust/9578559)