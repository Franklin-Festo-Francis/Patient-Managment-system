# Patient-Managment-system
#include <iostream>
#include <iomanip>  //for table
#include <string>

using namespace std;

struct Patient {
    int token_number=100;
    string name;
    int age;
    string gender;
    string disease;
    
    Patient* next;
};
struct Patient*head=NULL;
void addPatient( int token_number, string name, int age, string gender, string disease) {
        Patient* newPatient = new Patient{token_number ,name, age, gender, disease, nullptr};
          if (head==NULL) {
            head = newPatient;
        } else {
            Patient* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newPatient;
        }
        cout << "Patient added successfully.\n";
        token_number=token_number+1;
    }

    void displayPatients() {
        if (!head) {
            cout << "No patients to display.\n";
            return;
        }

        cout << "\n--------------------------------------------------------------------------------\n";
        cout << left << setw(10) << " ID" 
             << setw(20) << "Name" 
             << setw(10) << "Age" 
             << setw(10) << "Gender" 
             << setw(20) << "Disease" 
             << "\n";
        cout << "--------------------------------------------------------------------------------\n";

        Patient* temp = head;
        while (temp) {
            cout << left << setw(10) << temp->id
                 << setw(20) << temp->name
                 << setw(10) << temp->age
                 << setw(10) << temp->gender
                 << setw(20) << temp->disease
                 << "\n";
            temp = temp->next;
        }
        cout << "--------------------------------------------------------------------------------\n";
    }

    void deletePatient(int id) {
        if (!head) {
            cout << "No patients to delete.\n";
            return;
        }

        if (head->id == id) {
            Patient* toDelete = head;
            head = head->next;
            delete toDelete;
            cout << "Patient deleted successfully.\n";
            return;
        }

        Patient* temp = head;
        while (temp->next && temp->next->id != id) {
            temp = temp->next;
        }

        if (temp->next && temp->next->id == id) {
            Patient* toDelete = temp->next;
            temp->next = temp->next->next;
            delete toDelete;
            cout << "Patient deleted successfully.\n";
        } else {
            cout << "Patient with ID " << id << " not found.\n";
        }
    }
void searchPatient(int id) {
        Patient* temp = head;
        while (temp) {
            if (temp->id == id) {
                cout << "\nPatientID: " << temp->id
                     << "\nName: " << temp->name
                     << "\nAge: " << temp->age
                     << "\nGender: " << temp->gender
                     << "\nDisease: " << temp->disease << "\n";
                return;
            }
            temp = temp->next;
        }
        cout << "Patient with ID " << id << " not found.\n";
    }
int main() {
    int choice, id, age;
    string name, gender, disease;

    for(;;){
	    cout << "\nPatient Management System\n";
        cout << "1. Add Patient\n";
        cout << "2. Display All Patients\n";
        cout << "3. Delete Patient\n";
        cout << "4. Search Patient\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter Name: ";
                cin>>name;
                
                cout << "Enter Age: ";
                cin >> age;
                 
                cout << "Enter Gender: ";
                cin>>gender;
                
                cout << "Enter Disease: ";
                cin>>disease;
                
                addPatient(id, name, age, gender, disease);
                break;
                
            case 2:
                displayPatients();
                break;
                
            case 3:
                cout << "Enter Patient ID to delete: ";
                cin >> id;
                deletePatient(id);
                break;
                
            case 4:
                cout << "Enter Patient ID to search: ";
                cin >> id;
                searchPatient(id);
                break;
                
            case 5:
                cout << "Exiting the system.\n";
                break;
                
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    }

    return 0;
}
