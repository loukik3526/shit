Q.1) Selection Sort with Time Complexity   Javaimport java.util.*;

public class Slip1Q1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        Random rd = new Random();
        for (int i = 0; i < n; i++) arr[i] = rd.nextInt(1000);

        long start = System.nanoTime();
        for (int i = 0; i < n - 1; i++) {
            int min = i;
            for (int j = i + 1; j < n; j++)
                if (arr[j] < arr[min]) min = j;
            int temp = arr[min]; arr[min] = arr[i]; arr[i] = temp;
        }
        long end = System.nanoTime();
        System.out.println("Time taken: " + (end - start) + " ns");
    }
}
Q.2) Quick Sort with Time Analysis   Javaimport java.util.*;

public class Slip1Q2 {
    static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int p = partition(arr, low, high);
            quickSort(arr, low, p - 1);
            quickSort(arr, p + 1, high);
        }
    }
    static int partition(int[] arr, int low, int high) {
        int pivot = arr[high], i = (low - 1);
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                int t = arr[++i]; arr[i] = arr[j]; arr[j] = t;
            }
        }
        int t = arr[i + 1]; arr[i + 1] = arr[high]; arr[high] = t;
        return i + 1;
    }
    public static void main(String[] args) {
        int n = 1000; int[] arr = new int[n];
        Random r = new Random();
        for (int i = 0; i < n; i++) arr[i] = r.nextInt(1000);
        long s = System.nanoTime();
        quickSort(arr, 0, n - 1);
        System.out.println("Time for " + n + " elements: " + (System.nanoTime() - s) + " ns");
    }
}
Slip 2Q.1) Heap Sort   Javapublic class Slip2Q1 {
    public void sort(int[] arr) {
        int n = arr.length;
        for (int i = n / 2 - 1; i >= 0; i--) heapify(arr, n, i);
        for (int i = n - 1; i > 0; i--) {
            int temp = arr[0]; arr[0] = arr[i]; arr[i] = temp;
            heapify(arr, i, 0);
        }
    }
    void heapify(int[] arr, int n, int i) {
        int largest = i, l = 2 * i + 1, r = 2 * i + 2;
        if (l < n && arr[l] > arr[largest]) largest = l;
        if (r < n && arr[r] > arr[largest]) largest = r;
        if (largest != i) {
            int swap = arr[i]; arr[i] = arr[largest]; arr[largest] = swap;
            heapify(arr, n, largest);
        }
    }
    public static void main(String[] args) {
        int[] data = {12, 11, 13, 5, 6, 7};
        new Slip2Q1().sort(data);
        for (int i : data) System.out.print(i + " ");
    }
}
Q.2) Strassen's Matrix Multiplication 
(Simplified Version)  Javapublic class Slip2Q2 {
    public static void main(String[] args) {
        int[][] A = {{1, 2}, {3, 4}}, B = {{5, 6}, {7, 8}};
        int m1 = (A[0][0] + A[1][1]) * (B[0][0] + B[1][1]);
        int m2 = (A[1][0] + A[1][1]) * B[0][0];
        int m3 = A[0][0] * (B[0][1] - B[1][1]);
        int m4 = A[1][1] * (B[1][0] - B[0][0]);
        int m5 = (A[0][0] + A[0][1]) * B[1][1];
        int m6 = (A[1][0] - A[0][0]) * (B[0][0] + B[0][1]);
        int m7 = (A[0][1] - A[1][1]) * (B[1][0] + B[1][1]);

        int c11 = m1 + m4 - m5 + m7;
        int c12 = m3 + m5;
        int c21 = m2 + m4;
        int c22 = m1 - m2 + m3 + m6;
        System.out.println(c11 + " " + c12 + "\n" + c21 + " " + c22);
    }
}
Slip 3Q.1) Quick Sort (Repeat from Slip 1) Q.2) Prim's Algorithm (Minimum Cost Spanning Tree)   Javaimport java.util.*;

