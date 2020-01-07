## KMP 算法

```java
import java.util.ArrayList;
import java.util.List;

public class KMP {

    public static void main(String[] args){
        String str = "absbshdiffhsjhdgsabbaddabcbabdssedue";
        String parse = "abcbab";
        List<Integer> next = getNext(parse);


        int strlen = str.length();
        int parseLen = parse.length();

        int k=-1;//字符串匹配的位置，大于-1表示存在匹配的字符串

        int i=0;

        for (i=0;i<strlen;i++){
            while (k>-1 && parse.charAt(k+1) != str.charAt(i)){//如果有匹配的字符串，则从匹配的字符串里面先去查询一遍是否存在匹配，如果没有则
                k=next.get(k);
            }

            if (parse.charAt(k+1) == str.charAt(i)){//如果匹配，则让K表示匹配的位置
                k= k+1;
            }

            if (k==parseLen-1){//如果长度为匹配字符串的长度，则表示已匹配完成，退出
                break;
            }

        }

         System.out.println(str.charAt(i));
         System.out.println(i);

    }



    public static List<Integer> getNext(String parse){
        List<Integer> next = new ArrayList<Integer>();
        int strLen = parse.length();
        int k = -1;//k为循环到该字符串的最长前缀的位置
        next.add(0,k);//第一个默认为-1，只有一个字符串，所以没有最长前缀一说

        for (int i=1;i<strLen;i++){ //循环遍历每一个字符串 a,ab,abc,abca,abcba
            while (k>-1 && parse.charAt(k+1)!=parse.charAt(i)){//如果没有匹配成功，则k就必须回溯，如果回溯到最近一次的k=-1的位置，则跳出
                k = next.get(i);
            }

            if (parse.charAt(k+1) == parse.charAt(i)){//如果K+1（即上一步找到的最长前缀的位置+1）和上一步字符串+1的字符串匹配成功
                k = k+1;
            }

            next.add(i,k);
        }


        return next;
    }
}

```

