# super-market-billing-system
#include <iostream>
#include <fstream>
#include <vector>
#include <ctime>
#include <iomanip>
#include <sstream>
#include <cstdlib> // For rand() and srand()
#include <algorithm>
#include <utility>  // Needed for pair


using namespace std;



class shopping {
private:
    int pcode;
    float price;
    float dis;
    string pname;
    string category; // Added category
    int stock;       // Added stock
    time_t expiryDate; // Added expiry date

public:
    void menu();
    void administrator();
    void buyer();
    void buyFromMarket();
    void buyOnline();
    void add();
    void edit();
    void rem();
    void list();
	 void receipt(const vector<int>& arrc, const vector<int>& arrq);
    void filterByCategory();
    void manageStock();
    void checkout();
    string formatDate(time_t date);
    time_t parseDate(const string& dateStr);
};



void shopping::menu() {
    m:
    int choice;
    string email;
    string password;

    cout << "[1;32m" << "\t\t\t\t _________________________________________\n";
    cout << "[1;32m" << "\t\t\t\t|                                         |\n";
    cout << "[1;32m" << "\t\t\t\t|              Daily Shop                 |\n";
    cout << "[1;32m" << "\t\t\t\t|         Supermarket Main Menu           |\n";
    cout << "[1;32m" << "\t\t\t\t|_|\n";
    cout << "[1;32m" << "\t\t\t\t                                         \n";
    cout << "[1;32m" << "\t\t\t\t*\n";
    cout << "[1;32m" << "\t\t\t\t|            1.Admin              |\n";
    cout << "[1;32m" << "\t\t\t\t|            2.Buyer              |\n";
    cout << "[1;32m" << "\t\t\t\t|            3.Exit               |\n";
    cout << "[1;32m" << "\t\t\t\t*\n";
    cout << "[1;32m" << "\n\t\t\t\t Please select:";
    cin >> choice;

    switch (choice) {
        case 1:
            cout << "[1;32m" << "\t\t\t Please Login \n";
            cout << "[1;32m" << "\t\t\t Enter Email:  \n";
            cin >> email;
            cout << "[1;32m" << "\t\t\t Password     \n";
            cin >> password;

            if (email == "kkg2026@gmail.com" && password == "kkg") {
                administrator();
            } else {
                cout << "[1;32m" << "Invalid email/password";
            }
            break;
        case 2: {
            buyer();
            break;
        }
        case 3: {
            exit(0);
        }
        default: {
            cout << "[1;32m" << "Please select from the given options";
        }
    }
    goto m;
}

void shopping::administrator() {
    m:
    int choice;
    cout << "[1;32m" << "\n\n\n\t\t\t Administrator menu\n";
    cout << "[1;32m" << "\n\t\t\t|1. Add the product   |";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|2. Modify the product|";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|3. Delete the product|";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|4. List Products     |";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|5. Filter by Category|";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|6. Manage Stock      |";
    cout << "[1;32m" << "\n\t\t\t|                     |";
    cout << "[1;32m" << "\n\t\t\t|7. Back to main menu |";
    cout << "[1;32m" << "\n\n\t Please enter your choice";
    cin >> choice;

    switch (choice) {
        case 1:
            add();
            break;
        case 2:
            edit();
            break;
        case 3:
            rem();
            break;
        case 4:
            list();
            break;
        case 5:
            filterByCategory();
            break;
        case 6:
            manageStock();
            break;
        case 7:
            menu();
            break;
        default:
            cout << "[1;32m" << "Invalid choice!";
    }
    goto m;
}

void shopping::buyer() {
m:
    int choice;
    cout << "[1;32m" << "\t\t\t    Buyer Menu      \n";
    cout << "[1;32m" << "\t\t\t---------------------------------\n";
    cout << "[1;32m" << "\t\t\t 1. Buy from the Market\n";
    cout << "[1;32m" << "\t\t\t 2. Buy Online\n";
    cout << "[1;32m" << "\t\t\t 3. Go back\n";
    cout << "[1;32m" << "\t\t\t---------------------------------\n";
    cout << "[1;32m" << "\t\t\t Enter your choice: ";
    cin >> choice;

    switch (choice) {
        case 1:
            buyFromMarket();
            break;
        case 2:
            buyOnline();
            break;
        case 3:
            menu();
            return;
        default:
            cout << "[1;32m" << "Invalid choice, please try again.\n";
    }
    goto m;
}

