// Don't place your source in a package
import javax.swing.*;
import java.lang.reflect.Array;
import java.text.DecimalFormat;
import java.util.*;
import java.lang.*;
import java.io.*;
import java.math.*;
import java.util.stream.Stream;


// Please name your class Main
public class Main {
    static FastScanner fs=new FastScanner();
    static class FastScanner {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer("");
        public String next() {
            while (!st.hasMoreElements())
                try {
                    st=new StringTokenizer(br.readLine());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            return st.nextToken();
        }
        int Int() {
            return Integer.parseInt(next());
        }

        long Long() {
            return Long.parseLong(next());
        }

        String Str(){
            return next();
        }
    }


    public static void main (String[] args) throws java.lang.Exception {
        PrintWriter out = new PrintWriter(new BufferedWriter(new OutputStreamWriter(System.out)));

        int T=Int();
        for(int t=0;t<T;t++){
            int n=Int();
            long l=Long();
            long r=Long();

            Solution sol=new Solution(out);
            sol.solution(n,l,r);
        }
        out.close();

    }


    public static int Int(){
        return fs.Int();
    }
    public static long Long(){
        return fs.Long();
    }
    public static String Str(){
        return fs.Str();
    }

}






class Solution{
    PrintWriter out;
    public Solution(PrintWriter out){
        this.out=out;
    }





    public void solution(int n,long l,long r){
        long cur=2*(n-1);
        long sum=(2+cur)*(n-1)/2;
        if(l>sum){
            out.println(1);
            return;
        }


        //20 18 16 14 12 10 8 ...
        sum=0;
        int first=1;
        while(sum+cur<l){
            sum+=cur;
            cur-=2;
            first++;
        }



        for(long i=l;i<=r;i++){
            if(i%2==1){
                out.print(first+" ");
            }
            else{
                long dis=i-sum;
                out.print((first+dis/2)+" ");
            }
            if(i==sum+cur){
                sum+=cur;
                cur-=2;
                first++;
                if(first==n)first=1;
            }
        }
        out.println();
    }




     //1 2 1 3 1 4 2 3 2 4 3 4 1
    //1 2 1 3 1 4 1 5 2 3 2 4 2 5 3 4 3 5 4 5 1
    //1 2 1 3 1 4 1 5 1 6 2 3 2 4 2 5 2 6 3 4 3 5 3 6 4 5 4 6 5 6 1
    // 1 2 1 3 2 3 1


}







/*
                             ;\
                            |' \
         _                  ; : ;
        / `-.              /: : |
       |  ,-.`-.          ,': : |
       \  :  `. `.       ,'-. : |
        \ ;    ;  `-.__,'    `-.|
         \ ;   ;  :::  ,::'`:.  `.
          \ `-. :  `    :.    `.  \
           \   \    ,   ;   ,:    (\
            \   :., :.    ,'o)): ` `-.
           ,/,' ;' ,::"'`.`---'   `.  `-._
         ,/  :  ; '"      `;'          ,--`.
        ;/   :; ;             ,:'     (   ,:)
          ,.,:.    ; ,:.,  ,-._ `.     \""'/
          '::'     `:'`  ,'(  \`._____.-'"'
             ;,   ;  `.  `. `._`-.  \\
             ;:.  ;:       `-._`-.\  \`.
              '`:. :        |' `. `\  ) \
      -hrr-      ` ;:       |    `--\__,'
                   '`      ,'
                        ,-'


                      free bug dog
*/


