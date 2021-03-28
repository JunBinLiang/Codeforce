// Don't place your source in a package
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
    static class FastScanner {//scanner from SecondThread
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
            int n=Int();

            int A[][]=new int[n][2];
            for(int i=0;i<n;i++){
                A[i][0]=Int();
                A[i][1]=i;
            }

            int m=Int();
            int q[][]=new int[m][3];

            for(int i=0;i<m;i++){
                q[i][0]=Int();
                q[i][1]=Int()-1;
                q[i][2]=i;
            }

            Solution sol=new Solution();
            sol.solution(out,A,q);
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
    public void solution(PrintWriter out,int A[][],int q[][]){
        int B[]=new int[A.length];
        int res[]=new int[q.length];
        int arr[]=new int[A.length];

        for(int i=0;i<A.length;i++){
            B[i]=A[i][0];
        }

        Fenwick fen=new Fenwick(arr);
        Arrays.sort(A,(a,b)->{
            if(a[0]==b[0])return a[1]-b[1];
            return b[0]-a[0];
        });

        Arrays.sort(q,(a,b)->{
            return a[0]-b[0];
        });


        int j=0;
        for(int i=0;i<q.length;i++){
            int k=q[i][0],ith=q[i][1],index=q[i][2];
            while(j<=k-1){
                fen.update(A[j][1],1);
                j++;
            }
            int l=0,r=A.length-1;
            int pos=-1;
            while(l<=r){
                int mid=l+(r-l)/2;
                int sum=fen.sumRange(0,mid);
                if(sum>=ith+1){
                    pos=mid;
                    r=mid-1;
                }
                else{
                    l=mid+1;
                }
            }
            res[index]=B[pos];
        }

        for(int i:res){
            out.println(i);
        }
    }


    class Fenwick {
        int tree[];//1-index based
        int A[];
        int arr[];
        public Fenwick(int[] A) {
            this.A=A;
            arr=new int[A.length];
            tree=new int[A.length+1];
            int sum=0;
            for(int i=0;i<A.length;i++){
                update(i,A[i]);
            }
        }

        public void update(int i, int val) {
            arr[i]+=val;
            i++;
            while(i<tree.length){
                tree[i]+=val;
                i+=(i&-i);
            }

        }

        public int sumRange(int i, int j) {
            return pre(j+1)-pre(i);
        }

        public int pre(int i){
            int sum=0;
            while(i>0){
                sum+=tree[i];
                i-=(i&-i);
            }
            return sum;
        }
    }

}


