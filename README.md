#include <iostream>
using namespace std;

// Define structure for Node
struct Node {
    int data;
    Node* next;
};

// Function to insert at beginning
void insertAtBeginning(Node*& head, int value) {
    Node* newNode = new Node;   // Allocate memory
    newNode->data = value;
    newNode->next = head;
    head = newNode;
}

// Function to insert at end
void insertAtEnd(Node*& head, int value) {
    Node* newNode = new Node;   // Allocate memory
    newNode->data = value;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    Node* temp = head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
}

// Function to delete a node by value
void deleteNode(Node*& head, int value) {
    if (head == NULL) {
        cout << "List is empty.\n";
        return;
    }

    Node* temp = head;
    Node* prev = NULL;

    // If head node holds the value
    if (temp != NULL && temp->data == value) {
        head = temp->next;
        delete temp;   // Free memory
        cout << "Node deleted.\n";
        return;
    }

    // Search for the node to delete
    while (temp != NULL && temp->data != value) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) {
        cout << "Value not found.\n";
        return;
    }

    prev->next = temp->next;
    delete temp;   // Free memory
    cout << "Node deleted.\n";
}

// Function to display list
void display(Node* head) {
    if (head == NULL) {
        cout << "List is empty.\n";
        return;
    }

    Node* temp = head;
    cout << "Linked List: ";
    while (temp != NULL) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// Main function
int main() {
    Node* head = NULL;
    int choice, value;

    do {
        cout << "\n--- Singly Linked List Menu ---\n";
        cout << "1. Insert at Beginning\n";
        cout << "2. Insert at End\n";
        cout << "3. Delete a Node\n";
        cout << "4. Display List\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                insertAtBeginning(head, value);
                break;

            case 2:
                cout << "Enter value: ";
                cin >> value;
                insertAtEnd(head, value);
                break;

            case 3:
                cout << "Enter value to delete: ";
                cin >> value;
                deleteNode(head, value);
                break;

            case 4:
                display(head);
                break;

            case 5:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid choice.\n";
        }

    } while (choice != 5);

    // Free remaining memory before exit
    while (head != NULL) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}

<img width="623" height="224" alt="Screenshot 2026-02-11 095130" src="https://github.com/user-attachments/assets/3a96ae96-fda5-4086-91ff-070abc388779" />




Output
