//Functions_Challenge_2

#include <iostream>
#include <limits>
#include <iomanip>

// --- Function Prototypes ---
void inputGrades(double& g1, double& g2, double& g3);
double calculateAverage(const double g1, const double g2, const double g3);
char getLetterGrade(const double average);
double validateGradeInput(int gradeNum);

int main() {
    // Variables to hold the student's grades
    double grade1 = 0.0, grade2 = 0.0, grade3 = 0.0;
    int choice;
    bool gradesEntered = false;

    do {
        std::cout << "   STUDENT GRADE MANAGER\n";
        std::cout << "1. Input Grades\n";
        std::cout << "2. Calculate and Display Average\n";
        std::cout << "3. Assign and Display Letter Grade\n";
        std::cout << "4. Quit\n";
        std::cout << "Selection: ";

        // Menu Choice Validation
        if (!(std::cin >> choice)) {
            std::cout << "Please enter a number (1-4).\n";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            continue;
        }

        switch (choice) {
            case 1:
                inputGrades(grade1, grade2, grade3);
                gradesEntered = true;
                break;

            case 2:
                if (gradesEntered) {
                    double avg = calculateAverage(grade1, grade2, grade3);
                    std::cout << std::fixed << std::setprecision(2);
                    std::cout << "\nThe average of " << grade1 << ", " << grade2 
                              << ", and " << grade3 << " is: " << avg << "\n";
                } else {
                    std::cout << "Error: Please input grades first (Option 1).\n";
                }
                break;

            case 3:
                if (gradesEntered) {
                    double avg = calculateAverage(grade1, grade2, grade3);
                    char letter = getLetterGrade(avg);
                    std::cout << "\nBased on the average of " << avg 
                              << ", the Letter Grade is: " << letter << "\n";
                } else {
                    std::cout << "Error: Please input grades first (Option 1).\n";
                }
                break;

            case 4:
                std::cout << "Exiting have a nice day!\n";
                break;

            default:
                std::cout << "Invalid selection. Please try again.\n";
        }
    } while (choice != 4);

    return 0;
}


void inputGrades(double& g1, double& g2, double& g3) {
    std::cout << "\n--- Enter Student Grades ---\n";
    g1 = validateGradeInput(1);
    g2 = validateGradeInput(2);
    g3 = validateGradeInput(3);
    std::cout << "Grades successfully recorded.\n";
}

 // Calculates average using pass-by-value. 
double calculateAverage(const double g1, const double g2, const double g3) {
    return (g1 + g2 + g3) / 3.0;
}


//Determines letter grade based on a standard 10-point scale.
char getLetterGrade(const double average) {
    if (average >= 90.0) return 'A';
    if (average >= 80.0) return 'B';
    if (average >= 70.0) return 'C';
    if (average >= 60.0) return 'D';
    return 'F';
}


//Helper function to ensure user inputs valid numbers between 0-100.
double validateGradeInput(int gradeNum) {
    double input;
    while (true) {
        std::cout << "Enter grade #" << gradeNum << " (0-100): ";
        if (std::cin >> input && input >= 0 && input <= 100) {
            return input;
        } else {
            std::cout << "Invalid enter a number between 0-100.\n";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        }
    }
}
