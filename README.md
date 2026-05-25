# week2-grade-calculator-
# =========================================================
# STUDENT GRADE CALCULATOR
# Week 2 Project - Control Flow & Data Structures
# Created By: Your Name
# =========================================================

# =======================
# ANSI COLOR CODES
# =======================

GREEN = "\033[92m"
YELLOW = "\033[93m"
RED = "\033[91m"
BLUE = "\033[94m"
RESET = "\033[0m"

# =======================
# GLOBAL LIST
# =======================

students = []


# =========================================================
# FUNCTION: CALCULATE GRADE
# =========================================================

def calculate_grade(avg):

    if avg >= 90:
        return "A"

    elif avg >= 80:
        return "B"

    elif avg >= 70:
        return "C"

    elif avg >= 60:
        return "D"

    else:
        return "F"


# =========================================================
# FUNCTION: GET COMMENT
# =========================================================

def get_comment(grade):

    if grade == "A":
        return "Excellent Performance!"

    elif grade == "B":
        return "Very Good Work!"

    elif grade == "C":
        return "Good. Keep Improving."

    elif grade == "D":
        return "Needs More Practice."

    else:
        return "Failed. Please seek help."


# =========================================================
# FUNCTION: GET COLOR
# =========================================================

def get_color(grade):

    if grade == "A":
        return GREEN

    elif grade == "B":
        return BLUE

    elif grade == "C":
        return YELLOW

    else:
        return RED


# =========================================================
# FUNCTION: VALIDATE MARKS INPUT
# =========================================================

def get_valid_marks(subject):

    while True:

        try:

            marks = float(input(f"Enter marks for {subject} (0-100): "))

            if 0 <= marks <= 100:
                return marks

            else:
                print("Marks must be between 0 and 100.")

        except ValueError:
            print("Invalid input! Please enter numeric value.")


# =========================================================
# FUNCTION: ADD STUDENTS
# =========================================================

def add_students():

    while True:

        try:

            total = int(input("How many students do you want to add? "))

            if total > 0:
                break

            else:
                print("Please enter a positive number.")

        except ValueError:
            print("Invalid input! Please enter a whole number.")

    for i in range(total):

        print(f"\n================ STUDENT {i+1} ================")

        # =======================
        # NAME VALIDATION
        # =======================

        while True:

            name = input("Enter student name: ").strip()

            if name != "":
                break

            else:
                print("Name cannot be empty.")

        # =======================
        # SUBJECT MARKS
        # =======================

        math = get_valid_marks("Math")
        science = get_valid_marks("Science")
        english = get_valid_marks("English")

        # =======================
        # CALCULATE AVERAGE
        # =======================

        average = (math + science + english) / 3

        # =======================
        # CALCULATE GRADE
        # =======================

        grade = calculate_grade(average)

        # =======================
        # GET COMMENT
        # =======================

        comment = get_comment(grade)

        # =======================
        # STORE STUDENT RECORD
        # =======================

        student = {
            "name": name,
            "math": math,
            "science": science,
            "english": english,
            "average": average,
            "grade": grade,
            "comment": comment
        }

        students.append(student)

    print("\nStudents added successfully!")


# =========================================================
# FUNCTION: DISPLAY RESULTS
# =========================================================

def display_results():

    if len(students) == 0:
        print("No student records found.")
        return

    print("\n" + "=" * 95)
    print(" " * 35 + "STUDENT RESULTS")
    print("=" * 95)

    print(
        f"{'Name':<18}"
        f"{'Math':<10}"
        f"{'Science':<10}"
        f"{'English':<10}"
        f"{'Average':<10}"
        f"{'Grade':<10}"
        f"Comment"
    )

    print("-" * 95)

    for student in students:

        color = get_color(student["grade"])

        print(
            f"{student['name']:<18}"
            f"{student['math']:<10.1f}"
            f"{student['science']:<10.1f}"
            f"{student['english']:<10.1f}"
            f"{student['average']:<10.1f}"
            f"{color}{student['grade']:<10}{RESET}"
            f"{student['comment']}"
        )


# =========================================================
# FUNCTION: SHOW STATISTICS
# =========================================================

def show_statistics():

    if len(students) == 0:
        print("No student records available.")
        return

    averages = []

    for student in students:
        averages.append(student["average"])

    class_average = sum(averages) / len(averages)

    highest = max(averages)
    lowest = min(averages)

    topper = ""
    lowest_student = ""

    for student in students:

        if student["average"] == highest:
            topper = student["name"]

        if student["average"] == lowest:
            lowest_student = student["name"]

    print("\n" + "=" * 50)
    print(" " * 12 + "CLASS STATISTICS")
    print("=" * 50)

    print(f"Total Students : {len(students)}")
    print(f"Class Average  : {class_average:.2f}")
    print(f"Highest Marks  : {highest:.2f} ({topper})")
    print(f"Lowest Marks   : {lowest:.2f} ({lowest_student})")


# =========================================================
# FUNCTION: SEARCH STUDENT
# =========================================================

def search_student():

    if len(students) == 0:
        print("No records available.")
        return

    search_name = input("Enter student name to search: ").lower()

    found = False

    for student in students:

        if student["name"].lower() == search_name:

            print("\nStudent Found!")
            print("-" * 40)

            print(f"Name      : {student['name']}")
            print(f"Math      : {student['math']}")
            print(f"Science   : {student['science']}")
            print(f"English   : {student['english']}")
            print(f"Average   : {student['average']:.2f}")
            print(f"Grade     : {student['grade']}")
            print(f"Comment   : {student['comment']}")

            found = True
            break

    if not found:
        print("Student not found.")


# =========================================================
# FUNCTION: SAVE RESULTS TO FILE
# =========================================================

def save_to_file():

    if len(students) == 0:
        print("No records to save.")
        return

    try:

        file = open("student_results.txt", "w")

        file.write("STUDENT GRADE REPORT\n")
        file.write("=" * 50 + "\n")

        for student in students:

            file.write(f"Name      : {student['name']}\n")
            file.write(f"Math      : {student['math']}\n")
            file.write(f"Science   : {student['science']}\n")
            file.write(f"English   : {student['english']}\n")
            file.write(f"Average   : {student['average']:.2f}\n")
            file.write(f"Grade     : {student['grade']}\n")
            file.write(f"Comment   : {student['comment']}\n")

            file.write("-" * 50 + "\n")

        file.close()

        print("Results saved successfully in student_results.txt")

    except:
        print("Error while saving the file.")


# =========================================================
# FUNCTION: MAIN MENU
# =========================================================

def menu():

    while True:

        print("\n" + "=" * 60)
        print(" " * 15 + "STUDENT GRADE CALCULATOR")
        print("=" * 60)

        print("1. Add Student Records")
        print("2. Display Results")
        print("3. Show Statistics")
        print("4. Search Student")
        print("5. Save Results to File")
        print("6. Exit")

        choice = input("\nEnter your choice: ")

        # =======================
        # MENU OPTIONS
        # =======================

        if choice == "1":
            add_students()

        elif choice == "2":
            display_results()

        elif choice == "3":
            show_statistics()

        elif choice == "4":
            search_student()

        elif choice == "5":
            save_to_file()

        elif choice == "6":

            print("\nThank you for using the Grade Calculator!")
            print("=" * 60)

            break

        else:
            print("Invalid choice! Please try again.")


# =========================================================
# MAIN PROGRAM
# =========================================================

menu()
