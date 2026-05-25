# =========================================================
# STUDENT GRADE CALCULATOR
# =========================================================

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
# FUNCTION: COMMENT
# =========================================================

def get_comment(grade):

    if grade == "A":
        return "Excellent!"

    elif grade == "B":
        return "Very Good!"

    elif grade == "C":
        return "Good"

    elif grade == "D":
        return "Needs Improvement"

    else:
        return "Failed"


# =========================================================
# FUNCTION: VALID INPUT
# =========================================================

def get_marks(subject):

    while True:

        try:

            marks = float(input(f"Enter marks for {subject} (0-100): "))

            if 0 <= marks <= 100:
                return marks

            else:
                print("Marks must be between 0 and 100.")

        except ValueError:
            print("Invalid input! Enter numbers only.")


# =========================================================
# MAIN PROGRAM
# =========================================================

print("=" * 55)
print("          STUDENT GRADE CALCULATOR")
print("=" * 55)

# =========================================================
# NUMBER OF STUDENTS
# =========================================================

while True:

    try:

        total_students = int(input("Enter number of students: "))

        if total_students > 0:
            break

        else:
            print("Please enter a positive number.")

    except ValueError:
        print("Invalid input! Enter whole number.")


# =========================================================
# INPUT STUDENT DATA
# =========================================================

for i in range(total_students):

    print("\n" + "=" * 30)
    print(f"         STUDENT {i+1}")
    print("=" * 30)

    # Student Name
    while True:

        name = input("Enter student name: ").strip()

        if name != "":
            break

        else:
            print("Name cannot be empty.")

    # Subject Marks
    math = get_marks("Math")
    science = get_marks("Science")
    english = get_marks("English")

    # Average
    average = (math + science + english) / 3

    # Grade
    grade = calculate_grade(average)

    # Comment
    comment = get_comment(grade)

    # Store Data
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


# =========================================================
# DISPLAY RESULTS
# =========================================================

print("\n" + "=" * 90)
print(" " * 30 + "RESULT SUMMARY")
print("=" * 90)

print(
    f"{'Name':<18}"
    f"{'Math':<10}"
    f"{'Science':<10}"
    f"{'English':<10}"
    f"{'Average':<10}"
    f"{'Grade':<10}"
    f"Comment"
)

print("-" * 90)

for student in students:

    print(
        f"{student['name']:<18}"
        f"{student['math']:<10.1f}"
        f"{student['science']:<10.1f}"
        f"{student['english']:<10.1f}"
        f"{student['average']:<10.1f}"
        f"{student['grade']:<10}"
        f"{student['comment']}"
    )


# =========================================================
# CLASS STATISTICS
# =========================================================

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
print("              CLASS STATISTICS")
print("=" * 50)

print(f"Total Students : {len(students)}")
print(f"Class Average  : {class_average:.2f}")
print(f"Highest Marks  : {highest:.2f} ({topper})")
print(f"Lowest Marks   : {lowest:.2f} ({lowest_student})")


# =========================================================
# SEARCH STUDENT
# =========================================================

search = input("\nEnter student name to search: ").lower()

found = False

for student in students:

    if student["name"].lower() == search:

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
# SAVE FILE
# =========================================================

choice = input("\nDo you want to save results to file? (yes/no): ")

if choice.lower() == "yes":

    with open("student_results.txt", "w") as file:

        file.write("STUDENT GRADE REPORT\n")
        file.write("=" * 50 + "\n")

        for student in students:

            file.write(f"Name      : {student['name']}\n")
            file.write(f"Average   : {student['average']:.2f}\n")
            file.write(f"Grade     : {student['grade']}\n")
            file.write(f"Comment   : {student['comment']}\n")
            file.write("-" * 50 + "\n")

    print("Results saved successfully!")

print("\nThank you for using the Grade Calculator!")
print("=" * 55)
