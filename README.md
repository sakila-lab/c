#include <iostream>
#include <string>
using namespace std;
class Customers_data {
public:
    int C_Id;
    string C_Name;
    string C_Email;
    int C_Age;
    void display() {
        cout << "C_Id: " << C_Id << endl;
        cout << "C_Name: " << C_Name << endl;
        cout << "C_Email: " << C_Email << endl;
        cout << "C_Age: " << C_Age << endl;
    }
};
void show(string s = "Good", int n = 1) {
    for (int i = 1; i <= n; ++i) {
        cout << s;
    }
    cout << endl;
}

class student1 {
    int m1, m2, m3, m4, m5;
public:
    void get() {
        cout << "Enter the marks: ";
        cin >> m1 >> m2 >> m3 >> m4 >> m5;
    }
    friend class test;
};
class test {
    student1 s1;
public:
    void put() {
        s1.get();
        cout << "m1:" << s1.m1 << endl;
        cout << "m2:" << s1.m2 << endl;
        cout << "m3:" << s1.m3 << endl;
        cout << "m4:" << s1.m4 << endl;
        cout << "m5:" << s1.m5 << endl;
    }
};

class Student_Constructor {
public:
    int id;
    string name;

    Student_Constructor(int i, string n) {
        id = i;
        name = n;
    }
    void display() {
        cout << id << "  " << name << endl;
    }
};

class ClassroomDefault {
private:
    double length {4.5};
public:
    void print_length() {
        cout << "length = " << length << endl;
    }
};

int max(int m1, int m2) {
    return (m1 >= m2) ? m1 : m2;
}
float max(float m3, float m4) {
    return (m3 >= m4) ? m3 : m4;
}

class ClassDuration {
    int hr, min;
public:
    void input() {
        cout << "Enter class duration (hr min): ";
        cin >> hr >> min;
    }
    void operator++(int) {
        min++;
        if (min >= 60) {
            min = 0;
        }
    }
    void operator--(int) {
        if (hr == 0 && min == 0) return;
        hr--;
        if (hr < 0) hr = 24;
    }
    void display() {
        cout << "Class duration: " << hr << " hr " << min << " min\n";
    }
};

class Marks {
    int score;
public:
    void setScore(int val) { score = val; }
    Marks operator + (Marks& obj) { Marks temp; temp.score = score + obj.score; return temp; }
    Marks operator - (Marks& obj) { Marks temp; temp.score = score - obj.score; return temp; }
    Marks operator * (Marks& obj) { Marks temp; temp.score = score * obj.score; return temp; }
    Marks operator / (Marks& obj) {
        Marks temp;
        if (obj.score != 0) temp.score = score / obj.score;
        else { cout << "Error: Division by zero!" << endl; temp.score = 0; }
        return temp;
    }
    void display() const { cout << "Marks: " << score << endl; }
};

class Student_Static {
public:
    static int student_count;
    Student_Static() { student_count++; }
    static int get_count() { return student_count; }
};
int Student_Static::student_count = 3;

class Person {
protected:
    string name;
    int age;
public:
    void setPersonDetails(string n, int a) { name = n; age = a; }
    void showPersonDetails() { cout << "Name: " << name << ", Age: " << age; }
};
class Student : public Person {
protected:
    int rollNo;
    float marks;
public:
    void setStudentDetails(string n, int a, int r, float m) {
        setPersonDetails(n, a);
        rollNo = r;
        marks = m;
    }
    void showStudentDetails() {
        showPersonDetails();
        cout << ", Roll No: " << rollNo << ", Marks: " << marks << endl;
    }
};
class Classroom : public Student {
private:
    int totalStudents;
    Student students[50];
public:
    Classroom(int t) { totalStudents = t; }
    void inputDetails() {
        string n;
        int a, r;
        float m;
        for (int i = 0; i < totalStudents; i++) {
            cout << "\nEnter details of student " << i + 1 << ":\n";
            cout << "Name: "; cin >> n;
            cout << "Age: "; cin >> a;
            cout << "Roll No: "; cin >> r;
            cout << "Percentage: "; cin >> m;
            students[i].setStudentDetails(n, a, r, m);
        }
    }
    void displayDetails() {
        cout << "\n--- Class Student Details ---\n";
        for (int i = 0; i < totalStudents; i++) {
            students[i].showStudentDetails();
        }
    }
};

int main() {
    int choice;
    do {
        cout << "\n--- Main Menu ---\n";
        cout << "1. Customer Data\n";
        cout << "2. Function with Default Values\n";
        cout << "3. Friend Class Example\n";
        cout << "4. Constructor Example\n";
        cout << "5. Default Initialization Class\n";
        cout << "6. Function Overloading (Max)\n";
        cout << "7. Operator ++ and --\n";
        cout << "8. Operator Overloading (Arithmetic)\n";
        cout << "9. Static Members\n";
        cout << "10. Inheritance Example\n";
        cout << "0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: {
                Customers_data c; 
                c.C_Id = 101; c.C_Name = "John"; c.C_Email = "John123@gmail.com"; c.C_Age = 20; 
                c.display(); 
                break;
            }
            case 2: {
                cout << "the student has just passed: "; show();
                cout << "the student has secured distinction: "; show("Very Good");
                break;
            }
            case 3: {
                test t; t.put();
                break;
            }
            case 4: {
                Student_Constructor s1(1001, "Akila"), s2(1002, "Srihitha");
                s1.display(); s2.display();
                break;
            }
            case 5: {
                ClassroomDefault c; c.print_length();
                break;
            }
            case 6: {
                int m1, m2;
                cout << "Enter two integers: "; cin >> m1 >> m2;
                cout << "Max int: " << max(m1, m2) << endl;
                float f1, f2;
                cout << "Enter two floats: "; cin >> f1 >> f2;
                cout << "Max float: " << max(f1, f2) << endl;
                break;
            }
            case 7: {
                ClassDuration cd; cd.input();
                cd++; cout << "After incrementing by 1 minute:\n"; cd.display();
                cd--; cd--; cout << "After decrementing by 2 hours:\n"; cd.display();
                break;
            }
            case 8: {
                Marks student1, student2, result;
                int s1, s2; char op;
                cout << "Enter marks for Student 1: "; cin >> s1;
                cout << "Enter marks for Student 2: "; cin >> s2;
                student1.setScore(s1); student2.setScore(s2);
                cout << "Enter operation (+ - * /): "; cin >> op;
                switch(op) {
                    case '+': result = student1 + student2; break;
                    case '-': result = student2 - student1; break;
                    case '*': result = student1 * student2; break;
                    case '/': result = student1 / student2; break;
                    default: cout << "Invalid choice\n"; continue;
                }
                result.display(); break;
            }
            case 9: {
                cout << "Students before: " << Student_Static::get_count() << endl;
                Student_Static s1, s2, s3;
                cout << "Students after: " << Student_Static::get_count() << endl;
                break;
            }
            case 10: {
                int n; cout << "Enter number of students in class: "; cin >> n;
                Classroom cls(n); cls.inputDetails(); cls.displayDetails();
                break;
            }
        }
    } while(choice != 0);

    return 0;
}
