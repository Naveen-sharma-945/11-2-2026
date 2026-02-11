#include <iostream>

using namespace std;

// Structure for the Node
struct Node {
    int data;
    Node* next;
};

// Function to insert at the beginning
void insertAtBeginning(Node** head, int value) {
    Node* newNode = new Node(); // Dynamically allocate memory
    newNode->data = value;
    newNode->next = *head;      // Point new node to current head
    *head = newNode;            // Update head to the new node
    cout << "Inserted " << value << " at the beginning.\n";
}

// Function to insert at the end
void insertAtEnd(Node** head, int value) {
    Node* newNode = new Node();
    newNode->data = value;
    newNode->next = nullptr;

    if (*head == nullptr) {
        *head = newNode;
    } else {
        Node* temp = *head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Inserted " << value << " at the end.\n";
}

// Function to delete a node by value
void deleteNode(Node** head, int key) {
    Node* temp = *head;
    Node* prev = nullptr;

    // If head node itself holds the key to be deleted
    if (temp != nullptr && temp->data == key) {
        *head = temp->next;
        delete temp; // Free memory
        cout << "Node with value " << key << " deleted.\n";
        return;
    }

    // Search for the key to be deleted
    while (temp != nullptr && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    // If key was not present in linked list
    if (temp == nullptr) {
        cout << "Value " << key << " not found in the list.\n";
        return;
    }

    // Unlink the node from linked list and delete it
    prev->next = temp->next;
    delete temp; 
    cout << "Node with value " << key << " deleted.\n";
}

// Function to display the list
void displayList(Node* node) {
    if (node == nullptr) {
        cout << "List is empty.\n";
        return;
    }
    cout << "Current List: ";
    while (node != nullptr) {
        cout << node->data << " -> ";
        node = node->next;
    }
    cout << "NULL\n";
}

int main() {
    Node* head = nullptr; // Initialize empty list

    insertAtBeginning(&head, 10);
    insertAtBeginning(&head, 20);
    insertAtEnd(&head, 30);
    insertAtEnd(&head, 40);

    displayList(head);

    deleteNode(&head, 20); // Delete head
    deleteNode(&head, 30); // Delete middle node

    displayList(head);

    return 0;
    
<img width="372" height="214" alt="Screenshot 2026-02-11 095647" src="https://github.com/user-attachments/assets/b2df556c-0154-453a-8269-e8df0e5afded" />





}
