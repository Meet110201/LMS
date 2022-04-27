// LIBRARY MANAMGEMEY PROGRAM (GUGU v1.3)
// name -- PARMEET SINGH
// UID -- 20BCS4415

// header files
#include <iostream>
#include <stdio.h>
#include <stdlib.h>
#include <fstream>
#include <string.h>
#include <string>
#include <conio.h>
#include <iomanip>
using namespace std;

void MainMenu(); //declaration of mainmenu function
class Homepage   // creating the homepage class to print the heading of the program and other alignment opeartions of headings
{
public:
    enum Position // decalaring the global variables for print function
    {
        LEFT,
        CENTRE,
        RIGHT
    };
    const int lineLength = 60; // defining the lenght of border

    void print(Position pos, string s, int linelength) // function to print the text in left / right / center
    {
        int spaces = 0; // spaces to be printed ini value = 0
        switch (pos)
        {
        case CENTRE:
            spaces = ((linelength - s.size()) / 2); // text at center
            break;
        case RIGHT:
            spaces = (linelength - s.size()); // texxt at right
            break;
        }
        if (spaces > 0) // text at left
            cout << string(spaces, ' ');
        cout << s << endl; // message to be printed
    }
    void heading(const char *head) // print heading of the program -----  called by all the funnctions to print the respective heading
    {
        system("cls");
        cout << endl
             << endl
             << endl
             << "############################################################" << endl
             << " ---------------------------------------------------------- " << endl
             << "|                           GUGU                           |" << endl
             << "|                                                          |" << endl
             << "|              STATE LIBRARY MANAGEMENT SYSTEM             |" << endl
             << "|                                            Version 1.3   |" << endl
             << " ---------------------------------------------------------- " << endl
             << "############################################################" << endl
             << endl
             << endl;
        print(CENTRE, head, lineLength); // heading name sent by the function as a argument
        cout << "------------------------------------------------------------" << endl;
    }
    Homepage() // print the welcome screen
    {
        heading("");
        cout << "############################################################" << endl
             << " ---------------------------------------------------------- " << endl
             << "|              ****       WELCOME TO      ****             |" << endl
             << "|               ****       LIBRARY       ****              |" << endl
             << "|              ****       MANAGEMENT      ****             |" << endl
             << "|               ****       SYSTEM        ****              |" << endl
             << " ---------------------------------------------------------- " << endl
             << "############################################################" << endl
             << "\nPress any key to continue.....";
        getch();
    }
    friend class Library; // making the library class as friend class
};