void shopping::buyFromMarket() {
    list();
    vector<int> arrc;
    vector<int> arrq;
    int productCode, quantity;
    char addMore;

    do {
        cout << "[1;32m" << "Enter Product Code: ";
        cin >> productCode;
        cout << "[1;32m" << "Enter Quantity: ";
        cin >> quantity;

        arrc.push_back(productCode);
        arrq.push_back(quantity);

        cout << "[1;32m" << "Do you want to add another product? (y/n): ";
        cin >> addMore;
    } while (addMore == 'y' || addMore == 'Y');

    if (addMore == 'n' || addMore == 'N') {
        receipt(arrc, arrq); // Print receipt first
        // Payment and pickup instructions
        cout << "[1;32m" << "Payment Options: 1. Cash while receiving in market, 2. Online QR Code\n";
        int paymentOption;
        cin >> paymentOption;

        if (paymentOption == 2) {
            cout << "[1;32m" << "####################\n";
            cout << "[1;32m" << "# |||||||||||||||||#\n";
            cout << "[1;32m" << "# | | | | | | | | |#\n";
            cout << "[1;32m" << "#| | |  |  |  |  | #\n";
            cout << "[1;32m" << "#  | | | | | | | | #\n";
            cout << "[1;32m" << "# |  |  |  |  |  | #\n";
            cout << "[1;32m" << "# |||||||||||||||||#\n";
            cout << "[1;32m" << "####################\n";
            cout << "[1;32m" << "Transaction successful. Thank you for shopping!\n";
        }

        cout << "[1;32m" << "You can come and take your product between 10 AM to 8 PM.\n";
    }
}

void shopping::buyOnline() {
    list();
    vector<int> arrc;
    vector<int> arrq;
    int productCode, quantity;
    char addMore;
    string address;

    do {
        cout << "[1;32m" << "Enter Product Code: ";
        cin >> productCode;
        cout << "[1;32m" << "Enter Quantity: ";
        cin >> quantity;

        arrc.push_back(productCode);
        arrq.push_back(quantity);

        cout << "[1;32m" << "Do you want to add another product? (y/n): ";
        cin >> addMore;
    } while (addMore == 'y' || addMore == 'Y');

    if (addMore == 'n' || addMore == 'N') {
        cout << "[1;32m" << "Enter your address for delivery: ";
        cin.ignore();
        getline(cin, address);
        receipt(arrc, arrq); // Print receipt first

        // Payment and Delivery instructions
        cout << "[1;32m" << "Payment Options: 1. Cash on Delivery (COD), 2. Online QR Code\n";
        int paymentOption;
        cin >> paymentOption;

        if (paymentOption == 2) {
            cout << "[1;32m" << "####################\n";
            cout << "[1;32m" << "# |||||||||||||||||#\n";
            cout << "[1;32m" << "# | | | | | | | | |#\n";
            cout << "[1;32m" << "#| | |  |  |  |  | #\n";
            cout << "[1;32m" << "#  | | | | | | | | #\n";
            cout << "[1;32m" << "# |  |  |  |  |  | #\n";
            cout << "[1;32m" << "# |||||||||||||||||#\n";
            cout << "[1;32m" << "####################\n";
            cout << "[1;32m" << "Transaction successful. Thank you for shopping!\n";
        }

        cout << "[1;32m" << "Your order will be delivered in 4 to 5 days.\n";
    }
}

void shopping::receipt(const vector<int>& arrc, const vector<int>& arrq) { // Corrected
    fstream data;
    float total = 0;

    cout << "[1;32m" << "\n\n\t\t\t_____________________ RECEIPT _____________________\n";
    cout << "[1;32m" << "\nProduct No\t Product Name\t Quantity\tPrice\tAmount\tAmount with Discount\n";
    cout << "[1;32m" << "--------------------------------------------------------------------------\n";

    data.open("database.txt", ios::in);

    for (size_t i = 0; i < arrc.size(); i++) {
        data.clear();
        data.seekg(0, ios::beg);

        int pcode, stock;
        float price, dis;
        string pname, category, expiryStr;
        bool found = false;

        while (data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr) {
            if (pcode == arrc[i]) {
                float amount = price * arrq[i];
                float discount = amount - (amount * dis / 100);
                cout << "[1;32m" << pcode << "\t\t" << pname << "\t\t" << arrq[i] << "\t\t"
                     << price << "\t" << amount << "\t\t" << discount << endl;
                total += discount;
                found = true;
                break;
            }
        }

        if (!found) {
            cout << "[1;32m" << "\nError: Product code " << arrc[i] << " not found!";
        }
    }
    data.close();

    cout << "[1;32m" << "\n\n----------------------------------------------\n";
    cout << "[1;32m" << "Total Amount: " << total << endl;
}



