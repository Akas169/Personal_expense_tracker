# Personal_expense_trackerimport os

# Function to load expenses from file
def load_expenses(filename='expenses.txt'):
    if not os.path.exists(filename):
        return []
    with open(filename, 'r') as file:
        lines = file.readlines()
        return [line.strip().split(',') for line in lines]

# Function to save expenses to file
def save_expenses(expenses, filename='expenses.txt'):
    with open(filename, 'w') as file:
        for expense in expenses:
            file.write(','.join(expense) + '\n')

# Function to display all expenses
def view_expenses(expenses):
    print("\nID | Category | Description | Amount")
    print("-------------------------------------")
    for i, expense in enumerate(expenses, start=1):
        print(f"{i}  | {expense[0]} | {expense[1]} | {expense[2]}")

# Function to add a new expense
def add_expense(expenses):
    category = input("Enter the category: ")
    description = input("Enter description: ")
    amount = input("Enter the amount: ")
    expenses.append([category, description, amount])
    save_expenses(expenses)
    print("\nExpense added successfully!")

# Function to delete an expense by ID
def delete_expense(expenses):
    view_expenses(expenses)
    expense_id = int(input("\nEnter the ID of the expense to delete: ")) - 1
    if 0 <= expense_id < len(expenses):
        expenses.pop(expense_id)
        save_expenses(expenses)
        print("\nExpense deleted successfully!")
    else:
        print("\nInvalid ID. Please try again.")

# Main function to handle the menu
def main():
    expenses = load_expenses()

    while True:
        print("\nExpense Tracker Menu")
        print("1. View Expenses")
        print("2. Add Expense")
        print("3. Delete Expense")
        print("4. Exit")

        choice = input("\nEnter your choice (1-4): ")

        if choice == '1':
            view_expenses(expenses)
        elif choice == '2':
            add_expense(expenses)
        elif choice == '3':
            delete_expense(expenses)
        elif choice == '4':
            print("\nExiting... Goodbye!")
            break
        else:
            print("\nInvalid choice. Please try again.")

if __name__ == "__main__":
    main()
