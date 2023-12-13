
#include <iostream>
#include <vector>
#include <iomanip>
#include <string>
using namespace std;
struct Task {
    string description;
    bool completed;
};

// Function prototypes
void displayMenu();
void addTask(vector<Task>& tasks);
void viewTasks(const vector<Task>& tasks);
void markAsCompleted(vector<Task>& tasks);
void removeTask(vector<Task>& tasks);

int main() {
    vector<Task> tasks;

    int choice;
    do {
        displayMenu();
        cout << "Enter your choice (1-5): ";
        cin >> choice;

        switch (choice) {
        case 1:
            addTask(tasks);
            break;
        case 2:
            viewTasks(tasks);
            break;
        case 3:
            markAsCompleted(tasks);
            break;
        case 4:
            removeTask(tasks);
            break;
        case 5:
            std::cout << "Exiting the program. Goodbye!\n";
            break;
        default:
            std::cout << "Invalid choice. Please enter a number between 1 and 5.\n";
        }

    } while (choice != 5);

    return 0;
}

void displayMenu() {
    cout << "\n== To-Do List Manager ==\n";
    cout << "1. Add Task\n";
    cout << "2. View Tasks\n";
    cout << "3. Mark Task as Completed\n";
    cout << "4. Remove Task\n";
    cout << "5. Exit\n";
}

void addTask(vector<Task>& tasks) {
    Task newTask;
    cout << "Enter the description of the task: ";
    cin.ignore();
    getline(cin, newTask.description);
    newTask.completed = false;
    tasks.push_back(newTask);
    cout << "Task added successfully!\n";
}

void viewTasks(const vector<Task>& tasks) {
    cout << "\n=== Task List ===\n";
    cout << left << setw(4) << "ID" << setw(30) << "Description" << "Status\n";
    for (size_t i = 0; i < tasks.size(); ++i) {
        cout << left << setw(4) << i + 1 << setw(30) << tasks[i].description;
        if (tasks[i].completed) {
            cout << "Completed\n";
        }
        else {
            cout << "Pending\n";
        }
    }
}

void markAsCompleted(vector<Task>& tasks) {
    viewTasks(tasks);
    int taskId;
    cout << "Enter the ID of the task to mark as completed: ";
    cin >> taskId;

    if (taskId > 0 && static_cast<size_t>(taskId) <= tasks.size()) {
        tasks[taskId - 1].completed = true;
        cout << "Task marked as completed!\n";
    }
    else {
        cout << "Invalid task ID. No task marked as completed.\n";
    }
}

void removeTask(vector<Task>& tasks) {
    viewTasks(tasks);
    int taskId;
    cout << "Enter the ID of the task to remove: ";
    cin >> taskId;
    if (taskId > 0 && static_cast<size_t>(taskId) <= tasks.size()) {
        tasks.erase(tasks.begin() + taskId - 1);
        cout << "Task removed successfully!\n";
    }
    else {
        cout << "Invalid task ID. No task removed.\n";
    }
}
