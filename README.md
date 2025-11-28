/*1. Run the program.
2. The main window will show buttons.
3. 4. 5. 6. 7. Click Add Student or Add Faculty to add new records.
Click Create Course to make a new course.
Assign a faculty to a course using Assign Faculty.
Enroll a student in a course using Enroll Student. If the course is full, the
student will be placed in the waiting list.
Use View Course Details to see enrolled students, waiting list, and assigned
faculty.
11. Source Code*/
import javax.swing.*;
import java.awt.Component;
import java.awt.Dimension;
import java.util.*;
public class uniman {
static class Student {
String id, name;
Student(String id, String name) {
this.id = id;
this.name = name;
}
public String toString() {
return id + " - " + name;
}
}
static class Faculty {
String id, name;
Faculty(String id, String name) {
this.id = id;
this.name = name;
}
public String toString() {
return id + " - " + name;
}
}
static class Course {
String code, title;
Faculty faculty;
vii
int capacity;
List<Student> enrolled = new ArrayList<>();
Queue<Student> waitingList = new LinkedList<>();
Course(String code, String title, int capacity) {
this.code = code;
this.title = title;
this.capacity = capacity;
void assignFaculty(Faculty f) {
this.faculty = f;
}
}
boolean enroll(Student s) {
if (enrolled.size() < capacity) {
enrolled.add(s);
return true;
} else {
waitingList.add(s);
return false;
}
}
String getDetails() {
StringBuilder sb = new StringBuilder();
sb.append("Course: ").append(title).append("
(").append(code).append(")\n");
sb.append("Faculty: ").append(faculty != null ? faculty.name : "Not
Assigned").append("\n\n");
sb.append("Enrolled:\n");
for (Student s : enrolled) {
sb.append(" - ").append(s.name).append("\n");
}
sb.append("Waiting List:\n");
for (Student s : waitingList) {
sb.append(" * ").append(s.name).append("\n");
}
return sb.toString();
}
}
static List<Student> students = new ArrayList<>();
static List<Faculty> faculties = new ArrayList<>();
static Map<String, Course> courses = new HashMap<>();
public static void main(String[] args) {
SwingUtilities.invokeLater(() -> createMainGUI());
}
viii
static void createMainGUI() {
JFrame frame = new JFrame("University Management System");
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setSize(400, 400);
frame.setLayout(new BoxLayout(frame.getContentPane(),
BoxLayout.Y_AXIS));
frame.setLocationRelativeTo(null);
JButton addStudentBtn = new JButton("Add Student");
JButton addFacultyBtn = new JButton("Add Faculty");
JButton createCourseBtn = new JButton("Create Course");
JButton assignFacultyBtn = new JButton("Assign Faculty to Course");
JButton enrollStudentBtn = new JButton("Enroll Student in Course");
JButton viewCourseBtn = new JButton("View Course Details");
JButton[] buttons = {
addStudentBtn, addFacultyBtn, createCourseBtn,
assignFacultyBtn, enrollStudentBtn, viewCourseBtn
};
for (JButton btn : buttons) {
btn.setAlignmentX(Component.CENTER_ALIGNMENT);
btn.setMaximumSize(new Dimension(300, 30));
frame.add(Box.createRigidArea(new Dimension(0, 10)));
frame.add(btn);
}
addStudentBtn.addActionListener(e -> {
String id = JOptionPane.showInputDialog("Student ID:");
String name = JOptionPane.showInputDialog("Student Name:");
if (id != null && name != null && !id.isEmpty() && !name.isEmpty()) {
students.add(new Student(id.trim(), name.trim()));
JOptionPane.showMessageDialog(null, "Student added.");
}
});
addFacultyBtn.addActionListener(e -> {
String id = JOptionPane.showInputDialog("Faculty ID:");
String name = JOptionPane.showInputDialog("Faculty Name:");
if (id != null && name != null && !id.isEmpty() && !name.isEmpty()) {
faculties.add(new Faculty(id.trim(), name.trim()));
JOptionPane.showMessageDialog(null, "Faculty added.");
}
});
createCourseBtn.addActionListener(e -> {
String code = JOptionPane.showInputDialog("Course Code:");
String title = JOptionPane.showInputDialog("Course Title:");
try {
ix
int cap =
Integer.parseInt(JOptionPane.showInputDialog("Capacity:"));
courses.put(code.trim(), new Course(code.trim(), title.trim(), cap));
JOptionPane.showMessageDialog(null, "Course created.");
} catch (Exception ex) {
JOptionPane.showMessageDialog(null, "Invalid input. Please enter a
number for capacity.");
}
});
assignFacultyBtn.addActionListener(e -> {
String code = JOptionPane.showInputDialog("Course Code:");
String fid = JOptionPane.showInputDialog("Faculty ID:");
Course c = courses.get(code.trim());
Faculty f = findFaculty(fid.trim());
if (c != null && f != null) {
c.assignFaculty(f);
JOptionPane.showMessageDialog(null, "Faculty assigned.");
} else {
JOptionPane.showMessageDialog(null, "Invalid course or faculty.");
}
});
enrollStudentBtn.addActionListener(e -> {
String code = JOptionPane.showInputDialog("Course Code:");
String sid = JOptionPane.showInputDialog("Student ID:");
Course c = courses.get(code.trim());
Student s = findStudent(sid.trim());
if (c != null && s != null) {
boolean enrolled = c.enroll(s);
JOptionPane.showMessageDialog(null, enrolled ? "Student enrolled!" :
"Course full. Added to waiting list.");
} else {
JOptionPane.showMessageDialog(null, "Invalid course or student.");
}
});
viewCourseBtn.addActionListener(e -> {
String code = JOptionPane.showInputDialog("Enter Course Code:");
Course c = courses.get(code.trim());
if (c != null) {
JOptionPane.showMessageDialog(null, c.getDetails());
} else {
JOptionPane.showMessageDialog(null, "Course not found.");
}
});
frame.setVisible(true);
}
x
static Student findStudent(String id) {
for (Student s : students)
if (s.id.equalsIgnoreCase(id)) return s;
return null;
}
static Faculty findFaculty(String id) {
for (Faculty f : faculties)
if (f.id.equalsIgnoreCase(id)) return f;
return null;
}
}
