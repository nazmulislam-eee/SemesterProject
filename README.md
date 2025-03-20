#include <iostream>
#include <cstdlib>
using namespace std;
class universityAdmission
{
private:
    int totalStudents;
    int answer;
    int newStudents;
    int *rollNumberOfStudents;
public:

    universityAdmission (void)   // declaring constructor...
    {
        totalStudents = 0;
        rollNumberOfStudents = NULL;

    }

    void setTotalStudents ()
    {
        // prompting the user to enter the number of initial students
        cout << "Enter the number of initial students: ";
        cin >> totalStudents;
        // Memory allocation for our dynamic array
        rollNumberOfStudents = (int*)malloc(totalStudents * sizeof(int));
        if(rollNumberOfStudents == NULL)
        {
            printf("Memory allocation failed\n");
            exit(0);
        }

        for (int i = 0; i < totalStudents; i++)
        {
            // prompting the user to enter the roll number of existing students
            cout << "Enter the roll number of " << i + 1 << "th student: ";
            cin >> rollNumberOfStudents[i];
        }
    }

    void setAnswer ()
    {
        cout << endl;
        while (1)
        {
            cout << endl;
            // prompting the user to enter option for further functionalities
            cout << "1) Admit New Students" << endl;
            cout << "2) View Students" << endl;
            cout << "3) Exit" << endl;
            cout << "Enter option: ";
            cin >> answer;
            if (answer == 1)
            {
                admitNewStudents();
            }
            else if (answer == 2)
            {
                viewTotalStudents ();
            }
            else if (answer == 3)
            {
                cout << "Thank you" << endl;
                break;
            }
            else
            {
                cout << "Invalid Input, Please try again" << endl;

            }
        }
    }
// a function for admitting new students
    void admitNewStudents()
    {

        cout << "Enter the number of new students: ";
        cin >> newStudents;
        // memory reallocation for our dynamic array
        rollNumberOfStudents = (int*)realloc(rollNumberOfStudents, (totalStudents + newStudents) * sizeof(int));
        if(rollNumberOfStudents == NULL)
        {
            printf("Memory reallocation failed\n");
            exit(0);
        }
        for (int i = totalStudents; i < (totalStudents + newStudents); i++)
        {
            cout << "Enter the roll number of " << i+1 << "th new student: ";
            cin >> rollNumberOfStudents [i];
        }
        totalStudents = totalStudents + newStudents;
    }
    void viewTotalStudents ()
    {
        for (int i = 0; i < totalStudents; i++)
        {
            cout << "The roll number of " << i+1 << "th student is " << *(rollNumberOfStudents+i) << endl;
        }
    }
    // declaring destructor...
    ~universityAdmission ()
    {
        if (rollNumberOfStudents != NULL)
        {
            free(rollNumberOfStudents);
        }
    }
};
int main()
{
    // declaring an object
    universityAdmission student;
    // to take the number of total students from the user
    student.setTotalStudents();
    // for further functionalities
    student.setAnswer();

    return 0;
}