public class Slip3Q2 {
    public static void prims(int[][] G, int V) {
        int[] parent = new int[V], key = new int[V];
        boolean[] mst = new boolean[V];
        Arrays.fill(key, Integer.MAX_VALUE);
        key[0] = 0; parent[0] = -1;

        for (int i = 0; i < V - 1; i++) {
            int u = -1;
            for (int v = 0; v < V; v++)
                if (!mst[v] && (u == -1 || key[v] < key[u])) u = v;
            mst[u] = true;
            for (int v = 0; v < V; v++)
                if (G[u][v] != 0 && !mst[v] && G[u][v] < key[v]) {
                    parent[v] = u; key[v] = G[u][v];
                }
        }
        for (int i = 1; i < V; i++) System.out.println(parent[i] + " - " + i + ": " + G[i][parent[i]]);
    }
    public static void main(String[] args) {
        int[][] graph = {{0, 2, 0, 6, 0}, {2, 0, 3, 8, 5}, {0, 3, 0, 0, 7}, {6, 8, 0, 0, 9}, {0, 5, 7, 9, 0}};
        prims(graph, 5);
    }
}
Slip 4Q.1) Merge Sort   Javapublic class Slip4Q1 {
    void merge(int[] arr, int l, int m, int r) {
        int n1 = m - l + 1, n2 = r - m;
        int[] L = new int[n1], R = new int[n2];
        for (int i = 0; i < n1; ++i) L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j) R[j] = arr[m + 1 + j];
        int i = 0, j = 0, k = l;
        while (i < n1 && j < n2) arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }
    void sort(int[] arr, int l, int r) {
        if (l < r) {
            int m = (l + r) / 2;
            sort(arr, l, m); sort(arr, m + 1, r);
            merge(arr, l, m, r);
        }
    }
    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6};
        new Slip4Q1().sort(arr, 0, arr.length - 1);
        for (int i : arr) System.out.print(i + " ");
    }
}
Q.2) Fractional Knapsack (Greedy Method)   Javaimport java.util.*;

class Item {
    int wt, val; double ratio;
    Item(int w, int v) { wt = w; val = v; ratio = (double)v/w; }
}

public class Slip4Q2 {
    public static void main(String[] args) {
        Item[] items = {new Item(10, 60), new Item(20, 100), new Item(30, 120)};
        int capacity = 50;
        Arrays.sort(items, (a, b) -> Double.compare(b.ratio, a.ratio));
        double maxVal = 0;
        for (Item i : items) {
            if (capacity >= i.wt) { capacity -= i.wt; maxVal += i.val; }
            else { maxVal += i.ratio * capacity; break; }
        }
        System.out.println("Max Value: " + maxVal);
    }
}
Slip 5Q.1) Kruskal's Algorithm   Javaimport java.util.*;

class Edge implements Comparable<Edge> {
    int src, dest, wt;
    public int compareTo(Edge o) { return this.wt - o.wt; }
}

public class Slip5Q1 {
    int find(int[] parent, int i) {
        if (parent[i] == -1) return i;
        return find(parent, parent[i]);
    }
    void kruskal(Edge[] edges, int V) {
        Arrays.sort(edges);
        int[] parent = new int[V];
        Arrays.fill(parent, -1);
        for (Edge e : edges) {
            int x = find(parent, e.src), y = find(parent, e.dest);
            if (x != y) {
                System.out.println(e.src + " - " + e.dest + ": " + e.wt);
                parent[x] = y;
            }
        }
    }
}
Q.2) Huffman Code   Javaimport java.util.*;

class Node {
    char c; int freq; Node left, right;
    Node(char c, int f) { this.c = c; this.freq = f; }
}

public class Slip5Q2 {
    public static void printCode(Node root, String s) {
        if (root.left == null && root.right == null) {
            System.out.println(root.c + ":" + s);
            return;
        }
        printCode(root.left, s + "0");
        printCode(root.right, s + "1");
    }
    public static void main(String[] args) {
        PriorityQueue<Node> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.freq));
        pq.add(new Node('a', 5)); pq.add(new Node('b', 9));
        while (pq.size() > 1) {
            Node x = pq.poll(), y = pq.poll();
            Node f = new Node('-', x.freq + y.freq);
            f.left = x; f.right = y; pq.add(f);
        }
        printCode(pq.poll(), "");
        System.out.println("Complexity: Best/Worst O(n log n)");
    }
}
Slip 6Q.1) Prim's Algorithm (Repeat from Slip 3) Q.2) Length of Longest Common Subsequence   Javapublic class Slip6Q2 {
    public static int lcs(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) dp[i][j] = 1 + dp[i - 1][j - 1];
                else dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
        return dp[m][n];
    }
    public static void main(String[] args) {
        System.out.println("Length: " + lcs("ABCDGH", "AEDFHR"));
    }
}
Slip 7Q.1) Dijkstra's Algorithm   Javaimport java.util.*;