void shopping::add() {
    fstream data;
    int c, st;
    float p, d;
    string n, cat, expiryStr;

    cout << "[1;32m" << "\n\n\t\t\t Add new product";
    cout << "[1;32m" << "\n\n\t Product code of the product: ";
    cin >> pcode;
    cout << "[1;32m" << "\n\n\t Name of the product: ";
    cin.ignore();
    getline(cin, pname);
    cout << "[1;32m" << "\n\n\t Price of the product: ";
    cin >> price;
    cout << "[1;32m" << "\n\n\t Discount on product (%): ";
    cin >> dis;
    cout << "[1;32m" << "\n\n\t Category of the product: ";
    cin.ignore();
    getline(cin, category);
    cout << "[1;32m" << "\n\n\t Stock of the product: ";
    cin >> stock;
    cout << "[1;32m" << "\n\n\t Expiry Date (YYYY-MM-DD): ";
    cin >> expiryStr;

    data.open("database.txt", ios::app);  // ? Append mode
    if (!data) {
        cout << "[1;32m" << "\n\nError: Unable to open database.txt!";
        return;
    }

    // ? Write new product data
    data << pcode << " " << pname << " " << price << " " << dis << " " 
         << category << " " << stock << " " << expiryStr << "\n";
    data.close();

    cout << "[1;32m" << "\n\n\t\t Record inserted successfully!";
}


void shopping::edit() {
    fstream data, data1;
    int pkey;
    int token = 0;
    int c;
    float p;
    float d;
    string n;
    string cat;
    int st;
    string expiryStr;

    cout << "[1;32m" << "\n\t\t\t Modify the record";
    cout << "[1;32m" << "\n\t\t\t Product code:";
    cin >> pkey;

    data.open("database.txt", ios::in);
    if (!data) {
        cout << "[1;32m" << "\n\nFile doesn't exist!";
    } else {
        data1.open("database1.txt", ios::app | ios::out);

        data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        while (!data.eof()) {
            if (pkey == pcode) {
                cout << "[1;32m" << "\n\t\t Product new code:";
                cin >> c;
                cout << "[1;32m" << "\n\t\t Name of the product :";
                cin.ignore(); getline(cin, n);
                cout << "[1;32m" << "\n\t\t Price :";
                cin >> p;
                cout << "[1;32m" << "\n\t\t Discount :";
                cin >> d;
                cout << "[1;32m" << "\n\t\t Category :";
                cin.ignore(); getline(cin, cat);
                cout << "[1;32m" << "\n\t\t Stock :";
                cin >> st;
                cout << "[1;32m" << "\n\t\t Expiry Date (YYYY-MM-DD):";
                cin >> expiryStr;
                expiryDate = parseDate(expiryStr);

                data1 << " "<< c << " " << n << " " << p << " " << d << " " << cat << " " << st << " " << formatDate(expiryDate) << "\n";
                cout << "[1;32m" << "\n\n\t\t Record edited";
                token++;
            } else {
                data1 << " " << pcode << " " << pname << " " << price << " " << dis << " " << category << " " << stock << " " << formatDate(expiryDate) << "\n";
            }
            data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        }

        data.close();
        data1.close();

        remove("database.txt");
        rename("database1.txt", "database.txt");

        if (token == 0) {
            cout << "[1;32m" << "\n\n Record not found sorry!";
        }
    }
}

void shopping::rem() {
    fstream data, data1;
    int pkey;
    int token = 0;
    cout << "[1;32m" << "\n\n\t Delete product";
    cout << "[1;32m" << "\n\n\t Product code:";
    cin >> pkey;
    data.open("database.txt", ios::in);
    if (!data) {
        cout << "[1;32m" << "File doesnt exist";
    } else {
        data1.open("database1.txt", ios::app | ios::out);
        string expiryStr;
        data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        while (!data.eof()) {
            if (pcode == pkey) {
                cout << "[1;32m" << "\n\n\t Product deleted succes";
                token++;
            } else {
                data1 << " " << pcode << " " << pname << " " << price << " " << dis << " " << category << " " << stock << " " << expiryStr << "\n";
            }
            data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        }
        data.close();
        data1.close();
        remove("database.txt");
        rename("database1.txt", "database.txt");
        if (token == 0) {
            cout << "[1;32m" << "\n\n Record not found";
        }
    }
}

