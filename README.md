# ============================================================
# Student Information Management System
# PHINMA Cagayan de Oro College
# Using List (Array) + for loop only
# ============================================================

# students list format:
# [id, name, age, gender, date_of_birth, year_level, section, address, contact, email, parent_name, parent_contact, parent_address]

students = []

# users list format:
# [id, role, name, assigned_section]
# assigned_section is only for teacher, others will have "None"

users = []

def print_header(title):
    print("\n" + "=" * 60)
    print(title.center(60))
    print("=" * 60)

def print_line():
    print("-" * 60)

# -------------------- SAMPLE DATA --------------------
def load_sample_data():
    # Registrar
    users.append(["R001", "registrar", "Maria Santos", "None"])

    # Students
    users.append(["S001", "student", "Juan Dela Cruz", "None"])
    users.append(["S002", "student", "Ana Reyes", "None"])
    users.append(["S003", "student", "Pedro Santos", "None"])

    # Teachers (no section yet)
    users.append(["T001", "teacher", "Mr. Lopez", "None"])
    users.append(["T002", "teacher", "Ms. Garcia", "None"])

    # Student Records
    students.append(["S001", "Juan Dela Cruz", "18", "Male", "2007-05-12", "1st Year", "BSIT-1A",
                     "Cagayan de Oro City", "09171234567", "juan@phinma.edu.ph",
                     "Roberto Dela Cruz", "09189876543", "Cagayan de Oro City"])

    students.append(["S002", "Ana Reyes", "19", "Female", "2006-11-03", "1st Year", "BSIT-1A",
                     "Carmen, CDO", "09181234567", "ana@phinma.edu.ph",
                     "Elena Reyes", "09187654321", "Carmen, CDO"])

    students.append(["S003", "Pedro Santos", "18", "Male", "2007-02-20", "1st Year", "BSIT-1B",
                     "Iponan, CDO", "09191234567", "pedro@phinma.edu.ph",
                     "Luis Santos", "09195556677", "Iponan, CDO"])
James
# -------------------- REGISTRAR FUNCTIONS --------------------
def enroll_student():
    print_header("ENROLL NEW STUDENT")
    sid = input("Enter Student ID (ex: S004): ").upper()

    # Check if ID already exists using loop
    for i in range(len(students)):
        if students[i][0] == sid:
            print("\n[!] Error: Student ID already exists.")
            return
    for i in range(len(users)):
        if users[i][0] == sid:
            print("\n[!] Error: Student ID already exists.")
            return

    name = input("Enter Full Name: ")
    age = input("Enter Age: ")
    gender = input("Enter Gender: ")
    date_of_birth = input("Enter Date of Birth (ex: 2007-05-12): ")
    year_level = input("Enter Year Level (ex: 1st Year): ")
    section = input("Enter Section (ex: BSIT-1A): ").upper()
    address = input("Enter Address: ")
    contact = input("Enter Contact Number: ")
    email = input("Enter Email Address: ")
    parent_name = input("Enter Parents/Guardian Name: ")
    parent_contact = input("Enter Parents/Guardian Contact Number: ")
    parent_address = input("Enter Parents/Guardian Home Address: ")

    # Add to students list (array)
    students.append([sid, name, age, gender, date_of_birth, year_level, section,
                     address, contact, email, parent_name, parent_contact, parent_address])

    # Add to users list
    users.append([sid, "student", name, "None"])

    print("\n[+] Student " + sid + " successfully enrolled!")

def view_all_students():
    print_header("ALL STUDENT RECORDS")
    if len(students) == 0:
        print("No student records found.")
        return

    for i in range(len(students)):
        s = students[i]
        print("\nStudent ID       : " + s[0])
        print("Full Name        : " + s[1])
        print("Age              : " + s[2])
        print("Gender           : " + s[3])
        print("Date of Birth    : " + s[4])
        print("Year Level       : " + s[5])
        print("Section          : " + s[6])
        print("Address          : " + s[7])
        print("Contact          : " + s[8])
        print("Email            : " + s[9])
        print("Parent Name      : " + s[10])
        print("Parent Contact   : " + s[11])
        print("Parent Address   : " + s[12])
        print_line()

def search_student():
    print_header("SEARCH STUDENT")
    keyword = input("Enter Student ID or Name: ").upper()

    found = False
    for i in range(len(students)):
        s = students[i]
        if keyword == s[0] or keyword in s[1].upper():
            print("\nStudent ID       : " + s[0])
            print("Full Name        : " + s[1])
            print("Age              : " + s[2])
            print("Gender           : " + s[3])
            print("Date of Birth    : " + s[4])
            print("Year Level       : " + s[5])
            print("Section          : " + s[6])
            print("Address          : " + s[7])
            print("Contact          : " + s[8])
            print("Email            : " + s[9])
            print("Parent Name      : " + s[10])
            print("Parent Contact   : " + s[11])
            print("Parent Address   : " + s[12])
            print_line()
            found = True

    if not found:
        print("\n[!] No matching student found.")

