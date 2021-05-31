# MST 알고리즘 2번째 Prime 알고리즘

1. Prim 알고리즘은 시작점을 정해놓고 하나의 트리만 구성해 나가기 때문에 사이클이 형성되지 않음.
2. 각 정점마다 정점의 개수만큼 배열을 선언해서 가장 최소 가중치를 갖는 간선을 선택해감.
3. 방문, 미방문을 나타내는 vector가 필요함
4. Time complexity는 O(N^2)


```c++

#include <string>
#include <vector>
#include <set>
#include <algorithm>
#include <functional>

using namespace std;



int solution(int n, vector<vector<int>> costs) {
    int answer = 0;
    
    vector<vector<int>> graph(n, vector<int>(n));
    for(auto cost : costs)
    {
        graph[cost[0]][cost[1]] = cost[2];
        graph[cost[1]][cost[0]] = cost[2];
    }
    
    int len = costs.size();
    
    vector<int> visited;
    vector<int> unvisited(n);
    
    visited.push_back(0);
    for(int i=1;i<n;i++)
        unvisited[i] = i;
    
    unvisited.erase(unvisited.begin());
   
    
    for(int i=1;i<n;i++)
    {
        
        int min = 9999999;
        int midx=0;
        
        for(int j=0;j<i;j++)
        {
            for(int k=0;k<n-i;k++)
            {
                if(graph[visited[j]][unvisited[k]]>0 && min>graph[visited[j]][unvisited[k]])
                {
                    min = graph[visited[j]][unvisited[k]];
                    midx = k;
                }
            }
        }
        visited.push_back(unvisited[midx]);
        unvisited.erase(unvisited.begin()+midx);
        answer+=min;
        
        
        
    }
    
    
    
    
    
    
    
    return answer;
}



```
