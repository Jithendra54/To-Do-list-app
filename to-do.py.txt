# todo.py

import os

# The name of the file where tasks are stored
TASKS_FILE = "tasks.txt"

def show_menu():
    """Displays the main menu to the user."""
    print("\n--- To-Do List Menu ---")
    print("1. View tasks")
    print("2. Add a new task")
    print("3. Mark a task as complete")
    print("4. Exit")
    print("-----------------------")

def load_tasks():
    """Loads tasks from the tasks.txt file."""
    if not os.path.exists(TASKS_FILE):
        return []  # Return an empty list if the file doesn't exist
    with open(TASKS_FILE, "r") as f:
        tasks = f.readlines()
    # Strip newline characters from each task
    return [task.strip() for task in tasks]

def save_tasks(tasks):
    """Saves the list of tasks to the tasks.txt file."""
    with open(TASKS_FILE, "w") as f:
        for task in tasks:
            f.write(task + "\n")

def view_tasks(tasks):
    """Displays all current tasks."""
    print("\n--- Your Tasks ---")
    if not tasks:
        print("You have no tasks. Great job!")
    else:
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task}")
    print("------------------")

def add_task(tasks):
    """Adds a new task to the list."""
    new_task = input("Enter the new task: ")
    tasks.append(new_task)
    save_tasks(tasks)
    print(f"✅ Task '{new_task}' added successfully!")

def complete_task(tasks):
    """Marks a task as complete by removing it from the list."""
    view_tasks(tasks)
    if not tasks:
        return # Nothing to complete

    try:
        task_num = int(input("Enter the number of the task to mark as complete: "))
        if 1 <= task_num <= len(tasks):
            removed_task = tasks.pop(task_num - 1)
            save_tasks(tasks)
            print(f"🎉 Task '{removed_task}' marked as complete!")
        else:
            print("❌ Invalid task number. Please try again.")
    except ValueError:
        print("❌ Invalid input. Please enter a number.")

def main():
    """The main function to run the application."""
    tasks = load_tasks()
    while True:
        show_menu()
        choice = input("Enter your choice (1-4): ")
        if choice == '1':
            view_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            complete_task(tasks)
        elif choice == '4':
            print("Goodbye! 👋")
            break
        else:
            print("❌ Invalid choice. Please enter a number between 1 and 4.")

if __name__ == "__main__":
    main()