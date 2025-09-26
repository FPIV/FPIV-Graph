# FPIV Graph: The Ultimate Dart Graph Algorithms Library 🚀

**FPIV Graph** is a high-performance, feature-rich Dart library offering a comprehensive suite of graph algorithms for both directed and undirected graphs. Designed for speed, scalability, and clarity, it is ideal for research, education, and production use.

## Features

- **Breadth-First Search (BFS)**, **Depth-First Search (DFS)**
- **Shortest Path Algorithms**: Dijkstra, Bellman-Ford, Floyd-Warshall, Johnson’s, SPFA, Yen’s K-Shortest Paths
- **Minimum Spanning Tree**: Kruskal, Prim
- **Max Flow**: Edmonds-Karp, Dinic’s Algorithm
- **Strongly Connected Components**: Kosaraju, Tarjan
- **Topological Sort**, **Transitive Closure**
- **Eulerian & Hamiltonian Paths**, **Chinese Postman**
- **Graph Coloring**, **Bipartite Checking**
- **Bridge & Articulation Point Finding**
- **Cycle Detection**, **Tree Diameter**
- **Stoer-Wagner Min Cut**
- ...and more!

All algorithms are implemented with efficiency and clarity in mind, and the library is modular for easy extension.

## Benchmark Power

FPIV Graph is not just feature-rich—it’s fast. The included benchmark suite rigorously tests all algorithms on graphs with up to **100,000 elements** (vertices/edges), covering scenarios from sparse to dense, undirected and directed, trees, and flow networks. Results show:

- **Linear and near-linear algorithms** remain extremely fast even on large graphs.
- **Advanced algorithms** (e.g., Johnson’s, Floyd-Warshall, Dinic’s) are optimized for practical use.
- **NP-Complete algorithms** are included for completeness and small-scale experimentation.

Run your own benchmarks with:

```bash
dart run .benchmark/benchmark.dart
```

and see detailed performance metrics for every algorithm.

## Getting started

Add to your `pubspec.yaml`:

```yaml
dependencies:
	fpiv_graph: 0.1.0
```

Import in your Dart code:

```dart
import 'package:fpiv_graph/fpiv_graph.dart';
```

## Usage

Example: Running 

```dart
import 'package:fpiv_graph/fpiv_graph.dart';

void main() {
  print('--- FPIV Graph Library Examples ---');

  // ===================================================================
  // Section 1: Graph Traversal & Basic Properties
  // ===================================================================
  print('\n--- Traversal & Properties ---');
  final unweightedGraph = <String, List<String>>{
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': [],
  };

  // BFS: Traverses the graph level by level.
  print('BFS from A: ${bfs(unweightedGraph, 'A')}');

  // DFS: Traverses the graph by exploring as far as possible along each branch.
  print('DFS from A: ${dfs(unweightedGraph, 'A')}');
  
  // Connected Components: Finds sets of interconnected nodes.
  final components = connectedComponents({'A': ['B'], 'B': ['A'], 'C': []});
  print('Connected Components: $components');

  // Bipartite Check: Determines if the graph can be colored with two colors.
  final isBipartiteGraph = isBipartite({ 1: [2, 4], 2: [1, 3], 3: [2, 4], 4: [1, 3] });
  print('Is graph bipartite? $isBipartiteGraph');


  // ===================================================================
  // Section 2: Pathfinding & Shortest Path
  // ===================================================================
  print('\n--- Pathfinding ---');
  final weightedGraph = <String, List<WeightedEdge<String>>>{
    'A': [WeightedEdge('A', 'B', 1), WeightedEdge('A', 'C', 4)],
    'B': [WeightedEdge('B', 'C', 2), WeightedEdge('B', 'D', 5)],
    'C': [WeightedEdge('C', 'D', 1)],
    'D': [],
  };

  // Dijkstra: Finds the shortest path from a single source (no negative weights).
  print('Dijkstra (from A): ${dijkstra(weightedGraph, 'A')}');

  // Bellman-Ford: Finds the shortest path, handles negative weights.
  final nodes = {'A', 'B', 'C', 'D'};
  final edges = weightedGraph.values.expand((list) => list).toList();
  print('Bellman-Ford (from A): ${bellmanFord(nodes, edges, 'A')}');

  // Floyd-Warshall: Finds all-pairs shortest paths.
  final allPaths = floydWarshall(nodes, edges);
  print('Floyd-Warshall (A to D): ${allPaths['A']!['D']}');
  
  // Unweighted Shortest Path: Finds the path with the fewest edges.
  final path = shortestPathUnweighted(unweightedGraph, 'A', 'F');
  print('Shortest unweighted path (A to F): $path');


  // ===================================================================
  // Section 3: Minimum Spanning Tree (MST)
  // An MST is a subset of edges that connects all vertices with minimum total weight.
  // ===================================================================
  print('\n--- Minimum Spanning Tree ---');

  // Prim's Algorithm: Builds the MST by growing from a single node.
  final primMst = primMST(weightedGraph);
  final primWeight = primMst.fold<num>(0, (sum, edge) => sum + edge.weight);
  print('Prim MST total weight: $primWeight');

  // Kruskal's Algorithm: Builds the MST by adding the cheapest edges first.
  final kruskalMst = kruskalMST(nodes, edges);
  print('Kruskal MST edges: ${kruskalMst.map((e) => '(${e.source}-${e.target}:${e.weight})').toList()}');


  // ===================================================================
  // Section 4: Directed & Acyclic Graphs (DAGs)
  // ===================================================================
  print('\n--- Directed & Acyclic Graphs ---');
  
  // Topological Sort: Provides a linear ordering of nodes in a DAG.
  final sorted = topologicalSort(<int, List<int>>{ 1: [2], 2: [3], 3: [4], 4: [] });
  print('Topological Sort: $sorted');

  // Cycle Detection (Directed): Checks for cycles in a directed graph.
  final hasCycle = hasCycleDirected(<int, List<int>>{ 1: [2], 2: [3], 3: [1] });
  print('Directed graph has cycle? $hasCycle');

  // Kosaraju's Algorithm: Finds strongly connected components in a directed graph.
  final sccs = kosarajuSCC(<int, List<int>>{ 1: [2], 2: [3], 3: [1, 4], 4: [5], 5: [6], 6: [4] });
  print('Strongly Connected Components (count): ${sccs.length}');
  

  // ===================================================================
  // Section 5: Advanced Connectivity
  // ===================================================================
  print('\n--- Advanced Connectivity ---');
  final connectivityGraph = { 1: [2], 2: [1, 3, 4], 3: [2], 4: [2] };

  // Articulation Points (Cut Vertices): Nodes whose removal increases connected components.
  final points = articulationPoints(connectivityGraph);
  print('Articulation Points: $points');
}
```

See the `/example` folder for more advanced usage.

## Additional information

- Full API documentation: [coming soon]
- Issues and contributions welcome on GitHub
- Created and maintained by FPIV
