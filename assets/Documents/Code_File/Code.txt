// Code Create for Project 
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_set>
#include <unordered_map>

using namespace std;

class Graph {
public:
    unordered_map<string, vector<string>> graph;

    void addEdge(string u, string v) {
        graph[u].push_back(v);
        graph[v].push_back(u);
    }
};
void bfs(Graph& graph, string start) {
    unordered_set<string> visited;
    queue<string> queue;
    queue.push(start);
    visited.insert(start);

    while (!queue.empty()) {
        string node = queue.front();
        queue.pop();
        cout << node << " "; // Print mutual friend

        for (string neighbor : graph.graph[node]) {
            if (visited.find(neighbor) == visited.end()) {
                queue.push(neighbor);
                visited.insert(neighbor);
            }
        }
    }
}
void dfs(Graph& graph, string start, unordered_set<string>& visited) {
    cout << start << " "; // Print mutual friend
    visited.insert(start);

    for (string neighbor : graph.graph[start]) {
        if (visited.find(neighbor) == visited.end()) {
            dfs(graph, neighbor, visited);
        }
    }
}
void findMutualFriends(Graph& graph, string user) {
    cout << "Mutual friends (BFS): ";
    bfs(graph, user);
    cout << "\nMutual friends (DFS): ";
    unordered_set<string> visited;
    dfs(graph, user, visited);
}
int main() {
    // Create a sample social media graph
    Graph socialGraph;
    socialGraph.addEdge("Dharmil", "Kavan");
    socialGraph.addEdge("Kavan", "Vedant");
    socialGraph.addEdge("Rajan", "Rutvik");
    socialGraph.addEdge("Avinash", "Vedant");
    socialGraph.addEdge("Preet", "Dharmil");

  
    cout<<"Avinash Friends : "<<endl;
    findMutualFriends(socialGraph, "Avinash");
    cout<<endl<<"Rajan Friends: "<<endl;
    findMutualFriends(socialGraph, "Rajan");
    

    return 0;
}