def update_student():
    print_header("UPDATE STUDENT RECORD")
    sid = input("Enter Student ID to update: ").upper()

    index = find_student_index(sid)
    if index == -1:
        print("\n[!] Student ID not found.")
        return

    s = students[index]
    print("\nLeave blank if you do not want to change the information.")

    name = input("Full Name [" + s[1] + "]: ")
    age = input("Age [" + s[2] + "]: ")
    gender = input("Gender [" + s[3] + "]: ")
    date_of_birth = input("Date of Birth [" + s[4] + "]: ")
    year_level = input("Year Level [" + s[5] + "]: ")
    section = input("Section [" + s[6] + "]: ")
    address = input("Address [" + s[7] + "]: ")
    contact = input("Contact [" + s[8] + "]: ")
    email = input("Email [" + s[9] + "]: ")
    parent_name = input("Parent Name [" + s[10] + "]: ")
    parent_contact = input("Parent Contact [" + s[11] + "]: ")
    parent_address = input("Parent Address [" + s[12] + "]: ")
James
if name != "":
        students[index][1] = name
        # also update name in users
        u_index = find_user_index(sid)
        if u_index != -1:
            users[u_index][2] = name
    if age != "":
        students[index][2] = age
    if gender != "":
        students[index][3] = gender
    if date_of_birth != "":
        students[index][4] = date_of_birth
    if year_level != "":
        students[index][5] = year_level
    if section != "":
        students[index][6] = section.upper()
    if address != "":
        students[index][7] = address
    if contact != "":
        students[index][8] = contact
    if email != "":
        students[index][9] = email
    if parent_name != "":
        students[index][10] = parent_name
    if parent_contact != "":
        students[index][11] = parent_contact
    if parent_address != "":
        students[index][12] = parent_address

    print("\n[+] Student record updated successfully!")

def delete_student():
    print_header("DELETE STUDENT RECORD")
    sid = input("Enter Student ID to delete: ").upper()

    index = find_student_index(sid)
    if index == -1:
        print("\n[!] Student ID not found.")
        return

    confirm = input("Are you sure you want to delete " + sid + "? (Y/N): ").upper()
    if confirm == "Y":
        # Remove from students list
        students.pop(index)

        # Remove from users list
        u_index = find_user_index(sid)
        if u_index != -1:
            users.pop(u_index)

        print("\n[+] Student record deleted successfully!")
    else:
        print("\n[!] Deletion cancelled.")

def assign_section_to_teacher():
    print_header("ASSIGN SECTION TO TEACHER")

    # Show available sections using loop
    print("Available Sections in the system:")
    print_line()
    sections = []
    for i in range(len(students)):
        sec = students[i][6]
        if sec not in sections:
            sections.append(sec)
            print(" - " + sec)

    if len(sections) == 0:
        print("No sections found. Please enroll students first.")
        return

    print_line()

    # Show all teachers using loop
    print("List of Teachers:")
    print_line()
    for i in range(len(users)):
        if users[i][1] == "teacher":
            print("Teacher ID     : " + users[i][0])
            print("Name           : " + users[i][2])
            print("Current Section: " + users[i][3])
            print_line()

    teacher_id = input("Enter Teacher ID to assign section: ").upper()

    t_index = find_user_index(teacher_id)
    if t_index == -1 or users[t_index][1] != "teacher":
        print("\n[!] Teacher ID not found.")
        return

    new_section = input("Enter Section to assign (copy from available sections above): ").upper().strip()

    if new_section == "":
        print("\n[!] Section cannot be empty.")
        return

    users[t_index][3] = new_section

    print("\n[+] SUCCESS!")
    print("Teacher     : " + users[t_index][2])
    print("Assigned to : " + new_section)

def registrar_menu():
    while True:
        print_header("REGISTRAR MENU")
        print("1. Enroll New Student")
        print("2. View All Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Assign Section to Teacher")
        print("7. Logout")
        choice = input("\nEnter choice: ")

        if choice == "1":
            enroll_student()
        elif choice == "2":
            view_all_students()
        elif choice == "3":
            search_student()
        elif choice == "4":
            update_student()
        elif choice == "5":
            delete_student()
        elif choice == "6":
            assign_section_to_teacher()
        elif choice == "7":
            print("\n[+] Logging out...")
            break
        else:
            print("\n[!] Invalid choice.")

        input("\nPress Enter to continue...")
