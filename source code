#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define a structure for employee data
typedef struct {
    char name[50];
    int emp_id;
    float salary;
    char job_title[50];
} Employee;

// Function to add a new employee to the system
void add_employee(Employee *employees, int *num_employees) {
    // Prompt user to enter employee data
    printf("Enter employee name: ");
    scanf("%s", employees[*num_employees].name);

    printf("Enter employee ID: ");
    scanf("%d", &employees[*num_employees].emp_id);

    printf("Enter employee salary: ");
    scanf("%f", &employees[*num_employees].salary);

    printf("Enter employee job title: ");
    scanf("%s", employees[*num_employees].job_title);

    // Increment the number of employees
    *num_employees += 1;
}

// Function to save employee data to a CSV file
void save_data(Employee *employees, int num_employees) {
    FILE *file = fopen("employees.csv", "w");
    if (file == NULL) {
        printf("Error opening file.\n");
        return;
    }

    fprintf(file, "Name,Employee ID,Salary,Job Title\n");
    for (int i = 0; i < num_employees; i++) {
        fprintf(file, "%s,%d,%.2f,%s\n", employees[i].name, employees[i].emp_id, employees[i].salary, employees[i].job_title);
    }

    fclose(file);
    printf("Data saved to employees.csv.\n");
}

// Function to load employee data from a CSV file
void load_data(Employee *employees, int *num_employees) {
    FILE *file = fopen("employees.csv", "r");
    if (file == NULL) {
        printf("Error opening file.\n");
        return;
    }

    // Skip the header line
    char line[200];
    fgets(line, sizeof(line), file);

    while (fgets(line, sizeof(line), file) != NULL) {
        char *token;
        token = strtok(line, ",");
        
        strcpy(employees[*num_employees].name, token);

        token = strtok(NULL, ",");
        employees[*num_employees].emp_id = atoi(token);

        token = strtok(NULL, ",");
        employees[*num_employees].salary = atof(token);

        token = strtok(NULL, ",");
        strcpy(employees[*num_employees].job_title, token);

        (*num_employees)++;
    }

    fclose(file);
    printf("Data loaded from employees.csv.\n");
}

// Function to display all employees in the system
void display_employees(Employee *employees, int num_employees) {
    printf("\n%-20s%-10s%-10s%s\n", "Name", "ID", "Salary", "Job Title");
    for (int i = 0; i < num_employees; i++) {
        printf("%-20s%-10d%-10.2f%s\n", employees[i].name, employees[i].emp_id, employees[i].salary, employees[i].job_title);
    }
}

// Function to search for an employee by name
void search_employee(Employee *employees, int num_employees) {
    char search_name[50];
    printf("Enter name to search for: ");
    scanf("%s", search_name);

    for (int i = 0; i < num_employees; i++) {
        if (strcmp(search_name, employees[i].name) == 0) {
            printf("\n%-20s%-10s%-10s%s\n", "Name", "ID", "Salary", "Job Title");
            printf("%-20s%-10d%-10.2f%s\n", employees[i].name, employees[i].emp_id, employees[i].salary, employees[i].job_title);
            return;
        }
    }

    printf("Employee not found.\n");
}

int main() {
    Employee employees[50];  // Define an array of employees
    int num_employees = 0;   // Initialize the number of employees to zero
    int choice;

    do {
        // Display menu options
        printf("\n1. Add employee\n");
        printf("2. Display employees\n");
        printf("3. Search for employee\n");
        printf("4. Save data to CSV file\n");
        printf("5. Load data from CSV file\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        // Process user choice
        switch(choice) {
            case 1:
                add_employee(employees, &num_employees);
                break;
            case 2:
                display_employees(employees, num_employees);
                break;
            case 3:
                search_employee(employees, num_employees);
                break;
            case 4:
                save_data(employees, num_employees);
                break;
            case 5:
                load_data(employees, &num_employees);
                break;
            case 6:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (1);

    return 0;
}
