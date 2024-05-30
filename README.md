# DIJKSTRA-MATRIZ-2

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef pair<int, int> pii;
const int inf = INT_MAX / 2;
const int maxn = 500;
int n;
int dist[maxn][maxn];
bool visit[maxn][maxn];
int grafo[maxn][maxn];

bool verificaLimites(int x, int y){
    return x >= 0 && x < n && y >= 0 && y < n;
}

int dx[] = {1,-1,0,0};
int dy[] = {0,0,1,-1};

void dijkstra(int x_inicial, int y_inicial){
    for(int i = 0; i < n; i++){
        for(int j = 0; j < n; j++){
            dist[i][j] = inf;
            visit[i][j] = false;
        }
    }
    
    dist[x_inicial][y_inicial] = 0;
    priority_queue<pair<int, pii>, vector<pair<int, pii>>, greater<pair<int, pii>>> fila;
    fila.push({0, {x_inicial, y_inicial}});
    
    while(!fila.empty()){
        int x_atual = fila.top().second.first;
        int y_atual = fila.top().second.second;
        fila.pop();
        
        if(visit[x_atual][y_atual]) continue;
        visit[x_atual][y_atual] = true;
        
        for(int i = 0; i < 4; i++){
            int x_novo = x_atual + dx[i];
            int y_novo = y_atual + dy[i];
            
            if(verificaLimites(x_novo, y_novo)){
                int peso = grafo[x_novo][y_novo];
                if(dist[x_novo][y_novo] > dist[x_atual][y_atual] + peso){
                    dist[x_novo][y_novo] = dist[x_atual][y_atual] + peso;
                    fila.push({dist[x_novo][y_novo], {x_novo, y_novo}});
                }
            }
        }
    }
}

int main()
{
    cin >> n;
    
    for(int i = 0; i < n; i++){
        for(int j = 0; j < n; j++){
            cin >> grafo[i][j];
        }
    }
    
    dijkstra(0, 0);
    
    cout << dist[n - 1][n - 1] << endl;
    return 0;
}
```
