University Management System – Java Swing

A desktop-based University Management System built using Java and Swing, designed as part of a summer training project on Fundamentals of Data Structures.
The system helps manage students, faculty members, and courses, including automatic waiting-list handling when a course reaches full capacity.

📌 Features
🎓 Student Management

Add new students

Enroll students into courses

Automatic transfer to the waiting list if the course is full

👨‍🏫 Faculty Management

Add faculty members

Assign faculty to specific courses

📚 Course Management

Create new courses with capacity limits

Assign faculty

Track enrolled students and waiting lists

View course details anytime

🧠 Smart Enrollment

If enrolled < capacity → Student is added

If capacity full → Student goes to waiting list automatically

🛠️ Technologies Used

Java (JDK 8+) – Main programming language

Java Swing – UI development

Java Collections Framework –

ArrayList → Students & faculty storage

HashMap → Course mapping

Queue (LinkedList) → Waiting list

📂 Project Structure
src/
 └── uniman.java
      ├── Student Class
      ├── Faculty Class
      ├── Course Class
      ├── GUI (Swing-based)
      └── Main Method

⚙️ How to Run

Install JDK 8 or later

Open the project in Eclipse / IntelliJ / NetBeans

Compile and run:

javac uniman.java
java uniman


The GUI will launch with buttons for:

Add Student

Add Faculty

Create Course

Assign Faculty

Enroll Student

View Course Details

📘 User Guide
1️⃣ Add Student

Enter Student ID and Name → Click Add Student

2️⃣ Add Faculty

Enter Faculty ID and Name → Click Add Faculty

3️⃣ Create Course

Enter Course Code, Title, and Capacity

4️⃣ Assign Faculty

Enter Course Code & Faculty ID → Faculty is assigned

5️⃣ Enroll Student

Enter Course Code & Student ID →
System automatically decides enrolled/waiting list

6️⃣ View Course Details

Displays:

Course title & code

Faculty assigned

Enrolled student list

Waiting list

📈 Project Status

✔ Fully functional for basic operations
✔ Handles waiting list logic correctly
✖ Does not use a database (data is lost on exit)
➡ Can be extended with MySQL / SQLite in future

📄 Future Improvements

Add database for permanent storage

Add login system (Admin / Faculty / Student views)

Export reports as PDF

Modern GUI using JavaFX

REST API integration

📚 References

Oracle Official Java Documentation

TutorialsPoint – Java Swing

GeeksforGeeks – Java Collections
