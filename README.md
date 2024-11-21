# Disney-Heap-Adventure
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Structure to hold treasure details
struct Treasure {
    string princess;  // Name of the princess
    string item;      // Name of the treasure
    int priority;     // Magical priority value
};

// Function to display the heap
void displayHeap(const vector<Treasure>& heap) {
    cout << "Heap: ";
    for (auto& treasure : heap) {
        cout << treasure.priority << " ";
    }
    cout << endl;
}

// Insert into Max-Heap
void insertHeap(vector<Treasure>& heap, const Treasure& treasure) {
    heap.push_back(treasure);
    int i = heap.size() - 1;

    // Heapify up
    while (i > 0 && heap[i].priority > heap[(i - 1) / 2].priority) {
        swap(heap[i], heap[(i - 1) / 2]);
        i = (i - 1) / 2;
    }

    displayHeap(heap);
}

// Delete root from Max-Heap
void deleteRoot(vector<Treasure>& heap) {
    if (heap.empty()) {
        cout << "Heap is empty!" << endl;
        return;
    }

    cout << "Removing the most magical treasure: " << heap[0].princess << "'s " << heap[0].item << endl;
    heap[0] = heap.back();
    heap.pop_back();

    // Heapify down
    int i = 0;
    while (i < heap.size()) {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int largest = i;

        if (left < heap.size() && heap[left].priority > heap[largest].priority) largest = left;
        if (right < heap.size() && heap[right].priority > heap[largest].priority) largest = right;

        if (largest != i) {
            swap(heap[i], heap[largest]);
            i = largest;
        } else {
            break;
        }
    }

    displayHeap(heap);
}

// Heapify a random array
void buildHeap(vector<Treasure>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; i--) {
        int largest = i, left = 2 * i + 1, right = 2 * i + 2;

        if (left < heap.size() && heap[left].priority > heap[largest].priority) largest = left;
        if (right < heap.size() && heap[right].priority > heap[largest].priority) largest = right;

        if (largest != i) swap(heap[i], heap[largest]);
    }

    displayHeap(heap);
}

int main() {
    vector<Treasure> heap;

    cout << "Task 1: Insert Magical Treasures" << endl;
    vector<Treasure> treasures = {
        {"Moana", "Necklace", 50}, 
        {"Elsa", "Crown", 40}, 
        {"Rapunzel", "Hairbrush", 30}, 
        {"Ariel", "Pearl", 60}, 
        {"Tiana", "Frog Pin", 35}, 
        {"Cinderella", "Glass Slipper", 45}, 
        {"Belle", "Book", 25}
    };

    for (auto& treasure : treasures) {
        cout << "Adding " << treasure.princess << "'s " << treasure.item << " (priority: " << treasure.priority << ")" << endl;
        insertHeap(heap, treasure);
    }

    cout << "\nTask 2: Remove the Most Magical Treasure" << endl;
    deleteRoot(heap);

    cout << "\nTask 3: Organize Random Treasures into a Max-Heap" << endl;
    vector<Treasure> randomTreasures = {
        {"Moana", "Necklace", 30}, {"Elsa", "Crown", 50}, {"Rapunzel", "Hairbrush", 35}, 
        {"Ariel", "Pearl", 60}, {"Tiana", "Frog Pin", 25}, {"Cinderella", "Glass Slipper", 40}
    };
    cout << "Original treasures: ";
    for (auto& treasure : randomTreasures) {
        cout << treasure.priority << " ";
    }
    cout << endl;

    buildHeap(randomTreasures);

    return 0;