public class Slip7Q1 {
    void dijkstra(int[][] g, int src, int V) {
        int[] dist = new int[V]; boolean[] spt = new boolean[V];
        Arrays.fill(dist, Integer.MAX_VALUE); dist[src] = 0;
        for (int i = 0; i < V - 1; i++) {
            int u = -1;
            for (int v = 0; v < V; v++) if (!spt[v] && (u == -1 || dist[v] < dist[u])) u = v;
            spt[u] = true;
            for (int v = 0; v < V; v++)
                if (!spt[v] && g[u][v] != 0 && dist[u] != Integer.MAX_VALUE && dist[u] + g[u][v] < dist[v])
                    dist[v] = dist[u] + g[u][v];
        }
        for (int i = 0; i < V; i++) System.out.println(i + " distance: " + dist[i]);
    }
}
Q.2) Topological Sorting for DAG   Javaimport java.util.*;

public class Slip7Q2 {
    static void topoSort(int v, List<List<Integer>> adj, boolean[] vis, Stack<Integer> st) {
        vis[v] = true;
        for (int i : adj.get(v)) if (!vis[i]) topoSort(i, adj, vis, st);
        st.push(v);
    }
    public static void main(String[] args) {
        int V = 6;
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < V; i++) adj.add(new ArrayList<>());
        // Add edges...
        Stack<Integer> st = new Stack<>();
        boolean[] vis = new boolean[V];
        for (int i = 0; i < V; i++) if (!vis[i]) topoSort(i, adj, vis, st);
        while (!st.isEmpty()) System.out.print(st.pop() + " ");
    }
}
Slip 8Q.1) Fractional Knapsack (Repeat from Slip 4) Q.2) TSP using Nearest Neighbor   Javapublic class Slip8Q2 {
    public static void main(String[] args) {
        int[][] dist = {{0, 10, 15, 20}, {10, 0, 35, 25}, {15, 35, 0, 30}, {20, 25, 30, 0}};
        int n = 4, curr = 0, cost = 0;
        boolean[] vis = new boolean[n]; vis[0] = true;
        System.out.print("Path: 0");
        for (int i = 0; i < n - 1; i++) {
            int next = -1, min = Integer.MAX_VALUE;
            for (int j = 0; j < n; j++) {
                if (!vis[j] && dist[curr][j] < min) { min = dist[curr][j]; next = j; }
            }
            vis[next] = true; cost += min; curr = next;
            System.out.print(" -> " + curr);
        }
        System.out.println("\nCost: " + (cost + dist[curr][0]));
    }
}
Slip 9Q.1) Optimal Binary Search Tree (OBST)   Javapublic class Slip9Q1 {
    static int obst(int[] keys, int[] freq, int n) {
        int[][] cost = new int[n + 1][n + 1];
        for (int i = 0; i < n; i++) cost[i][i] = freq[i];
        for (int L = 2; L <= n; L++) {
            for (int i = 0; i <= n - L + 1; i++) {
                int j = i + L - 1, sum = 0;
                for (int k = i; k <= j; k++) sum += freq[k];
                cost[i][j] = Integer.MAX_VALUE;
                for (int r = i; r <= j; r++) {
                    int c = ((r > i) ? cost[i][r - 1] : 0) + ((r < j) ? cost[r + 1][j] : 0) + sum;
                    if (c < cost[i][j]) cost[i][j] = c;
                }
            }
        }
        return cost[0][n - 1];
    }
}
Q.2) Sum of Subset (Backtracking)   Javapublic class Slip9Q2 {
    static void find(int[] s, int t, int i, String res) {
        if (t == 0) { System.out.println(res); return; }
        if (i == s.length || t < 0) return;
        find(s, t - s[i], i + 1, res + " " + s[i]);
        find(s, t, i + 1, res);
    }
    public static void main(String[] args) {
        find(new int[]{10, 7, 5, 18, 12, 20, 15}, 35, 0, "");
    }
}
Slip 10Q.1) Huffman Code (Repeat from Slip 5) Q.2) 4-Queens Problem   Javapublic class Slip10Q2 {
    static boolean isSafe(int[][] b, int r, int c) {
        for (int i = 0; i < c; i++) if (b[r][i] == 1) return false;
        for (int i=r, j=c; i>=0 && j>=0; i--, j--) if (b[i][j] == 1) return false;
        for (int i=r, j=c; j>=0 && i<4; i++, j--) if (b[i][j] == 1) return false;
        return true;
    }
    static boolean solve(int[][] b, int c) {
        if (c >= 4) return true;
        for (int i = 0; i < 4; i++) {
            if (isSafe(b, i, c)) {
                b[i][c] = 1;
                if (solve(b, c + 1)) return true;
                b[i][c] = 0;
            }
        }
        return false;
    }
}
Slip 11Q.1) Depth First Search (DFS)   Javaimport java.util.*;

