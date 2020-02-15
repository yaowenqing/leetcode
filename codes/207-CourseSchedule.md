There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Example 1:
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

Example 2:
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Note:
The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
You may assume that there are no duplicate edges in the input prerequisites.

BFS方法

对于BFS的方法，我们首先需要构建出一个有向图，对于二元对[i, j]，因为j是i的先决条件，因此我们构建有向图使得j指向i。
之后，我们计算每一个顶点的入度。然后我们在图中寻找图中入度为0的顶点。

如果一个图中没有入度为0的顶点，说明这个图中存在环，我们返回false；
否则，我们将这个入度为0的顶点的入度设置为-1防止再次访问它，并将它的邻居的入度都减少1。几何含义是将这个顶点从图中删除。

重复numCourses次之后，所有的顶点入度都变为-1时才可返回true

bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        Graph G = buildGraph(numCourses, prerequisites);
        vector<int> degree = calIndegree(G);
        //经历了numCourses次循环后所有的顶点入度都变为-1时才可返回true
        for(int i=0;i<numCourses;i++){
            int j=0;
            while(j<numCourses){
                if(degree[j]==0)//找到了入度为0的点
                    break;
                j++;
            }
            if(j==numCourses)//没有入度为0的点，说明图中有环
                return false;
            //因为degree[j]此时为0，所以--使得j的入度为-1
            //类似于将节点j从图中删除
            degree[j]--;    
            for(auto adj : G[j])
                //因为我们“将节点j从图中删除”，因此将节点j相邻的节点的入度都-1
                degree[adj]--;  
        }
        return true;
    }
    
    typedef vector<vector<int>> Graph;
    
    //根据所给条件构建有向图，second指向first
    Graph buildGraph(int numCourses,vector<vector<int>>&prerequisites){
        Graph G(numCourses);
        for(auto p:prerequisites)
            G[p[1]].push_back(p[0]);
        return G;
    }
    
    //计算节点入度
    vector<int> calIndegree(Graph&G){
        vector<int> degree(G.size(),0);
        for(auto v:G)
            for(auto adj:v)
                degree[adj]++;
        return degree;
}


DFS方法

对于DFS的方法，我们在访问时会从其中一个节点出发，然后不断的深入访问，如果我们返回到了我们当前路径中已经访问过的节点，就说明图是存在环的。
否则，我们就从另外一个尚未访问过的节点出发，并重复这个过程。