class Library : public Homepage // inheriting the homepage class in library class
{
public:
    char BookName[100], bookAuthor[50], bookID[20], bookPublication[50], UserName[10], Password[8]; // declaring the required variables
    int q, B, p;                                                                                    // declaring the required variables
    Library()                                                                                       // declaring a constructor for default values of the variables
    {
        strcpy(BookName, "NIL");        // default value
        strcpy(bookAuthor, "NIL");      // default value
        strcpy(bookID, "NIL");          // default value
        strcpy(bookPublication, "NIL"); // default value
        q = 0;                          // default value
        B = 0;                          // default value
        p = 0;                          // default value
    }
    void studentMenu() // menu option for student
    {
        int choice = 0;
        do
        {
            heading("*** STUDENT MENU ***");        // printing the heading
            cout << "\n\t~ 1 >> View Books" << endl // option 1
                 << "\t~ 2 >> Search Books" << endl // option 2
                 << endl
                 << "\t~ 9 >> Go to Main Menu" << endl   // option 3
                 << "\t~ 0 >> Close Application" << endl // option 4
                 << "\n>> Enter Choice :> ";
            cin >> choice;
            switch (choice)
            {
            case 1:
                Book_list(1); // calling the book_list function to get the list of books
                break;
            case 2:
                find_book(1); // calling the find_book function to find the book in database by name / book ID
                break;
            case 9:
                cout << "\n\n";
                print(CENTRE, "THANK YOU !! :)", lineLength); // thankyou message
                getch();
                MainMenu(); // moving to main Menu
                break;
            case 0:
                exit(0); // closing the application
                break;
            default:
                cout << "\n\n";
                print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength);
                getch();
                break;
            }
        } while (choice != 0);
    }
    void librarianMenu() // menu option for librarian
    {
        int choice = 0;
        do
        {
            heading("*** LIBRARIAN MENU ***");                     // printing the heading
            cout << "\n\t~ 1 >> View Books" << endl                  // option 1
                 << "\t~ 2 >> Search Books" << endl                // option 2
                 << "\t~ 3 >> Modify / Add / Delete Books" << endl // option 3
                 << "\t~ 4 >> Issue Books" << endl                 // option 4
                 << "\t~ 5 >> Update Credential" << endl           // option 5
                 << endl
                 << "\t~ 9 >> Log Out to Main Menu" << endl // option 6
                 << "\t~ 0 >> Close Application" << endl    // option 7
                 << "\n>> Enter Choice :> ";
            cin >> choice;
            switch (choice)
            {
            case 1:
                Book_list(2); // calling the book_list function to get the list of books
                break;
            case 2:
                find_book(2); // calling the find_book function to find the book in database by name / book ID
                break;
            case 3:
                Edit_menu(); // calling the edit_menu to edit the library database accordingly
                break;
            case 4:
                issue_book(); // calling the issue_book function to issue the book
                break;
            case 5:
                updateCredential(); // calling the updateCredential function to update the password and username
                break;
            case 9:
                cout << "\n\n";
                print(CENTRE, "THANK YOU !! :)", lineLength); // thankyou message
                getch();
                MainMenu();
                break;
            case 0:
                exit(0); // close the application
                break;
            default:
                cout << "\n\n";
                print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength);
                getch();
                break;
            }
        } while (choice != 0); // going agian to re enter the correct option
    }
    void getdata() // function to get the book data
    {
        int i;
        fflush(stdin);
        heading("*** ENTER BOOK DETAILS ***"); // printing the heading
        cout << "\n\t>> Enter Book's Name : "; // book name
        cin.getline(BookName, 100);
        for (i = 0; BookName[i] != '\0'; i++) // making the small aplhabets to capital for entring in the database
        {
            if (BookName[i] >= 'a' && BookName[i] <= 'z')
                BookName[i] -= 32;
        }
        cout << "\t>> Enter Author's Name : "; // book author
        cin.getline(bookAuthor, 50);
        cout << "\t>> Enter Publication name : "; // book publication
        cin.getline(bookPublication, 50);
        cout << "\t>> Enter Book's ID : "; // book Id
        cin.getline(bookID, 20);
        cout << "\t>> Enter Book's Price : "; // book price
        cin >> p;
        cout << "\t>> Enter Book's Quantity : "; // book stock amount
        cin >> q;
    }
    void display_book(int i) // funtion to print the books details in tabular form using iomanip functions
    {
        if (i == 1) // for student
            cout << "  |   " << left << setw(7) << bookID << "|  " << left << setw(50) << BookName << "|  " << left << setw(50) << bookAuthor << "|  " << left << setw(50) << bookPublication << "|" << left << setw(9) << " "
                 << "| " << right << setw(12) << " |" << endl;
        else if (i == 2) // for librarian
            cout << "  |   " << left << setw(7) << bookID << "|  " << left << setw(50) << BookName << "|  " << left << setw(50) << bookAuthor << "|  " << left << setw(50) << bookPublication << "|  Rs. " << left << setw(4) << p << "| " << right << setw(4) << q << " Pcs.  |" << endl;
    }
    void Book_list(int i)
    {
        int b, r = 0;
        heading("*** BOOK LIST ***"); // printing the haeding
        b = branch(i);                // calliing the branch function to print the varioous branches and aassigning the return value to variable  b
        heading("*** BOOK LIST ***");
        ifstream intf("Booksdata.txt", ios::binary); // reading the booksdatabase file from directory
        if (!intf)                                   // checking the file is open or not
        {
            cout << "\n\n";
            print(CENTRE, "Error: 504 -- File Not Found", lineLength);
            getch();
        }
        else
        {
            heading("*** BOOK LIST ***");
            cout << left << setw(10) << "  S. No" << left << setw(30) << "Book ID" << left << setw(56) << "Book Name" << left << setw(52) << "Author" << left << setw(32) << "Publication" << left << setw(10) << "Price" << left << setw(7) << "Quantity" << endl;
            cout << " _______________________________________________________________________________________________________________________________________________________________________________________________________\n"
                 << endl;
            intf.read((char *)this, sizeof(*this)); // reading the book data from othe file
            while (!intf.eof())                     // printin the data of book to screen
            {
                if (b == B) // checking the branch function return value is matching or not
                {
                    if (q == 0 && i == 1) // checking the book stock in the database
                    {
                    }
                    else // printing the books
                    {
                        r++;
                        cout << "|" << right << setw(4) << r;
                        display_book(i); // display_book is called to print he book detials
                    }
                }
                intf.read((char *)this, sizeof(*this)); // reading the nxt book from the database
            }
            cout << " _______________________________________________________________________________________________________________________________________________________________________________________________________" << endl;
        }
        intf.close(); // closing the file booksdata.txt
        cout << "\n\n";
        cout << "\nPress any key to continue.....";
        getch();
        if (i == 1)
            studentMenu(); // going back to student menu
        else
            librarianMenu(); // going back to librarian menu
    }
    void find_book(int x) // function to find the a particular book form the database of library
    {
        int i, b, cont = 0;
        char ch[100];
        heading("*** FIND BOOKS ***"); // printing the heading
        b = branch(x);
        heading("*** FIND BOOKS ***");
        ifstream intf("Booksdata.txt", ios::binary); // reading the booksdata.txt in binary format
        if (!intf)                                   // checking the file is open or not
        {
            print(CENTRE, "Error: 504 -- File Not Found", lineLength); // error message
            getch();                                                   // program pause (expecting a char)
            if (x == 1)
                studentMenu(); // going back to student menu
            else
                librarianMenu(); // hoing back to library menu
        }
        heading("*** FIND BOOKS ***");                  // printing the nxt screen heading
        cout << "\n\t~ 1 >> Search By Name" << endl       // option 1
             << "\t~ 2 >> Search By Book's ID" << endl; // option2
        cout << "\nEnter Your Choice : ";
        cin >> i;
        fflush(stdin);
        intf.read((char *)this, sizeof(*this)); // reading the file
        if (i == 1)                             // if part for search book by name
        {
            cout << "\n\tEnter Book's Name : ";
            cin.getline(ch, 100); // reading the user entered book name
            heading("*** FIND BOOKS ***");
            cout << left << setw(30) << "     Book ID" << left << setw(56) << "Book Name" << left << setw(52) << "Author" << left << setw(32) << "Publication" << left << setw(10) << "    Price" << left << setw(7) << "Quantity" << endl;
            cout << "   ________________________________________________________________________________________________________________________________________________________________________________________________\n"
                 << endl;
            while (!intf.eof()) // ckecking end of file
            {
                for (i = 0; b == B && q != 0 && BookName[i] != '\0' && ch[i] != '\0' && (ch[i] == BookName[i] || ch[i] == BookName[i] + 32); i++) // for loop conditions for comparing the char of book names and stock
                    ;
                if (BookName[i] == '\0' && ch[i] == '\0') // if cond for end of book name
                {
                    display_book(x); // displaying the books found
                    cont++;          // book counter
                    break;
                }
                intf.read((char *)this, sizeof(*this)); // reading the next data form booksdata.txt
            }
            cout << "   ________________________________________________________________________________________________________________________________________________________________________________________________" << endl;
            getch();
        }
        else if (i == 2) // if part for search book by ID
        {
            cout << "\n\tEnter Book's ID : ";
            cin.getline(ch, 100); // reading the user entered book id
            heading("*** FIND BOOKS ***");
            cout << left << setw(30) << "     Book ID" << left << setw(56) << "Book Name" << left << setw(52) << "Author" << left << setw(32) << "Publication" << left << setw(10) << "    Price" << left << setw(7) << "Quantity" << endl;
            cout << "   ________________________________________________________________________________________________________________________________________________________________________________________________\n"
                 << endl;
            while (!intf.eof()) // checking the end of file
            {
                for (i = 0; b == B && q != 0 && bookID[i] != '\0' && ch[i] != '\0' && ch[i] == bookID[i]; i++) // for loop conditions for comparing the char of book id and stock
                    ;
                if (bookID[i] == '\0' && ch[i] == '\0') // if cond for end of book id
                {
                    display_book(x); // displaying the books found
                    cont++;          // book counter
                    break;
                }
                intf.read((char *)this, sizeof(*this)); // reading the next data form booksdata.txt
            }
            cout << "   ________________________________________________________________________________________________________________________________________________________________________________________________" << endl;
        }
        else // error condition in case of wrong input
        {
            cont++;
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength); // error message
            getch();
            find_book(x); // going back to find_book function
        }
        intf.close();  // closing the file
        if (cont == 0) // condition if the book count is zero of not
        {
            cout << "\n\n";
            print(LEFT, "SORRY !!  Book is not available  :( :(", lineLength);
            cout << "\nPress any key to continue.....";
            getch();
        }
        else if (!cont == 0)
        {
            cout << "\n\n";
            print(LEFT, "These Book(s) is/are available  :) :)", lineLength);
            cout << "\nPress any key to continue.....";
            getch();
        }
        if (x == 1)
            studentMenu(); // going back to student menu
        else
            librarianMenu(); // going back to librarian menu
    }
    int branch(int x) // function to distribute the books of different branches
    {
        int i;
        heading("*** BRANCH ***");                        // printing the heading
        cout << "\n\t~ 1 >> Class 12th" << endl             // branch 1
             << "\t~ 2 >> Computer Science" << endl       // branch 2
             << "\t~ 3 >> Electrical" << endl             // branch 3
             << "\t~ 4 >> Civil Engineering" << endl      // branch 4
             << "\t~ 5 >> Mechanical Engineering" << endl // branch 5
             << "\t~ 6 >> Newspapers" << endl             // branch 6
             << endl
             << "\t~ 9 >> Go to menu\n"; // option 7
        cout << "\n>> Enter your choice : ";
        cin >> i;
        switch (i) // switch case to return the respective branch value
        {
        case 1:
            return 1;
            break;
        case 2:
            return 2;
            break;
        case 3:
            return 3;
            break;
        case 4:
            return 4;
            break;
        case 5:
            return 5;
            break;
        case 6:
            return 6;
            break;
        case 9:
            if (x == 1)
                studentMenu(); // going back to student menu
            else
                librarianMenu(); // going back to librarian menu
            break;
        default: // case for error
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength);
            getch();
            branch(x);
            break;
        }
    }
    void authorization() // function for password authentication
    {
        string temp1, temp2;                       // declaring the varaiables
        ofstream file_o("password.txt", ios::out); // creating the file for saving the password
        string tempU = "admin", tempP = "admin";   // writing to file (default username- admin and password - admin)
        file_o << tempU << endl;                   // writing to file
        file_o << tempP;                           // writing to file
        file_o.close();                            // closing the file
        ifstream file_open("password.txt");        // opening the password.txt from the directory to read the username and password
        int attempt = 0;                           // attempt counter
        do
        {
            heading("*** AUTHENTICATION ***"); // printing the heading
            cout << endl
                 << "\t~ User Name : "; // enter username
            cin >> UserName;
            cout << "\t~ Password : "; // enter passowrd
            cin >> Password;
            getline(file_open, temp1);                                                    // reading username form the password.txt file
            getline(file_open, temp2);                                                    // reading password form the password.txt file
            if ((!strcmp(UserName, temp1.c_str())) && (!strcmp(Password, temp2.c_str()))) // comparing the username and password of file and user by using strcmp
            {
                cout << "\n\n";
                print(CENTRE, "LOGIN SUCCESSFULL.. :)", lineLength); // if correct the proceed to librarian menu
                getch();                                             // program paused
                librarianMenu();                                     // calling the librarian menu
            }
            else // condition for wrong password
            {
                cout << "\n\n";
                print(CENTRE, "Acess Denied...Try Again ...", lineLength);      // error message
                cout << "\n\tAttempts Left : " << (-1) * (attempt - 2) << endl; // reamining attempts (max attemps 3)
                attempt++;                                                      // attemp increment
                getch();
            }
        } while (attempt <= 2); // checking the atempt count if completed exit the loop
        if (attempt > 2)        // if no attempts are there the print the below message do according
        {
            cout << "\n\n";
            heading("LOGIN FAILED ... :(");                             // error message
            print(CENTRE, "Acess Denied... ", lineLength);              //error message
            print(CENTRE, "Authorised Personels only....", lineLength); // error message
            getch();
            MainMenu(); // going back to main menu
        }
        file_open.close(); // close the password.txt file
    }
    void updateCredential() // funciton to update username and password in password.txt file
    {
        heading("*** Update Credentials ***");         // printing the heading
        string temp1, temp2, newPassword, newUsername; // required variables
        ifstream file_open;                            // opening the password.txt the file
        file_open.open("password.txt");
        int attempt = 0; // attemp counter
        do
        {
            cout << endl
                 << "\t\t~ User Name : "; // enter username
            cin >> UserName;
            cout << "\t\t~ Old Password : "; // enter password
            cin >> Password;
            getline(file_open, temp1);                                                    // reading username form the password.txt file
            getline(file_open, temp2);                                                    // reading password form the password.txt file
            if ((!strcmp(UserName, temp1.c_str())) && (!strcmp(Password, temp2.c_str()))) // comparing the username and password of file and user by using strcmp
            {
                ofstream file_out("password.txt", ios::out); // opening the password.txt file to edit the data
                if (!strcmp(temp1.c_str(), "admin"))         // checking the previous username is default usernme (admin) or not
                {
                    cout << "\n\t\tNew Username : "; // enter new username
                    cin >> newUsername;
                    file_out << newUsername << endl; // replace the new username with old username
                    cout << "\n\t\tNew Password : "; // enter new password
                    cin >> newPassword;
                    file_out << newPassword; // replace the new password with old password
                    cout << "\n\n";
                    print(LEFT, "Password and Username has been changed Successfully... :)", lineLength); // successfull message
                }
                else // if username is not default (admin)
                {
                    file_out << temp1 << endl;
                    cout << "\n\t\tNew Password : "; // enter new password
                    cin >> newPassword;
                    file_out << newPassword;                                                   // replace the new password with old password
                    cout << "\n\n";
                    print(LEFT, "Password has been changed Successfully... :)", lineLength); // successfull message
                }
                file_out.close(); // close the password.txt file

                cout << "\nPress any key to continue.....";
                getch();
                librarianMenu(); // go back to librarian menu
            }
            else
            {
                cout << "\n\n";
                print(CENTRE, "Acess Denied...Try Again ...", lineLength);      // error message
                cout << "\n\tAttempts Left : " << (-1) * (attempt - 2) << endl; // error message
                attempt++;                                                      // attempt counter
                getch();                                                        //pause program
            }
        } while (attempt <= 2);
        if (attempt > 2)
        {
            heading("LOGIN FAILED");                                    // printing the heading
            cout << "\n\n";
            print(CENTRE, "Acess Denied... ", lineLength);              // error message
            print(CENTRE, "Authorised Personels only....", lineLength); // error message
            getch();
            MainMenu(); // go back to main menu
        }
        file_open.close(); // close the password.txt file
    }
    void Edit_menu()
    {
        int i;
        heading("*** EDIT BOOKS ***");                             // printing the heading
        cout << "\n\t~ 1 >> Modification In Current Books" << endl // option 1
             << "\t~ 2 >> Add New Book" << endl                    // option 2
             << "\t~ 3 >> Delete A Book" << endl                   // option 3
             << endl
             << "\t~ 9 >> Go to Main Menu" << endl // option 4
             << "\t~ 0 >>EXIT\n";                  // option 5
        cout << "\n>> Enter your choice : ";
        cin >> i;
        switch (i)
        {
        case 1:
            modifyCurrentBooks(); // calling the function modifyCurrentBooks() to edit data in current books
            break;
        case 2:
            addNewBook(); // calling the function addNewBook() to add new book
            break;
        case 3:
            deleteBook(); // calling the function deleteBook() to detele the book form database
            break;
        case 9:
            librarianMenu(); // gooing back to librarian menu
            break;
        case 0:
            exit(0); // close the application
        default:
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength); // error message
            getch();
            Edit_menu(); // going back to edit menu
            break;
        }
    }
    void modifyCurrentBooks()
    {
        char ch, st1[100]; // declaring the required variables
        int i = 0, b, cont = 0;
        heading("*** MODIFY CURRRENT BOOK ***");      // printing the heading
        b = branch(2);                                // calliing the branch function to print the varioous branches and aassigning the return value to variable  b
        heading("*** MODIFY CURRRENT BOOK ***");      // printing the heading
        ifstream intf1("Booksdata.txt", ios::binary); // opening the booksdatabase.txt file to read
        if (!intf1)                                   // checking the file is open or not
        {
            cout << "\n\n";
            print(CENTRE, "Error: 504 -- File Not Found", lineLength); // error message
            getch();
            librarianMenu(); // go back to librarian menu
        }
        intf1.close();                                 // close the booksdata.txt file
        cout << "\n\t~ 1 >> Search By Book Name" << endl // option 1
             << "\t~ 2 >> Search By Book's ID\n";      // option 2
        cout << "\n>> Enter Your Choice : ";
        cin >> i;
        fflush(stdin);
        switch (i)
        {
        case 1: // search book by name and then edit it
        {
            cout << "\n\tEnter Book Name : "; // enter book name
            cin.getline(st1, 100);
            fstream intf("Booksdata.txt", ios::in | ios::out | ios::ate | ios::binary); // opening the booksdata.txt file to edit
            intf.seekg(0);                                                              // set the position of the next character to be extracted from the file
            intf.read((char *)this, sizeof(*this));                                     // reading the data from the booksdata.txt file
            while (!intf.eof())                                                         // checking end of file
            {
                for (i = 0; b == B && BookName[i] != '\0' && st1[i] != '\0' && (st1[i] == BookName[i] || st1[i] == BookName[i] + 32); i++) // for loop conditions for comparing the char of book names and stock
                    ;
                if (BookName[i] == '\0' && st1[i] == '\0') // if cond for end of book name
                {
                    cont++;                                   // book counter
                    getdata();                                // geting data to replace / update with the old data of a book
                    intf.seekp(intf.tellp() - sizeof(*this)); // set the position of the pointer in the output sequence with the specified position
                    intf.write((char *)this, sizeof(*this));  // writing the data taken from getdata() function in line 556
                    break;
                }
                intf.read((char *)this, sizeof(*this)); // reading the nxt book from the booksdata.txt file
            }
            intf.close(); // close the booksdata.txt file
            break;
        }
        case 2: // search book by ID and then edit it
        {
            cout << "\n\tEnter Book's ID : "; // enter book ID
            cin.getline(st1, 100);
            fstream intf("Booksdata.txt", ios::in | ios::out | ios::ate | ios::binary); // opening the booksdata.txt file to edit
            intf.seekg(0);                                                              // set the position of the next character to be extracted from the file
            intf.read((char *)this, sizeof(*this));                                     // reading the data from the booksdata.txt file
            while (!intf.eof())                                                         // checking end of file
            {
                for (i = 0; b == B && bookID[i] != '\0' && st1[i] != '\0' && st1[i] == bookID[i]; i++) // for loop conditions for comparing the char of book ID and stock
                    ;
                if (bookID[i] == '\0' && st1[i] == '\0') // if cond for end of book ID
                {
                    cont++;                                   // book counter
                    getdata();                                // geting data to replace / update with the old data of a book
                    intf.seekp(intf.tellp() - sizeof(*this)); // set the position of the pointer in the output sequence with the specified position
                    intf.write((char *)this, sizeof(*this));  //writing the data taken from getdata() function in line 556
                    break;
                }
                intf.read((char *)this, sizeof(*this)); // reading the nxt book from the booksdata.txt file
            }
            intf.close(); // close the booksdata.txt file
            break;
        }
        default: // incase of wrong input of choice
        {
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength); // error message
            getch();
            modifyCurrentBooks(); // again calling the modifyCurrenBooks() function
            break;
        }
        }
        if (cont == 0) // if condition for no record of books
        {
            cout << "\n\n";
            print(CENTRE, "Book Not Found", lineLength);
            getch();
            Edit_menu(); // calling back to editMenu()
        }
        else // else statement for successfull operation
        {
            cout << "\n\n";
            print(CENTRE, "Update Successful", lineLength);
            getch();
        }
    }
    void addNewBook()
    {
        B = branch(2);                                          // assinging the branch in which the books is to added
        heading("*** ADD NEW BOOK ***");                        // printing the heading
        getdata();                                              // calling the function getdata() to get data from the user
        ofstream outf("Booksdata.txt", ios::app | ios::binary); // opening the file booksdata.txt for editing
        outf.write((char *)this, sizeof(*this));                // writing the data to the file taken by getdata() function
        outf.close();                                           // close bookdata.txt file
        cout << "\n\n";
        print(CENTRE, "Book Added Successful..", lineLength);   // successfull message
        cout << endl
             << "ADD NEW BOOK (y/n) : ";
        char choice;
        cin >> choice;
        if (choice == 'y')
        {
            addNewBook();
        }
        else if (choice == 'n')
        {
        }
    }
    void deleteBook()
    {
        char ch, st1[100]; // declaring the required variables
        int i = 0, b, cont = 0;
        heading("*** DELETE / REMOVE BOOK ***");      // printing the heading
        b = branch(2);                                // calliing the branch function to print the varioous branches and aassigning the return value to variable  b
        ifstream intf1("Booksdata.txt", ios::binary); // reading the booksdatabase.txt file
        if (!intf1)                                   // checking the file is open or not
        {
            cout << "\n\n";
            print(CENTRE, "Error: 504 -- File Not Found", lineLength); // error message
            getch();                                                   // pause program
            intf1.close();                                             // close the booksdata.txt file
            librarianMenu();                                           // go back to librarian menu
        }
        intf1.close();                           // close the booksdata.txt file
        heading("*** DELETE / REMOVE BOOKS");    // printing the heading
        cout << "\n\t~ 1 >> By Book Name" << endl  // option 1
             << "\t~ 2 >> By Book's ID" << endl; // option 2
        cout << "\n>> Enter Your Choice : ";
        cin >> i;
        fflush(stdin);
        switch (i)
        {
        case 1: // search book by name and then edit it
        {
            cout << "\n\tEnter Book Name : "; // enter book name
            cin.getline(st1, 100);
            ofstream outf("temp.txt", ios::app | ios::binary); // creating a file temp.txt to store the data of books that are not to be delete
            ifstream intf("Booksdata.txt", ios::binary);       // opening the booksdatabase.txt file to read
            intf.read((char *)this, sizeof(*this));            // reading the data from the booksdata.txt file
            while (!intf.eof())                                // checking end of file
            {
                for (i = 0; b == B && BookName[i] != '\0' && st1[i] != '\0' && (st1[i] == BookName[i] || st1[i] == BookName[i] + 32); i++) // for loop conditions for comparing the char of book names and stock
                    ;
                if (BookName[i] == '\0' && st1[i] == '\0') // if cond for end of book name
                {
                    cont++;                                 // book counter
                    intf.read((char *)this, sizeof(*this)); // reading the data from the booksdata.txt file
                }
                else
                {
                    outf.write((char *)this, sizeof(*this)); // writing the data to temp.txt file
                    intf.read((char *)this, sizeof(*this));  // reading the nxt data from the booksdata.txt file
                }
            }
            intf.close();                        // close the booksdata.txt file
            outf.close();                        // close the temp.txt file
            remove("Booksdata.txt");             // delete the booksdata.txt file from directory
            rename("temp.txt", "Booksdata.txt"); // renameing the temp.txt file to booksdata.txt file
            break;
        }
        case 2: // search book by ID and then edit it
        {
            cout << "\n\tEnter Book's ID : "; // enter book ID
            cin.getline(st1, 100);
            ofstream outf("temp.txt", ios::app | ios::binary); // creating a file temp.txt to store the data of books that are not to be delete
            ifstream intf("Booksdata.txt", ios::binary);       // opening the booksdatabase.txt file to read
            intf.read((char *)this, sizeof(*this));            // reading the data from the booksdata.txt file
            while (!intf.eof())                                // checking end of file
            {
                for (i = 0; b == B && bookID[i] != '\0' && st1[i] != '\0' && st1[i] == bookID[i]; i++) // for loop conditions for comparing the char of book ID and stock
                    ;
                if (bookID[i] == '\0' && st1[i] == '\0') // if cond for end of book name
                {
                    cont++;                                 // book counter
                    intf.read((char *)this, sizeof(*this)); // reading the data from the booksdata.txt file
                }
                else
                {
                    outf.write((char *)this, sizeof(*this)); // writing the data to temp.txt file
                    intf.read((char *)this, sizeof(*this));  // reading the nxt data from the booksdata.txt file
                }
            }
            outf.close();                        // close the temp.txt file
            intf.close();                        // close the booksdata.txt file
            remove("Booksdata.txt");             // delete the booksdata.txt file from directory
            rename("temp.txt", "Booksdata.txt"); // renameing the temp.txt file to booksdata.txt file
            break;
        }
        default: // incase of wrong input of choice
        {
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength); // error message
            getch();
            deleteBook(); // again calling the deleteBook() function
            break;
        }
        }
        if (cont == 0) // if condition for no record of books
        {
            cout << "\n\n";
            print(CENTRE, "No Record Found", lineLength);
            getch();
            Edit_menu(); // calling back to editMenu()
        }
        else // else statement for successfull operation
        {
            cout << "\n\n";
            print(CENTRE, "Deletion Successful", lineLength);
            getch();
        }
    }
    void issue_book() // function to issue the book to a student (access to librarian only)
    {
        char st[50], st1[20]; // declaring the required variables
        int b, i, j, d, m, y, dd, mm, yy, cont = 0;
        heading("*** ISSUE BOOK ***");                             // printing the heading
        cout << "\n\t~ 1 >> Issue Book" << endl                      // option 1
             << "\t~ 2 >> View Issued Book" << endl                // option 2
             << "\t~ 3 >> Search student who isuued books" << endl // option 3
             << "\t~ 4 >> Re-Issue Book" << endl                   // option 4
             << "\t~ 5 >> Return Book" << endl                     // option 5
             << endl
             << "\t~ 9 >> Go back to menu" << endl // option 6
             << "\n>> Enter Your Choice : ";
        cin >> i;
        fflush(stdin);
        switch (i)
        {
        case 1: // case for issue book to a student
        {
            heading("*** ISSUE BOOK ***"); // printing the heading
            b = branch(2);                 // calliing the branch function to print the varioous branches and aassigning the return value to variable  b
            heading("*** ISSUE BOOK ***"); //priniting the heading
            fflush(stdin);
            cout << "\n\tEnter Book Name : "; // enter book name
            cin.getline(BookName, 100);
            cout << "\tEnter Book's ID : "; // enter book ID
            cin.getline(bookID, 20);
            //strcpy(st,bookID);
            edit_bookStock(bookID, b, 1);      // calling the edit_bookStock() function to find the book in booksdata.txt
            cout << "\tEnter Student Name : "; // enter student name
            cin.getline(bookAuthor, 100);
            cout << "\tEnter Student's ID : "; // set student id
            cin.getline(bookPublication, 20);  // temporaryly using bookpublication to set student id
            cout << "\tEnter date : ";         // enter date of issue in format (dd mm yyyy) give space between the numbers
            cin >> q >> B >> p;
            ofstream outf("student.txt", ios::binary | ios::app); // creating the file student.txt to store the book issue data
            outf.write((char *)this, sizeof(*this));              // write the above data entered to the file
            outf.close();                                         // close student.txt file
            cout << "\n\n";
            print(CENTRE, "Issue Successfully", lineLength);      // successfull message
            cout << "\nPress any key to continue.....";
            getch();
            break;
        }
        case 2: // case for veiwing the issued books
        {
            heading("*** VIEW ISSUED BOOK ***");       // printing the heading
            ifstream intf("student.txt", ios::binary); // opening the student.txt file to read the data
            intf.read((char *)this, sizeof(*this));    // reading the data from student.txt file
            i = 0;
            while (!intf.eof()) //checking the end of file
            {
                i++;
                cout << "\n\t " << i << ". ****************************** \n"; // printing the data on the screen
                cout << "\tStudent Name : " << bookAuthor << endl
                     << "\tStudent's ID : " << bookPublication << endl
                     << "\tBook Name : " << BookName << endl
                     << "\tBook's ID : " << bookID << endl
                     << "\tDate : " << q << "/" << B << "/" << p << endl;
                intf.read((char *)this, sizeof(*this)); // reading the  nxt data from the student.txt file
            }
            getch();
            intf.close(); // close the file student.txt
            break;
        }
        case 3: // case for searching the student in student.txt file
        {
            heading("*** SEARCH STUDENT ***"); // printing the heading
            fflush(stdin);
            cout << "\tEnter Student Name : "; // enter sudent name
            cin.getline(st, 50);
            cout << "\tEnter Student's ID : "; // enter student ID
            cin.getline(st1, 20);
            cout << endl;
            ifstream intf("student.txt", ios::binary); // opening the file student.txt to read
            intf.read((char *)this, sizeof(*this));    // reading the data from student.txt file
            cont = 0;                                  // counter
            while (!intf.eof())                        // checking the end of file
            {
                for (i = 0; bookPublication[i] != '\0' && st1[i] != '\0' && st1[i] == bookPublication[i]; i++) // for loop to match the student name from file and user
                    ;
                if (bookPublication[i] == '\0' && st1[i] == '\0') // if cond for end of student name
                {
                    heading("*** STUDENT FOUND **");
                    cont++;        // counter increment
                    if (cont == 1) // condtion to print the data on screen
                    {
                        cout << "\tStudent Name : " << bookAuthor << endl;
                        cout << "\tStudent's ID : " << bookPublication << endl;
                    }
                    cout << "\t"<< cont << ". "
                         << endl
                         << "\tBook Name : " << BookName << endl
                         << "\tBook's ID : " << bookID << endl
                         << "\tDate : " << q << "/" << B << "/" << p << endl;
                }
                intf.read((char *)this, sizeof(*this)); // reading the nxt data from the student file
            }
            getch();
            intf.close();                                     // close the student.txt file
            if (cont == 0)                                    // if condition for no record found in student.txt file
            {
                cout << "\n\n";
                print(CENTRE, "No Record Found", lineLength); // message
            }

            break;
        }
        case 4: // case for re - issue the book
        {
            heading("*** RE - ISSUE BOOK ***"); // printing the heading
            fflush(stdin);
            cout << "\tEnter Student's ID : "; // enter student name
            cin.getline(st, 50);
            cout << "\tEnter Book's ID : "; // enter book id
            cin.getline(st1, 20);
            cout << endl;
            fstream intf("student.txt", ios::in | ios::out | ios::ate | ios::binary); // opening the file student.txt file edit
            intf.seekg(0);                                                            // set the position of the next character to be extracted from the file
            intf.read((char *)this, sizeof(*this));                                   // reading the data from student.txt file
            while (!intf.eof())                                                       // checking the end of file
            {
                for (i = 0; bookID[i] != '\0' && st1[i] != '\0' && st1[i] == bookID[i]; i++) // for loop conditions for comparing the char of book ID
                    ;
                for (j = 0; bookPublication[j] != '\0' && st[j] != '\0' && st[j] == bookPublication[j]; j++) // for loop conctions for comparing the student ID
                    ;
                if (bookID[i] == '\0' && bookPublication[j] == '\0' && st[j] == '\0' && st1[i] == '\0') // if condition to check the end of book and student ID respectively
                {
                    d = q;
                    m = B;
                    y = p;
                    cout << "\n\tEnter New Date : "; // enter new date
                    cin >> q >> B >> p;
                    fine(d, m, y, q, B, p);                             // calling the fine function to ckeck for fine amount
                    intf.seekp(intf.tellp() - sizeof(*this));           // set the position of the pointer in the output sequence with the specified position
                    intf.write((char *)this, sizeof(*this));            // updating the data in student.txt file
                    cout << "\n\n";
                    print(CENTRE, "Re-Issue Successfully", lineLength); // successfull message
                    break;
                }
                intf.read((char *)this, sizeof(*this)); // reading the next data from the student.txt file
            }
            getch();
            intf.close(); // close the student.txt file
            break;
        }
        case 5: // case for returnig the book to library
        {
            heading("*** RETURN BOOK ***"); // printing the heading
            b = branch(2);                          // calliing the branch function to print the varioous branches and aassigning the return value to variable  b
            heading("*** RETURN BOOK ***"); // printing the heading
            fflush(stdin);
            cout << "\tEnter Book's ID : "; // enter book ID
            cin.getline(st1, 20);
            edit_bookStock(st1, b, 2);         // calling edit_bookStock() function to check the name of student in the student.txt file and editing the stock values of book in the booksdata.txt file
            cout << "\tEnter Student's ID : "; // enter student ID
            cin.getline(st, 20);
            cout << "\tEnter Present date : "; // enter present date
            cin >> d >> m >> y;
            ofstream outf("temp.txt", ios::app | ios::binary); // creating a temp.txt file to write the data in it
            ifstream intf("student.txt", ios::binary);         // opening the student.txt file to read
            intf.read((char *)this, sizeof(*this));            // reading the data from the student.txt file
            while (!intf.eof())                                // checking the end of file
            {
                for (i = 0; bookID[i] != '\0' && st1[i] != '\0' && st1[i] == bookID[i]; i++) // for loop conditions for comparing the char of book ID
                    ;
                for (j = 0; bookPublication[j] != '\0' && st[j] != '\0' && st[j] == bookPublication[j]; j++) // for loop conctions for comparing the student ID
                    ;
                if (bookID[i] == '\0' && bookPublication[j] == '\0' && st[j] == '\0' && st1[i] == '\0' && cont == 0) // if condition to check the end of book and student ID respectively
                {
                    cont++;                                                  //counter
                    intf.read((char *)this, sizeof(*this));                  // reading the data from the student.txt file
                    fine(q, B, p, d, m, y);                                  // calling the file function to check for file amount
                    cout << "\n\n";
                    print(CENTRE, "Book Returned Successfully", lineLength); // successfull messsage
                }
                else
                {
                    outf.write((char *)this, sizeof(*this)); // writing to temp.txt file
                    intf.read((char *)this, sizeof(*this));  // reading the nxt data from the student.txt file
                }
            }
            intf.close();                      // close the student.txt file
            outf.close();                      // close the temp.txt file
            getch();                           // pause the program
            remove("student.txt");             // delete the student.txt file from directory
            rename("temp.txt", "student.txt"); // rename the temp.txt to student.txt
            break;
        }
        case 9: // case for going back to librarian menu
        {
            librarianMenu(); // calling the librarian function to go back
            break;
        }
        default:
            cout << "\n\n";
            print(CENTRE, "INVALID INPUT!!! Try again... :(", lineLength); // error message
            getch();
            librarianMenu(); // going back to librarian menu
            break;
        }
    }
    void edit_bookStock(char st[], int b, int x) // function to edit the booksdata.txt for books quantity
    {
        int i, cont = 0;                                                            // declaring the required variables
        fstream intf("Booksdata.txt", ios::in | ios::out | ios::ate | ios::binary); // opening the booksdata.txt to edit
        intf.seekg(0);                                                              // set the position of the next character to be extracted from the file
        intf.read((char *)this, sizeof(*this));                                     // // reading the data from the booksdata.txt file
        while (!intf.eof())                                                         // checking the end of file
        {
            for (i = 0; b == B && bookID[i] != '\0' && st[i] != '\0' && st[i] == bookID[i]; i++) // for loop conditions for comparing the char of book ID
                ;
            if (bookID[i] == '\0' && st[i] == '\0') // if condition to check the end of book ID from file and user respectively
            {
                cont++;     // counter
                if (x == 1) // condition to remove the book from database (quantity)
                {
                    q--;
                }
                else // cindition to add book n database (quantity)
                {
                    q++;
                }
                intf.seekp(intf.tellp() - sizeof(*this)); // set the position of the pointer in the output sequence with the specified position
                intf.write((char *)this, sizeof(*this));  // updating the data in booksdata.txt file
                break;
            }
            intf.read((char *)this, sizeof(*this)); // reading the next data from the student.txt file
        }
        if (cont == 0) // if condition for no record found in student.txt file
        {
            cout << "\n\n";
            print(CENTRE, "No Record Found", lineLength); // message
            cout << "\nPress any key to continue.....";
            getch();      // pause program
            issue_book(); // calling the issue_book() function to repeat the operation again
        }
        intf.close(); // close the booksdata.txt file
    }
    void fine(int d, int m, int y, int dd, int mm, int yy) //funtion to fine the student for late deposite of issued book
    {
        long int n1, n2; // declaring the required variables
        int years, l, i;
        const int monthDays[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}; // array of months in a year
        n1 = y * 365 + d;
        for (i = 0; i < m - 1; i++)
            n1 += monthDays[i];
        years = y;
        if (m <= 2)
            years--;
        l = years / 4 - years / 100 + years / 400;
        n1 += l;
        n2 = yy * 365 + dd;
        for (i = 0; i < mm - 1; i++)
            n2 += monthDays[i];
        years = yy;
        if (m <= 2)
            years--;
        l = years / 4 - years / 100 + years / 400;
        n2 += l;
        n1 = n2 - n1;
        n2 = n1 - 15;
        if (n2 > 0)
            cout << "\n\tThe Total Fine is : " << n2;
    }
};

void MainMenu() // main menu function to drive the program further
{
    Homepage h;                         // homepage object
    Library l;                          // library oblject
    h.heading("*** CHOOSE OPTION ***"); // printing the heading
    int choice;
    cout << endl
         << "\t~ 1 >> Student" << endl           // option 1
         << "\t~ 2 >> Librarian" << endl         // option 2
         << "\t~ 3 >> Close Application" << endl // option 3
         << "\n>> Enter your Choice : ";
    cin >> choice;
    switch (choice)
    {
    case 1:
        l.studentMenu(); // calling the studentmenu function from library class
        break;
    case 2:
        l.authorization(); // calling the authorization function from library class
        break;
    case 3:
        exit(0); // close the application
    default:
        cout << "\n\n";
        l.print(l.LEFT, "\tPlease enter valid option :(", l.lineLength); // error message
        getch();
        MainMenu(); // calling again main menu function
    }
}
int main() // driver function
{
    MainMenu(); // calling the mainMenu function
    return 0;   // return 0 to ensure the proggram is successfully terminated
}

// end of program