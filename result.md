# 力扣刷题题解

------

## 001

### 题目

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

 

示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
示例 2：

输入：nums = [3,2,4], target = 6
输出：[1,2]
示例 3：

输入：nums = [3,3], target = 6
输出：[0,1]


提示：

2 <= nums.length <= 103
-109 <= nums[i] <= 109
-109 <= target <= 109
只会存在一个有效答案

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解

这是一道很简单的题,我们可以直接使用map来解出这道题,用target值减去数组中的数得到一个新的数,并且加以判断,如果这个数不在map里面就把此时数组中的数存进map,key值为nums[i],value为i。如果这个结果已经在map中，那就说明找到了一对相加等于target的数，直接输出map中对应key值的value和i。

思路如下:

1.创建一个map

2.for循环遍历nums数组

3.用target值减去nums[i]

  得到result并对result加以判断:

​    如果map中存在result: 则直接输出[map.get(result),i]

​    如果map中不存在result:则将nums[i]和i 存于map中.

代码如下：

```js
var twoSum = function(nums, target) {
    const map = new Map();
    for (var i = 0; i < nums.length; i++){
        const result = target - nums[i];
        if(map.has(result)){
            return [map.get(result),i];
        }else{
            map.set(nums[i],i);
        }
    }
    return [];
};
```

