/**
 * @file LinkedList.cpp
 * @author Your Name
 * @brief Implementation of a Singly Linked List in C++
 * @details Features: Insertion (Start/End), Deletion, and Display using 
 * dynamic memory management (new/delete).
 */

#include <iostream>

using namespace std;

// Structure for the Node
struct Node {
    int data;
    Node* next;

    // Constructor to simplify node creation
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // 1. Insertion at the beginning
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
        cout << "[+] Node " << value << " inserted at the beginning." << endl;
    }

    // 2. Insertion at the end
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "[+] Node " << value << " inserted at the end." << endl;
    }

    // 3. Deletion of a node by value
    void deleteNode(int key) {
        if (head == nullptr) {
            cout << "[!] List is empty. Deletion failed." << endl;
            return;
        }

        Node* temp = head;
        Node* prev = nullptr;

        // If head node itself holds the key
        if (temp != nullptr && temp->data == key) {
            head = temp->next;
            delete temp; 
            cout << "[-] Node " << key << " deleted." << endl;
            return;
        }

        // Search for the key
        while (temp != nullptr && temp->data != key) {
            prev = temp;
            temp = temp->next;
        }

        // If key not found
        if (temp == nullptr) {
            cout << "[!] Value " << key << " not found in the list." << endl;
            return;
        }

        prev->next = temp->next;
        delete temp;
        cout << "[-] Node " << key << " deleted." << endl;
    }

    // 4. Display the list
    void display() {
        if (head == nullptr) {
            cout << "List is empty." << endl;
            return;
        }
        Node* temp = head;
        cout << "Linked List: ";
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }

    // Destructor to prevent memory leaks on exit
    ~LinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }
};

int main() {
    LinkedList list;

    // Demonstrate Operations
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtEnd(30);
    list.insertAtEnd(40);
    
    list.display();

    list.deleteNode(20); // Delete Head
    list.deleteNode(30); // Delete Middle

    list.display();

    return 0;
}
