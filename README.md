

# Maze Solver
from collections import deque
def bfs(graph, start, end):
    """
    Breadth-First Search (BFS) algorithm to find the shortest path
    from the start node to the end node.
    """
    queue = deque([(start, [start])])
    visited = set()
    while queue:
        node, path = queue.popleft()
        if node == end:
            return path
        if node not in visited:
            visited.add(node)
            for neighbor in graph[node]:
                queue.append((neighbor, path + [neighbor]))
    return []
def solve_maze(maze_graph, start_node, end_node):
    """
    Solve the maze by finding a path from the start node to the end node
    using BFS graph traversal algorithm.
    """
    return bfs(maze_graph, start_node, end_node)
# Example usage
maze_graph = {
    1: [2],
    2: [1, 3, 4],
    3: [2, 7],
    4: [2, 5, 6],
    5: [4, 9],
    6: [4, 7],
    7: [3, 6, 8],
    8: [7, 9],
    9: [5, 8, 10],
    10: [9]
}
start_node = 1
end_node = 10
path = solve_maze(maze_graph, start_node, end_node)
print(f"Path from {start_node} to {end_node}: {path}")

remove comments

#Employment Managemnt System
class Employee:
    def __init__(self, name, position, department, salary, supervisor=None):
        self.name = name
        self.position = position
        self.department = department
        self.salary = salary
        self.supervisor = supervisor
        self.subordinates = []

    def add_subordinate(self, employee):
        self.subordinates.append(employee)

    def remove_subordinate(self, employee):
        self.subordinates.remove(employee)

    def promote(self, new_position, new_salary):
        self.position = new_position
        self.salary = new_salary

    def demote(self, new_position, new_salary):
        self.position = new_position
        self.salary = new_salary

    def change_department(self, new_department):
        self.department = new_department


class Department:
    def __init__(self, name, budget):
        self.name = name
        self.budget = budget
        self.employees = []

    def add_employee(self, employee):
        self.employees.append(employee)
        employee.department = self

    def remove_employee(self, employee):
        self.employees.remove(employee)
        employee.department = None

    def manage_budget(self, new_budget):
        self.budget = new_budget


class EmployeeManagementSystem:
    def __init__(self):
        self.employees = []
        self.departments = []

    def add_employee(self, name, position, department, salary, supervisor=None):
        employee = Employee(name, position, department, salary, supervisor)
        self.employees.append(employee)
        if supervisor:
            supervisor.add_subordinate(employee)

    def remove_employee(self, employee):
        self.employees.remove(employee)
        if employee.supervisor:
            employee.supervisor.remove_subordinate(employee)
        for subordinate in employee.subordinates:
            subordinate.supervisor = None

    def update_employee(self, employee, **kwargs):
        if "name" in kwargs:
            employee.name = kwargs["name"]
        if "position" in kwargs:
            employee.position = kwargs["position"]
        if "department" in kwargs:
            employee.change_department(kwargs["department"])
        if "salary" in kwargs:
            employee.salary = kwargs["salary"]

    def create_department(self, name, budget):
        department = Department(name, budget)
        self.departments.append(department)

    def assign_employee_to_department(self, employee, department):
        department.add_employee(employee)

    def manage_department_budget(self, department, new_budget):
        department.manage_budget(new_budget)

    def track_employee_performance(self, employee):
        # Implement performance tracking logic
        pass

    def generate_performance_reports(self):
        # Implement report generation logic
        pass

    def identify_top_performers(self):
        # Implement logic to identify top performers
        pass

    def change_credentials(self):
        # Implement credential management logic
        pass

    def log_out(self):
        # Implement log out logic
        pass

    def main_menu(self):
        while True:
            print("Main Menu:")
            print("1. Employee Management")
            print("2. Department Management")
            print("3. Performance Tracking")
            print("4. Security Settings")
            print("5. Exit")
            choice = input("Enter your choice (1-5): ")

            if choice == "1":
                self.employee_management_menu()
            elif choice == "2":
                self.department_management_menu()
            elif choice == "3":
                self.performance_tracking_menu()
            elif choice == "4":
                self.security_settings_menu()
            elif choice == "5":
                break
            else:
                print("Invalid choice. Try again.")

    def employee_management_menu(self):
        while True:
            print("Employee Management Menu:")
            print("1. Add Employee")
            print("2. Remove Employee")
            print("3. Update Employee Information")
            print("4. Change Department")
            print("5. Promote Employee")
            print("6. Demote Employee")
            print("7. Back to Main Menu")
            choice = input("Enter your choice (1-7): ")

            if choice == "1":
                self.add_employee_menu()
            elif choice == "2":
                self.remove_employee_menu()
            elif choice == "3":
                self.update_employee_menu()
            elif choice == "4":
                self.change_department_menu()
            elif choice == "5":
                self.promote_employee_menu()
            elif choice == "6":
                self.demote_employee_menu()
            elif choice == "7":
                break
            else:
                print("Invalid choice. Try again.")

    def department_management_menu(self):
        while True:
            print("Department Management Menu:")
            print("1. Create Department")
            print("2. Assign Employee to Department")
            print("3. Manage Department Budget")
            print("4. Back to Main Menu")
            choice = input("Enter your choice (1-4): ")

            if choice == "1":
                self.create_department_menu()
            elif choice == "2":
                self.assign_employee_to_department_menu()
            elif choice == "3":
                self.manage_department_budget_menu()
            elif choice == "4":
                break
            else:
                print("Invalid choice. Try again.")

    def performance_tracking_menu(self):
        while True:
            print("Performance Tracking Menu:")
            print("1. Track Employee Performance")
            print("2. Generate Performance Reports")
            print("3. Identify Top Performers")
            print("4. Back to Main Menu")
            choice = input("Enter your choice (1-4): ")

            if choice == "1":
                self.track_employee_performance_menu()
            elif choice == "2":
                self.generate_performance_reports_menu()
            elif choice == "3":
                self.identify_top_performers_menu()
            elif choice == "4":
                break
            else:
                print("Invalid choice. Try again.")

    def security_settings_menu(self):
        while True:
            print("Security Settings Menu:")
            print("1. Change Credentials")
            print("2. Log Out")
            choice = input("Enter your choice (1-2): ")

            if choice == "1":
                self.change_credentials()
            elif choice == "2":
                self.log_out()
                break
            else:
                print("Invalid choice. Try again.")

    # Additional menu methods for specific operations
    def add_employee_menu(self):
        # Implement logic to add a new employee
        pass

    def remove_employee_menu(self):
        # Implement logic to remove an employee
        pass

    def update_employee_menu(self):
        # Implement logic to update employee information
        pass

    def change_department_menu(self):
        # Implement logic to change an employee's department
        pass

    def promote_employee_menu(self):
        # Implement logic to promote an employee
        pass

    def demote_employee_menu(self):
        # Implement logic to demote an employee
        pass

    def create_department_menu(self):
        # Implement logic to create a new department
        pass

    def assign_employee_to_department_menu(self):
        # Implement logic to assign an employee to a department
        pass

    def manage_department_budget_menu(self):
        # Implement logic to manage a department's budget
        pass

    def track_employee_performance_menu(self):
        # Implement logic to track an employee's performance
        pass

    def generate_performance_reports_menu(self):
        # Implement logic to generate performance reports
        pass

    def identify_top_performers_menu(self):
        # Implement logic to identify top performers
        pass


# Run the Employee Management System
ems = EmployeeManagementSystem()
ems.main_menu()
