// Don't place your source in a package
import java.util.*;
import java.lang.*;
import java.io.*;
import java.math.*;






// Please name your class Main
public class Main {
    static Scanner in = new Scanner(System.in);
    public static void main (String[] args) throws java.lang.Exception {
        PrintWriter out = new PrintWriter(System.out);

        int T=1;
        for(int t=0;t<T;t++){
            int n=Int();
            int A[][]=new int[n][2];


            for(int i=0;i<n;i++){
                A[i][0]=Int();
                A[i][1]=Int();
            }

            Solution sol=new Solution();
            sol.solution(out,A);

        }
        out.flush();

    }

    public static long Long(){
        return in.nextLong();
    }
    public static int Int(){
        return in.nextInt();
    }
    public static String Str(){
        return in.next();
    }
}


class Solution{
    int dp[];
    TreeMap<Integer,Integer>tree=new TreeMap<>();
    public void solution(PrintWriter out,int A[][]){
        int res=Integer.MIN_VALUE;
        int n=A.length;
        Arrays.sort(A,(a,b)->{
            return a[0]-b[0];
        });
        dp=new int[n];
        Arrays.fill(dp,-1);

        for(int i=0;i<A.length;i++){
            tree.put(A[i][0],i);
        }


        for(int i=0;i<A.length;i++){
            res=Math.max(res,1+dfs(A,i));
        }
        System.out.println((n+1)-res);
    }

    public int dfs(int A[][],int i){
        if(dp[i]!=-1){
            return dp[i];
        }

        int pos=A[i][0];
        int pow=A[i][1];



        Integer floor=tree.floorKey(pos-pow-1);
        int res=1;
        if(floor==null){

        }
        else{
            res+=dfs(A,tree.get(floor));
        }
        dp[i]=res;
        return res;
    }

}

