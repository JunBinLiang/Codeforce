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

        int T=1;
        for(int t=0;t<T;t++){
            int n=Int(),m=Int();

            Solution sol=new Solution(out);
            sol.solution(n,m);
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



    public void solution(int n,int mod){
        long res=0;
        long ncr[][]=new long[501][501];
        long pow[]=new long[501];
        pow[0]=1;
        for(int i=1;i<pow.length;i++){
            pow[i]=(pow[i-1]*2)%mod;
        }

        ncr[0][0]=1;
        for (int i=1;i<ncr.length;i++) {
            ncr[i][0]=1;
            for (int j=1;j<ncr[0].length;j++) {
                ncr[i][j]=(ncr[i-1][j]+ncr[i-1][j-1])%mod;
            }
        }


        long dp[][]=new long[n+1][n+1];


        for(int i=1;i<dp.length;i++){
            dp[i][i]=pow[i-1];
            for(int j=1;j<i;j++){
                for(int k=1;k<i;k++){
                    //pow[cnt-1]
                    if(i-k-1>=1&&j>=k){
                        dp[i][j]=dp[i][j]+dp[i-k-1][j-k]*((ncr[j][k]*pow[k-1])%mod);
                        dp[i][j]%=mod;
                    }
                }

            }
        }




        for(int i=1;i<=n;i++){
            res+=dp[n][i];
            res%=mod;
        }
        out.println(res);
    }



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


