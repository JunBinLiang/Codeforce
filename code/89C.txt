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
        //reading /writing file
        //Scanner sc=new Scanner(new File("input.txt"));
        //PrintWriter pr=new PrintWriter("output.txt");

        int T=1;
        for(int t=0;t<T;t++){
            int n=Int();int m=Int();
            char A[][]=new char[n][m];
            for(int i=0;i<n;i++){
                String s=Str();
                for(int j=0;j<m;j++){
                    A[i][j]=s.charAt(j);
                }
            }

            Solution sol=new Solution(out);
            sol.solution(A);
        }
        out.close();

    }

    public static int[] Arr(int n){
        int A[]=new int[n];
        for(int i=0;i<n;i++)A[i]=Int();
        return A;
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
    int INF=Integer.MAX_VALUE;
    int MOD=1000000007;
    public Solution(PrintWriter out){
        this.out=out;
    }

    int pre[];
    int next[];
    int up[];
    int down[];

    int pre1[];
    int next1[];
    int up1[];
    int down1[];

    public void solution(char A[][]){
        int n=A.length,m=A[0].length;
        pre=new int[n*m+1];
        next=new int[n*m+1];
        up=new int[n*m+1];
        down=new int[n*m+1];

        pre1=new int[n*m+1];
        next1=new int[n*m+1];
        up1=new int[n*m+1];
        down1=new int[n*m+1];

        int res=-1;
        int cnt=0;
        firstinit(A);
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(A[i][j]=='.')continue;
                init();
                int jump=dfs(A,i*A[0].length+j);
                if(jump>res){
                    res=jump;
                    cnt=1;
                }
                else if(jump==res){
                    cnt++;
                }
            }
        }
        out.println(res+" "+cnt);
    }


    public void firstinit(char A[][]){
        Arrays.fill(pre1,-1);
        Arrays.fill(next1,-1);
        Arrays.fill(up1,-1);
        Arrays.fill(down1,-1);
        for(int i=0;i<A.length;i++){
            TreeSet<Integer>tree=new TreeSet<>();
            for(int j=0;j<A[0].length;j++){
                if(A[i][j]!='.'){
                    tree.add(i*A[0].length+j);
                }
            }
            for(int j=0;j<A[0].length;j++){
                if(A[i][j]=='.')continue;
                int id=i*A[0].length+j;
                Integer hi=tree.higher(id);
                if(hi!=null){
                    next1[id]=hi;
                }
                Integer lo=tree.lower(id);
                if(lo!=null){
                    pre1[id]=lo;
                }
            }
        }


        for(int j=0;j<A[0].length;j++){
            TreeSet<Integer>tree=new TreeSet<>();
            for(int i=0;i<A.length;i++){
                if(A[i][j]!='.'){
                    tree.add(i*A[0].length+j);
                }
            }
            for(int i=0;i<A.length;i++){
                int id=i*A[0].length+j;
                if(A[i][j]!='.'){
                    Integer hi=tree.higher(id);
                    if(hi!=null){
                        down1[id]=hi;
                    }
                    Integer lo=tree.lower(id);
                    if(lo!=null){
                        up1[id]=lo;
                    }
                }
            }
        }

    }

    public void init(){
        for(int i=0;i<pre1.length;i++){
            pre[i]=pre1[i];
            next[i]=next1[i];
            down[i]=down1[i];
            up[i]=up1[i];
        }
    }

    public void del(int id){
        int preid=pre[id];
        int nextid=next[id];
        if(preid!=-1)next[preid]=nextid;
        if(nextid!=-1)pre[nextid]=preid;

        int upid=up[id];
        int downid=down[id];
        if(upid!=-1)down[upid]=downid;
        if(downid!=-1)up[downid]=upid;

    }

    public int  dfs(char A[][],int id){
        if(id==-1)return 0;
        int i=id/A[0].length;
        int j=id%A[0].length;
        char c=A[i][j];

        if(c=='U'){
            int nextid=up[id];
            del(id);
            return 1+dfs(A,nextid);
        }
        else if(c=='D'){
            int nextid=down[id];
            del(id);
            return 1+dfs(A,nextid);
        }
        else if(c=='R'){
            int nextid=next[id];
            del(id);
            return 1+dfs(A,nextid);
        }
        else{
            int nextid=pre[id];
            del(id);
            return 1+dfs(A,nextid);
        }
    }
}

