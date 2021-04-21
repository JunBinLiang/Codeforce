// Don't place your source in a package

import java.math.BigInteger;
import java.util.*;
import java.lang.*;
import java.io.*;



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
        PrintWriter out = new PrintWriter(System.out);


        int T=1;
        for(int t=0;t<T;t++){
            long k=Long();
            Solution sol=new Solution(out);
            sol.solution(k);
        }
        out.flush();

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


    long f[]=new long[15];
    public void solution(long k){
        f[0]=9;
        for(int i=1;i<f.length;i++){
            f[i]=10*f[i-1];
        }
        for(int i=1;i<f.length;i++){
            f[i]*=(i+1);
        }

        long l=1,r=1000000000000l;
        long res=-1;
        long count=0;
        while(l<=r){
            long mid=l+(r-l)/2;
            long cnt=get(mid);
            if(cnt>=k){
                res=mid;
                count=cnt;
                r=mid-1;
            }
            else{
                l=mid+1;
            }
        }

        int extra=(int)(count-k);
        String s=res+"";
        out.println(s.charAt(s.length()-1-extra));
    }

    public long get(long n){
        long res=0;
        long base=0;
        int i=0;
        while(true){
            if(n<=base*10+9){
                res=res+(i+1)*(n-base);
                break;
            }
            res+=(f[i]);
            i++;
            base=base*10+9;
        }
        return res;
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