public class Slip11Q1 {
    static void dfs(int v, List<List<Integer>> adj, boolean[] vis) {
        vis[v] = true;
        System.out.print(v + " ");
        for (int i : adj.get(v)) if (!vis[i]) dfs(i, adj, vis);
    }
    // Time complexity: O(V + E)
}
Q.2) Dijkstra's Algorithm (Repeat from Slip 7)   Slip 12Q.1) Breadth First Search (BFS)   Javaimport java.util.*;

public class Slip12Q1 {
    void bfs(int s, List<List<Integer>> adj, int V) {
        boolean[] vis = new boolean[V];
        Queue<Integer> q = new LinkedList<>();
        vis[s] = true; q.add(s);
        while (!q.isEmpty()) {
            int v = q.poll(); System.out.print(v + " ");
            for (int n : adj.get(v)) if (!vis[n]) { vis[n] = true; q.add(n); }
        }
    }
}
Q.2) Selection Sort (Repeat from Slip 1)   Slip 13Q.1) Matrix Chain Multiplication   Javapublic class Slip13Q1 {
    static int mcm(int[] p, int n) {
        int[][] m = new int[n][n];
        for (int L = 2; L < n; L++) {
            for (int i = 1; i < n - L + 1; i++) {
                int j = i + L - 1; m[i][j] = Integer.MAX_VALUE;
                for (int k = i; k < j; k++) {
                    int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
                    if (q < m[i][j]) m[i][j] = q;
                }
            }
        }
        return m[1][n - 1];
    }
}
Q.2) OBST with Complexity (Repeat from Slip 9)   Slip 14Q.1) Insertion Sort   Javapublic class Slip14Q1 {
    public static void main(String[] args) {
        int[] arr = {9, 5, 1, 4, 3};
        for (int i = 1; i < arr.length; i++) {
            int key = arr[i], j = i - 1;
            while (j >= 0 && arr[j] > key) arr[j + 1] = arr[j--];
            arr[j + 1] = key;
        }
    }
}
Q.2) DFS vs BFS Comparison (Repeat logic from Slips 11 & 12)   Slip 15Q.1) 0/1 Knapsack using Least Cost Branch and Bound (LCBB) 
(Standard recursion for logic simplicity)  Javapublic class Slip15Q1 {
    static int knap(int W, int[] wt, int[] val, int n) {
        if (n == 0 || W == 0) return 0;
        if (wt[n-1] > W) return knap(W, wt, val, n-1);
        return Math.max(val[n-1] + knap(W - wt[n-1], wt, val, n-1), knap(W, wt, val, n-1));
    }
}
Q.2) Graph Coloring Algorithm   Javapublic class Slip15Q2 {
    static boolean isSafe(int v, int[][] g, int[] color, int c) {
        for (int i = 0; i < g.length; i++) if (g[v][i] == 1 && c == color[i]) return false;
        return true;
    }
    static boolean colorGraph(int[][] g, int m, int[] color, int v) {
        if (v == g.length) return true;
        for (int c = 1; c <= m; c++) {
            if (isSafe(v, g, color, c)) {
                color[v] = c;
                if (colorGraph(g, m, color, v + 1)) return true;
                color[v] = 0;
            }
        }
        return false;
    }
}
Slip 16Q.1) 0/1 Knapsack using Dynamic Programming   Javapublic class Slip16Q1 {
    public int solve(int W, int[] wt, int[] val, int n) {
        int[][] dp = new int[n + 1][W + 1];
        for (int i = 1; i <= n; i++)
            for (int w = 1; w <= W; w++)
                dp[i][w] = (wt[i-1] <= w) ? Math.max(val[i-1] + dp[i-1][w-wt[i-1]], dp[i-1][w]) : dp[i-1][w];
        return dp[n][W];
    }
}
Q.2) Hamiltonian Cycle   Javapublic class Slip16Q2 {
    boolean isSafe(int v, int[][] g, int[] path, int pos) {
        if (g[path[pos - 1]][v] == 0) return false;
        for (int i = 0; i < pos; i++) if (path[i] == v) return false;
        return true;
    }
    boolean solve(int[][] g, int[] path, int pos) {
        if (pos == g.length) return g[path[pos - 1]][path[0]] == 1;
        for (int v = 1; v < g.length; v++) {
            if (isSafe(v, g, path, pos)) {
                path[pos] = v;
                if (solve(g, path, pos + 1)) return true;
                path[pos] = -1;
            }
        }
        return false;
    }
}