void shopping::list() {
    fstream data;
    data.open("database.txt", ios::in);

    if (!data) {
        cout << "[1;32m" << "Error: Could not open file!" << endl;
        return;
    }

    cout << "[1;32m" << "\n\n|_|\n";
    cout << "[1;32m" << left << setw(10) << "PCode" 
         << setw(20) << "Name" 
         << setw(10) << "Price"
         << setw(10) << "Discount"
         << setw(15) << "Category" 
         << setw(10) << "Stock" 
         << setw(15) << "Expiry Date" << endl;
    cout << "[1;32m" << "|_|\n";

    string line;
    while (getline(data, line)) {
        stringstream ss(line);
        int pcode, stock;
        float price, discount;
        string pname, category, expiryStr;

        ss >> pcode >> pname >> price >> discount >> category >> stock >> expiryStr;

        if (!ss.fail()) { // Ensure valid data
            cout << "[1;32m" << left << setw(10) << pcode
                 << setw(20) << pname
                 << setw(10) << price
                 << setw(10) << discount
                 << setw(15) << category
                 << setw(10) << stock
                 << setw(15) << expiryStr << endl;
        }
    }

    data.close();
}


void shopping::filterByCategory() {
    fstream data;
    string searchCategory;
    cout << "[1;32m" << "\n\n\t Enter category to filter: ";
    cin.ignore(); getline(cin, searchCategory);
    data.open("database.txt", ios::in);
    cout << "[1;32m" << "\n\n|\n";
    cout << "[1;32m" << "ProNo\t\tName\t\tPrice\t\tCategory\tStock\t\tExpiry\n";
    cout << "[1;32m" << "\n\n|\n";
    string expiryStr;
    data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
    while (!data.eof()) {
        if (category == searchCategory) {
            cout << "[1;32m" << pcode << "\t\t" << pname << "\t\t" << price << "\t\t" << category << "\t\t" << stock << "\t\t" << expiryStr << "\n";
        }
        data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
    }
    data.close();
}

void shopping::manageStock() {
    fstream data, data1;
    int pkey;
    int newStock;
    int token = 0;
    cout << "[1;32m" << "\n\n\t Manage Stock";
    cout << "[1;32m" << "\n\n\t Product code:";
    cin >> pkey;
    cout << "[1;32m" << "\n\n\t New Stock:";
    cin >> newStock;
    data.open("database.txt", ios::in);
    if (!data) {
        cout << "[1;32m" << "File doesnt exist";
    } else {
        data1.open("database1.txt", ios::app | ios::out);
        string expiryStr;
        data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        while (!data.eof()) {
            if (pcode == pkey) {
                stock = newStock;
                data1 << " " << pcode << " " << pname << " " << price << " " << dis << " " << category << " " << stock << " " << expiryStr << "\n";
                cout << "[1;32m" << "\n\n\t Stock updated successfully";
                token++;
            } else {
                data1 << " " << pcode << " " << pname << " " << price << " " << dis << " " << category << " " << stock << " " << expiryStr << "\n";
            }
            data >> pcode >> pname >> price >> dis >> category >> stock >> expiryStr;
        }
        data.close();
        data1.close();
        remove("database.txt");
        rename("database1.txt", "database.txt");
        if (token == 0) {
            cout << "[1;32m" << "\n\n Record not found";
        }
    }
}

string shopping::formatDate(time_t date) {
    char buffer[80];
    struct tm tmstruct;
    localtime_r(&date, &tmstruct);
    strftime(buffer, sizeof(buffer), "%Y-%m-%d", &tmstruct);
    return string(buffer);}

time_t shopping::parseDate(const string& dateStr) {
    struct tm tmstruct = {0};
    int year, month, day;
    char dash1, dash2;

    stringstream ss(dateStr);
    ss >> year >> dash1 >> month >> dash2 >> day;

    if (ss.fail() || dash1 != '-' || dash2 != '-') {
        cerr << "Invalid date format. Please use YYYY-MM-DD." << endl;
        return time(0); // Return current time on error
    }

    tmstruct.tm_year = year - 1900;
    tmstruct.tm_mon = month - 1;
    tmstruct.tm_mday = day;   
    tmstruct.tm_hour = 0;
    tmstruct.tm_min = 0;
    tmstruct.tm_sec = 0;

    return mktime(&tmstruct);
}

int main() {
    shopping s;
    s.menu();
    return 0;
}