```js
import java.io.*;
import java.net.URL;
import java.net.URLConnection;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class second {
    static List<String> pictureURL = new ArrayList<String>();
    static List<String> titleGlobal = new ArrayList<String>();
    static List<String> contentGlobal = new ArrayList<String>();
    //store with one url with quote and one class
    static List<String> urlAndClass = new ArrayList<String>();

    static String SendGet(String url, String encode) {
        String result = "";
        BufferedReader in = null;
        try {
            URL realUrl = new URL(url);
            URLConnection connection = realUrl.openConnection();
            connection.connect();
            in = new BufferedReader(new InputStreamReader(
                    connection.getInputStream(), encode));
            String line;
            while ((line = in.readLine()) != null) {
                result += line + '\n';
            }
        } catch (Exception exc) {
            System.out.println("发送GET请求出现异常！" + exc);
            exc.printStackTrace();
        }
        // 使用finally来关闭输入流
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

    //得到不同类别的页面
    static void getClass(String str) {
        String regex = "<ul class=\"clearfix\">[\\s\\S]*?</ul>";
        String div = "";
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(str);
        if (matcher.find()) {
            div += matcher.group().replaceAll("(<ul class=\"clearfix\">[\\s\\S]*?百家|个性推荐[\\s\\S]*?</ul>)", "");
        }
        System.out.println(div);
        regex = "(<a href.*?</a>)";
        pattern = Pattern.compile(regex);
        matcher = pattern.matcher(div);
        while (matcher.find()) {
            urlAndClass.add(matcher.group().replaceAll("(</a|>|<a href=)", ""));
        }
    }

    //得到某个url的编码方式
    static String getEncode(String url) {
        String result = "";
        String encode = "utf-8";
        BufferedReader in = null;
        try {
            URL realUrl = new URL(url);
            URLConnection connection = realUrl.openConnection();
            connection.connect();
            in = new BufferedReader(new InputStreamReader(
                    connection.getInputStream(), "utf-8"));
            String line;
            int i = 0;
            while ((line = in.readLine()) != null) {
                result += line + '\n';
                i++;
                if (i == 20)
                    break;
            }
            //System.out.println(result);
            String reg = "charset=.*?\"";
            Pattern pat = Pattern.compile(reg);
            Matcher mat = pat.matcher(result);
            while (mat.find()) {
                encode = mat.group().replaceAll("(charset=|\")", "");
            }
        } catch (Exception exc) {
            System.out.println("发送GET请求出现异常！" + exc);
            exc.printStackTrace();
        }
        // 使用finally来关闭输入流
        finally {
            try {
                if (in != null) {
                    in.close();
                }
            } catch (Exception e2) {
                e2.printStackTrace();
            }
        }
        return encode;
    }

    //爬一遍urlAndClass变量内的所有网址，并且创建相应的文件
    static void searchClass() throws IOException {
        String path = "http://news.baidu.com";
        String rootPath = "H:\\try\\";
        //存储需要创建的文件夹路径
        String dirPath = "";
        //此变量存储绝对路径或者相对路径
        String newspath = "";
        //中文的正则表达式
        String reg = "[\u4e00-\u9fa5]";
        Pattern pat = Pattern.compile(reg);
        //获取中文内容
        String className = null;
        int i = 0;
        while (i < urlAndClass.size()) {
            className = "";
            newspath = urlAndClass.get(i);
            Matcher mat = pat.matcher(newspath);
            while (mat.find()) {
                className += mat.group();
            }
            newspath = mat.replaceAll("");
            newspath = newspath.replaceAll("\"", "");
            if (newspath.indexOf("http") == -1) {
                newspath = path + newspath;
            }
            dirPath = rootPath + className + ".txt";
            System.out.println(newspath + "--" + className);
            File txt = new File(dirPath);
            if (!txt.exists()) {
                txt.createNewFile();
            }
            getContent2(newspath, dirPath);
            if (i == urlAndClass.size())
                break;
            i++;
        }
        //System.out.println(urlAndClass.get(1));
    }

    //得到regex里面的内容
    static String getReg(String input, String regex, String seperator) {
        String result = "";
        Pattern pat = Pattern.compile(regex);
        Matcher mat = pat.matcher(input);
        while (mat.find()) {
            result += mat.group() + seperator;
        }
        return result;
    }

    static String removeATag(String str) {
        str = getReg(str, "(href=\".*?\"|>[\\s\\S]*?<)", "\r\n");
        str = str.replaceAll("(href=|</a>|<|>)", "");
        return str;
    }

    //得到某类新闻url和存储的文件信息，把href链接和标题，存入对应txt中
    static void getContent2(String newspath, String path) throws IOException {
        String result = SendGet(newspath, getEncode(newspath));
        FileWriter fw = new FileWriter(path);
        String reg = "id=\"body\"[\\s\\S]*?id=\"goTop\"";
        result = getReg(result, reg, "");
        reg = "<a href=\"http[\\s\\S]*?</a>";
        result = getReg(result, reg, "");
        fw.write(removeATag(result));
        fw.close();
    }

    //updateDB中要用
    static boolean existChinese(String str) {
        String reg = "[\u4e00-\u9fa5]";
        Pattern pat = Pattern.compile(reg);
        Matcher mat = pat.matcher(str);
        while (mat.find()) {
            return true;
        }
        return false;
    }

    //插入数据库
    public static void updateDB() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/try";
        String username = "root";
        String pwd = "admin123";
        Connection conn = null;
        ResultSet res = null;
        Statement stm = null;
        PreparedStatement pst = null;
        String sql;
        String path = "H:\\try\\";
        File dir = new File(path);
        File[] files = dir.listFiles();
        int id = 2;
        try {
            //Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection(url, username, pwd);
            stm = conn.createStatement();
            System.out.println("Connect success!");
        } catch (Exception e) {
            e.printStackTrace();
        }
        assert files != null;
        for (File file : files) {
            //得到所有txt文件的内容
            String url2 = "";
            String title = "";
            String newsClass = "";
            int u = 0, t = 0;
            int count = 0;
            try {
                newsClass = getReg(file.getAbsolutePath(), "[\\u4e00-\\u9fa5]*?.txt", "");
                newsClass = newsClass.replaceAll(".txt", "");
                FileReader fr = new FileReader(file.getAbsolutePath());
                BufferedReader br = new BufferedReader(fr);//构造一个BufferedReader类来读取文件
                String s = null;
                while ((s = br.readLine()) != null && s != "\r\n") {//使用readLine方法，一次读一行
                    if (s.indexOf("\"") != -1) {
                        url2 = s.replaceAll("\"", "");
                        u = 1;
                    }
                    if (existChinese(s) && u == 1) {
                        title = s;
                        t = 1;
                    }
                    if (t == 1) {
                        //System.out.println("url2" + "--" + "title");
                        t = 0;
                        u = 0;
                        //每个类别插入五条信息
                        if (count >= 6) {
                            continue;
                        }
                        count++;
                        try {
                            //删除旧数据库
                            //sql = "delete from news where id > 1;";
//stm.executeUpdate(sql);
                            //插入新的行
                            sql = "insert ignore into table1(NewsType,NewsTitle,NewsTime)" +
                                    " values(?,?,NOW());";
                            assert conn != null;
                            pst = conn.prepareStatement(sql);
                            /*
                            pst.setInt(1, id);
                            pst.setString(2, title);
                            pst.setString(3, "yyj");
                            pst.setDate(4, new Date(2017 - 1900, 5 - 1, 14));
                            pst.setString(5, url2);
                            pst.setString(6, "");//picture
                            pst.setBoolean(7, false);//star
                            pst.setString(8, newsClass);//class
                            */
                            pst.setString(1, newsClass);//class
                            pst.setString(2, title);

                            pst.executeUpdate();
                            id++;
                            //选择所有的行输出
                            sql = "select * from table1 where NewsID >?;";
                            pst = conn.prepareStatement(sql);
                            pst.setString(1, "1");
                            res = pst.executeQuery();
                            while (res.next()) {
                                System.out.println(res.getString("NewsID") + "\t" + res.getString("NewsTitle") + "\t" + res.getString("NewsType"));
                            }
                        } catch (SQLException e) {
                            System.out.println("sql error!");
                            e.printStackTrace();
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                }
                br.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        conn.close();
    }

    public static void main(String[] args) throws IOException, SQLException {
        // 定义即将访问的链接
        String url = new String("http://news.baidu.com/");
        //从URL下载文件的类
        //getPic getPic = new getPic();
        //得到结果的字符串
        String result = SendGet(url, getEncode(url));
        //新闻类别,赋值到全局变量urlAndClass内
        getClass(result);
        //把urlAndClass变量内的所有url都爬一遍
        searchClass();
        System.out.println(urlAndClass.toString());
        try {
            updateDB();
        } catch (SQLException e) {
            System.out.println("sql error!");
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}

```

