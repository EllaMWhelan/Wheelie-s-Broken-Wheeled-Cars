# GPA Calculator

def letter_to_gpa(grade):
    """Converts a letter grade to the GPA value."""
    grade_scale = {
        'A': 4.0, 'A-': 3.7, 'B+': 3.3, 'B': 3.0, 'B-': 2.7,
        'C+': 2.3, 'C': 2.0, 'C-': 1.7, 'D+': 1.3, 'D': 1.0, 'F': 0.0
    }
    return grade_scale.get(grade.upper(), None)  # Returns None if grade is invalid

def calculate_gpa(grades, credit_hours):
    """Calculates GPA given a list of grades and their corresponding credit hours."""
    total_points = 0
    total_credits = 0
    
    for i in range(len(grades)):
        gpa_value = letter_to_gpa(grades[i])
        if gpa_value is not None:
            total_points += gpa_value * credit_hours[i]
            total_credits += credit_hours[i]
        else:
            print(f"Invalid grade entered: {grades[i]}")
            return None
    
    if total_credits == 0:
        return 0.0
    
    return total_points / total_credits

def main():
    grades = []
    credit_hours = []
    
    print("Welcome to the GPA calculator!")
    
    while True:
        grade = input("Enter the letter grade for the course (or type 'done' to finish): ").strip()
        if grade.lower() == 'done':
            break
        try:
            credits = float(input(f"Enter the credit hours for the course with grade {grade}: "))
            grades.append(grade)
            credit_hours.append(credits)
        except ValueError:
            print("Invalid input. Please enter numeric values for credit hours.")
    
    if grades and credit_hours:
        gpa = calculate_gpa(grades, credit_hours)
        if gpa is not None:
            print(f"Your GPA is: {gpa:.2f}")
    else:
        print("No courses entered.")

if __name__ == "__main__":
    main()
