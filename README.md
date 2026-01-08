# Eco-Bin-Tracker-C-Smart-Waste-Collection-System
A smart waste collection system inspired by a real-life problem and implemented using core Data Structures in C++.



Author

Uddin Md Borhan
Computer Engineering Student
Tongmyong University, Busan, South Korea

Project Motivation (Real-Life Story)

This project is directly inspired by my personal experience working at a seafood restaurant in Busan.

Every day, the garbage truck follows a fixed route and fixed time. If we miss that time even once, the truck does not return, and the waste remains until the next day. This creates problems such as overflowing bins, bad smell and hygiene issues, and inefficient waste management.

While facing this situation daily, I realized that this real-world problem closely matches several Data Structure concepts that we learn in class. That realization became the foundation of EcoBin Tracker.

Project Overview

EcoBin Tracker is a simulated smart-city waste management system that improves traditional garbage collection by using:

Queue for normal bin pickup order
Stack for handling missed bins
Linked List for dynamic route updates
Graph and Dijkstra’s Algorithm for shortest path optimization
This project demonstrates how theoretical Data Structures can solve real-life urban problems efficiently.

Project Objectives
Simulate a smart waste collection system
Reduce bin overflow using logical scheduling
Optimize fuel usage through shortest path routing
Automatically handle missed garbage bins
Prove the practical importance of Data Structures
System Components
Smart Bins (Simulated)
Each bin has a unique ID
Sends data for collection order
Garbage Truck Logic
Uses Queue for regular pickups
Uses Stack to revisit missed bins (Last Missed, First Collected)
Control Server (Logic Layer)
Uses Linked List to update routes dynamically
Uses Graph and Dijkstra’s Algorithm to calculate shortest distances
Data Structures Used and Why
Queue – Normal Collection
Follows First Come, First Served (FCFS)
Matches real garbage truck behavior
Stack – Missed Bin Recovery
Stores bins that were skipped
Last missed bin is collected first
Linked List – Dynamic Routes
Allows easy insertion and deletion of bins
Suitable for changing routes in real time
Graph and Dijkstra – Shortest Path
Represents city layout as nodes and edges
Finds the most fuel-efficient route
Technologies Use
Language: C++
Concepts: Data Structures and Algorithms
How to Run the Project
#include
#include
using namespace std;

void queueDemo() {
cout << "\n=== QUEUE (Normal Collection) ===" << endl;
queue route;

// Add bins to route
route.push(12);
route.push(18);
route.push(22);
route.push(30);

cout << "Queue Route: ";
while (!route.empty()) {
    cout << "Bin" << route.front() << " ";
    route.pop();
}
cout << endl;
}

// ========================================
// 2. STACK - Missed Bin Recovery
// ========================================
#include

void stackDemo() {
cout << "\n=== STACK (Missed Bins) ===" << endl;
stack missed;

// Add missed bins
missed.push(22);
missed.push(18);
missed.push(8);

cout << "Missed Bin Stack (LIFO): ";
while (!missed.empty()) {
    cout << "Bin" << missed.top() << " ";
    missed.pop();
}
cout << endl;
}

// ========================================
// 3. LINKED LIST - Dynamic Route
// ========================================

struct Node {
int binId;
Node* next;
};

class LinkedList {
public:
Node* head = NULL;

void addBin(int id) {
    Node* newNode = new Node();
    newNode->binId = id;
    newNode->next = NULL;

    if (!head) {
        head = newNode;
        return;
    }

    Node* temp = head;
    while (temp->next) {
        temp = temp->next;
    }
    temp->next = newNode;
}

void show() {
    cout << "\n=== LINKED LIST (Dynamic Route) ===" << endl;
    cout << "Route: ";
    Node* temp = head;
    while (temp) {
        cout << "Bin" << temp->binId << " -> ";
        temp = temp->next;
    }
    cout << "END" << endl;
}
};

void linkedListDemo() {
LinkedList route;
route.addBin(12);
route.addBin(18);
route.addBin(22);
route.addBin(30);
route.show();
}

// ========================================
// 4. GRAPH - Dijkstra Shortest Path
// ========================================
#include
#include

vector<vector<pair<int, int>>> graph;

void dijkstra(int start, int n) {
vector dist(n, INT_MAX);
vector visited(n, false);

dist[start] = 0;

for (int i = 0; i < n; i++) {
    int u = -1;
    for (int j = 0; j < n; j++) {
        if (!visited[j] && (u == -1 || dist[j] < dist[u])) {
            u = j;
        }
    }

    visited[u] = true;

    for (auto edge : graph[u]) {
        int v = edge.first;
        int weight = edge.second;
        if (dist[u] + weight < dist[v]) {
            dist[v] = dist[u] + weight;
        }
    }
}

cout << "\n=== GRAPH (Dijkstra Shortest Path) ===" << endl;
for (int i = 0; i < n; i++) {
    cout << "Distance to Bin" << i << " = " << dist[i] << " km" << endl;
}
}

void graphDemo() {
int n = 5; // 5 bins
graph.resize(n);

// Add edges (bin connections with distance)
graph[0].push_back({ 1, 5 });
graph[0].push_back({ 2, 3 });
graph[1].push_back({ 2, 2 });
graph[1].push_back({ 3, 6 });
graph[2].push_back({ 3, 4 });
graph[2].push_back({ 4, 7 });
graph[3].push_back({ 4, 3 });

dijkstra(0, n); // Start from Bin 0
}

// ========================================
// MAIN FUNCTION
// ========================================

int main() {
cout << "=====================================" << endl;
cout << " ECOBIN TRACKER - C++ VERSION" << endl;
cout << "=====================================" << endl;

// 1. Queue Demo
queueDemo();

// 2. Stack Demo
stackDemo();

// 3. Linked List Demo
linkedListDemo();

// 4. Graph Demo
graphDemo();

cout << "\n=====================================" << endl;
cout << "   ALL DATA STRUCTURES COMPLETED" << endl;
cout << "=====================================" << endl;

return 0;
}

Sample Output
=== QUEUE (Normal Collection) ===
Queue Route: Bin12 Bin18 Bin22 Bin30

=== STACK (Missed Bins) ===
Missed Bin Stack (LIFO): Bin8 Bin18 Bin22

=== LINKED LIST (Dynamic Route) ===
Route: Bin12 -> Bin18 -> Bin22 -> Bin30 -> END

=== GRAPH (Dijkstra Shortest Path) ===
Distance to Bin0 = 0 km
Distance to Bin1 = 5 km
Distance to Bin2 = 3 km
Distance to Bin3 = 7 km
Distance to Bin4 = 10 km
Future Improvements
Add real sensor data using IoT
Implement real-time bin overflow alerts
Add a GUI or web dashboard
Use GPS-based live routing
Extend the system into a full Smart City solution
Learning Outcomes
Through this project, I learned:

How Data Structures apply to real-life systems
How to design logic based on real problems
How to structure and document a complete C++ project
How to present a technical solution professionally
Acknowledgment
Special thanks to my professors at Tongmyong University and to my real-life work experience in Busan, which inspired this project.

Contact
If you have any suggestions or feedback, feel free to connect.

Uddin Md Borhan
Computer Engineering, Tongmyong University
Busan, South Korea
Email: [mdborhanuddin829@gmail.com]

