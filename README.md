#include <iostream>
#include <cstdlib>
#include <chrono>
#include <thread>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>
#include <fstream> 
#include <random>


using namespace std;

// Menu functions
void learn();
void quiz();
void miniGames();
void rewards();
void exitProgram();

// learn functions
void datalearn();
void infolearn();
void rizallearn();
void discretelearn();
void stslearn();

//quiz function
void dataquiz();
void infoquiz();
void rizalquiz();
void discretequiz();
void stsquiz();

// mini game function
void wscramble();
void tictactoe();
void rockpaperscissor();

// tic tac toe
void tttoevscom();
void tttoe2pl();

void clearScreen() {
#ifdef _WIN32
system("cls");
#else
system("clear");
#endif
}

void loading() {
    cout <<"\n\n\n\n\n\n\n\n\n\n";
cout << "\t\t\t ";
cout << "Loading";
for (int i = 0; i < 5; i++) {
cout << ".";
cout.flush();
this_thread::sleep_for(chrono::milliseconds(500));
}

}

void exiting() {
    cout <<"\n\n\n\n\n\n\n\n\n\n";
cout << "\t\t\t ";
cout << "Exiting";
for (int i = 0; i < 5; i++) {
cout << ".";
cout.flush();
this_thread::sleep_for(chrono::milliseconds(500));
}

}

void checking() {
    cout <<"\n\n\n\n\n\n\n\n\n\n";
cout << "\t\t\t ";
cout << "Checking";
for (int i = 0; i < 5; i++) {
cout << ".";
cout.flush();
this_thread::sleep_for(chrono::milliseconds(500));
}
}

void opening() {
    cout <<"\n\n\n\n\n\n\n\n\n\n";
cout << "\t\t\t ";
cout << "Opening the System";
for (int i = 0; i < 5; i++) {
cout << ".";
cout.flush();
this_thread::sleep_for(chrono::milliseconds(500));
}
}
void typewriter(string text, int delay_ms = 30) {
    for (char c : text) {
        cout << c << flush;
        this_thread::sleep_for(chrono::milliseconds(delay_ms));
    }
    cout << endl;
}


int points = 0;
int stars = 0;
bool WordScrambleUnlocked = false;
bool TicTacToeUnlocked = false;
bool RockPaperScissorsUnlocked = false;
bool hasReadData = false;
bool hasReadInfo= false;
bool hasReadRizal = false;
bool hasReadDiscrete= false;
bool hasReadSTS= false;
bool passeddata=false;
bool passedinfo=false;
bool passedrizal=false;
bool passeddiscrete=false;
bool passedsts=false;

// Function to convert points to stars (2 points = 1 star)
void convertPointsToStars() {
if (points >= 2) {
int convertibleStars = points / 2;
cout << "You have " << points << " points. You can convert to " << convertibleStars << " stars.\n";
cout << "How many stars do you want to convert? (Enter 0 to cancel): ";
int convertAmount;
cin >> convertAmount;
if (convertAmount > 0 && convertAmount <= convertibleStars) {
stars += convertAmount;
points -= convertAmount * 2;
cout << "Converted! You now have " << stars << " stars and " << points << " points.\n";
} else if (convertAmount > convertibleStars) {
cout << "\033[3;1;91mNot enough points!\033[0m\n";
}
} else {
cout << "\033[3;1;91mNot enough points to convert (need at least 2).\033[0m\n";
}
cout << "\nPress Enter to go back...";
    cin.ignore(); 
    cin.get();    
    clearScreen();
}

// Function to check and unlock mini games
void checkUnlocks() {
    cout<<"\033[3;1;92m";
if (stars >= 5 && !WordScrambleUnlocked) {
WordScrambleUnlocked = true;
cout << "Unlocked: Word Scramble!\n";
stars -= 5;
}
if (stars >= 15 && !TicTacToeUnlocked) {
TicTacToeUnlocked = true;
cout << "Unlocked: Tic Tac Toe!\n";
stars -= 15;
}
if (stars >= 25 && !RockPaperScissorsUnlocked) {
RockPaperScissorsUnlocked = true;
cout << "Unlocked: Rock Paper Scissors!\n";
stars -= 25;
cout<<"\033[0m";
}
}

void saveProgress() {
    ofstream file("progress.txt");
    if (file.is_open()) {
        file << points << endl;
        file << stars << endl;
        file << hasReadData<< endl;
        file << hasReadSTS<< endl;
        file<< hasReadDiscrete<< endl;
        file << hasReadRizal<< endl;
        file << hasReadInfo<< endl;
        file << passedsts << endl;
        file << passeddiscrete << endl;
        file << passedrizal << endl;
        file << passedinfo << endl;
        file << passeddata << endl;
        file << WordScrambleUnlocked << endl;
        file << TicTacToeUnlocked << endl;
        file << RockPaperScissorsUnlocked << endl;
        file.close();
        cout << "\033[3;1;92mProgress saved successfully!\033[0m\n";
    } else {
        cout << "\033[3;1;91mError saving progress.\033[0m\n";
    }
}

void loadProgress() {
    ifstream file("progress.txt");
    if (file.is_open()) {
        file >> points;
        file >> stars;
        file >> hasReadData;
        file >> hasReadSTS;
        file >> hasReadDiscrete;
        file >> hasReadRizal;
        file >> hasReadInfo;
        file >> passeddata;
        file >> passedinfo;
        file >> passedrizal;
        file >> passeddiscrete;
        file >> passedsts;
        file >> WordScrambleUnlocked;
        file >> TicTacToeUnlocked;
        file >> RockPaperScissorsUnlocked;
        file.close();
        string texts[] = {"\033[3;1;92mProgress loaded successfully!\033[0m\n"
        };
        for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}
    } else {
        string texts[] = {"\033[3;1;91mNo previous progress found. Starting fresh.\033[0m\n"
        };
        for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}
    }
}

int main() {
    opening();
    clearScreen();
    cout <<"\n\n\n\n\n\n\n\n\n\n";
cout << "\t\t\t ";
    string texts[] = { "WELCOME IN BRAINBATTLE!\n", "A sytem to train your brain, beat the quizzes and unlock the fun"
    };
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}
cout << "\nPress Enter to start...";
    cin.ignore(); 
    cin.get();   
clearScreen();
    loadProgress();
    clearScreen();
int choice;
do {
cout<<"\033[1;33m====================\t";
      cout << "MAIN MENU\t";
             cout<< "====================\033[0m\n";
cout << "\033[7mPoints: " << points << " | Stars: " << stars << "\n\n\033[0m";
cout << "\033[36m1. Learn\n";
cout << "2. Quiz\n";
cout << "3. Mini Games\n";
cout << "4. Rewards\n";
cout << "5. Exit\n";
cout << "Enter your choice: ";
cin >> choice;
cout<<"\033[0m";
clearScreen();

if (choice != 5) {
loading();
clearScreen();
}

else {
exiting();
clearScreen();
}

if(cin.fail()) { 
        cin.clear(); 
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
        cout << "\033[3;1;90mInvalid choice!\033[0m\n";
        cout << "\nPress Enter to go back...";
        cin.get();
        clearScreen();
        continue; 
    }

switch(choice) {  
        case 1:  
            learn();  
            break;  
        case 2:  
            quiz();  
            break;  
        case 3:  
            miniGames();  
            break;  
        case 4:  
            rewards();  
            break;  
        case 5:  
            exitProgram();  
            break;  
        default:  
            cout << "\033[3;1;90mInvalid choice! Please try again.\n";  
            cout << "\nPress Enter to go back...\033[0m";
    cin.ignore(); 
    cin.get();    
    clearScreen();
    
    }  
} while(choice != 5);  
  
return 0;

}


void learn() {
int choice;
do {
cout<<"\033[1;35m====================\t";
      cout << "LEARN SECTION\t";
             cout<<"====================\n\033[0m";
cout << "\033[36m1. Data Structures\n";
cout << "2. Information Management\n";
cout << "3. Rizal\n";
cout << "4. Discrete Math\n";
cout << "5. STS\n";
cout << "6. Back to Main Menu\n";
    cout << "Enter your choice: ";
    cin >> choice;
    cout<<"\033[0m";
    clearScreen();
    loading();
    clearScreen();

    if(cin.fail()) { 
        cin.clear(); 
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
        cout << "\033[3;31mInvalid choice!\n";
        cout << "\nPress Enter to go back...\033[0m";
        cin.get();
        clearScreen();
        continue; 
    }

    switch(choice) {  
        case 1:  
            datalearn();  
            break;  
        case 2:  
            infolearn();  
            break;  
        case 3:  
            rizallearn();  
            break;  
        case 4:  
            discretelearn();  
            break;  
        case 5:  
            stslearn();  
            break;  
        case 6:  
            return;  
        default:  
            cout << "\033[3;1;91mInvalid choice!\n";  
            cout << "\nPress Enter to go back...\033[0m";
            cin.ignore();
            cin.get();    
            clearScreen();
    }  
} while(choice != 6);
}

void datalearn() {
    clearScreen(); 
    cout<<"\033[1;32m====================\t";
      cout << "DATA STRUCTURE\t";
             cout<< "====================\n\033[0m";
             string texts[] = { "Definition:\n",
     "A Data Structure is a way of storing and organizing data in a computer\n", "so that it can be used efficiently. It helps programmers make\n", "algorithms faster and more reliable.\n\n", "Common Types:\n", "1. Array - Stores elements of the same type in contiguous memory.\n", "2. Linked List - A series of nodes connected by pointers.\n",
    "3. Stack - Follows Last In, First Out (LIFO).\n",
    "4. Queue - Follows First In, First Out (FIFO).\n", 
    "5. Tree - A hierarchical structure with nodes.\n", 
    "6. Graph - Collection of nodes and edges.\n", 
    "7. Hash Table - Stores key-value pairs for quick access.\n\n", 
    "Importance of Data Structures:\n", 
    "- Helps in efficient data access and storage.\n", 
    "- Makes algorithms faster and simpler.\n", 
"- Used in databases, operating systems, and networking.\n", 
    "- Reduces complexity and improves performance.\n\n"
                 
             };
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}

    
    
    if (!hasReadData){
    cout << "\033[3;1;92mYou earned +5 point! Current Points: " << points << "\n\033[0m";
    points += 5;
    hasReadData=true;

    }
    else{
        cout<< "\033[3;1;91mNo more points added after first read!\033[0m";
    }

    cout << "\nPress Enter to go back...";
    cin.ignore(); 
    cin.get();    
    clearScreen();
}
void infolearn() {
    clearScreen();
    cout<<"\033[1;94m====================\t";
      cout << "INFORMATION MANAGEMENT\t";
             cout<< "====================\033[0m\n";

    string texts[] = { 
    "1. Data vs Information:\n",
     "- Data: Raw, unprocessed facts (numbers, names, measurements).\n",
    "- Information: Processed and organized data that has meaning.\n\n",

    "2. Metadata:\n",
    "- Metadata is data that describes other data.\n",
    "  Example: Author of a file, creation date, keywords.\n\n", 

     "3. Database Management System (DBMS):\n", 
     "- A software used to create, organize, and manage databases.\n", 
    "  Examples: MySQL, Oracle, SQL Server, PostgreSQL.\n\n", 
    "4. Data Integrity:\n", 
     "- Ensuring that data in a database is accurate, consistent, and reliable.\n\n",
"5. Data Integration:\n",
    "- The process of combining data from different sources into a unified dataset.\n\n",
"6. Normalization:\n",
     "- The process of organizing data to reduce redundancy (duplication).\n\n",
"7. SQL Data Types:\n", 
    "- INT: Whole numbers (e.g., 1, 10)\n", 
     "- VARCHAR: Text (e.g., \"Hello\")\n", 
    "- DECIMAL: Decimal numbers (e.g., 3.14)\n", 
    "- DATE: Dates (e.g., 2023-11-15)\n\n", 
"8. Aggregate Functions:\n", 
    "- COUNT(): Counts the number of rows\n", 
    "- SUM(): Adds all values\n",
    "- AVG(): Computes average\n",
    "- MAX(): Largest value\n", 
    "- MIN(): Smallest value\n\n",

    "9. Single-user vs Multi-user databases:\n", 
     "- Single-user: Only one user can access database at a time.\n", 
    "- Multi-user: Multiple users can use database at the same time.\n\n"
    };
    
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}
    
    
    
    if (!hasReadInfo){
    cout << "\033[3;1;92mYou earned +5 point! Current Points: " << points << "\033[0m\n";
    points += 5;
    hasReadInfo=true;
    }
    else{
        cout<< "\033[3;1;91mNo more points added after first read!\033[0m";
    }

    
    cout << "\nPress Enter to go back...";
    cin.ignore(); 
    cin.get();    
    clearScreen();
}


void rizallearn() {
    clearScreen();
    cout<<"\033[1;34m====================\t";
      cout << "RIZAL\t";
             cout<< "====================\033[0m\n";

    string texts[] = {
         "Birth and Early Life:\n", 
    "- Jose Rizal was born on June 19, 1861, in Calamba, Laguna.\n", 
    "- He grew up in a loving and educated family.\n", 
    "- He studied in Biñan and Manila, showing exceptional intelligence.\n\n", 

    " Education and Studies Abroad:\n",
     "- Rizal went to Europe to continue his studies due to discrimination at UST.\n",
     "- He studied medicine, philosophy, arts, and humanities.\n\n",

    "Literary Works:\n",
     "1. Noli Me Tangere (1887) - Exposed social injustices.\n",
    "2. El Filibusterismo (1891) -Continued advocacy for reforms.\n",
    "3. Mi Último Adiós (1896) - Poem written before his execution.\n",
    "- Also wrote poems, essays, and letters promoting patriotism.\n\n",

     "Reform Movements:\n",
     "- Joined the Propaganda Movement in Europe.\n",
    "- Founded La Liga Filipina in 1892 to promote unity and education.\n\n",

     "Exile and Later Life:\n",
    "- Rizal was exiled to Dapitan from 1892 to 1896.\n",
     "- In Dapitan, he taught, practiced medicine, and worked on community projects.\n\n",

     "Death and Legacy:\n",
    "- Rizal was executed on December 30, 1896, in Luneta, Manila.\n", 
     "- His writings inspired nationalism and independence.\n", 
    "- December 30 is celebrated as Rizal Day.\n\n"
    };
    
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}

    
    
    if (!hasReadRizal){
    cout << "\033[3;1;92mYou earned +5 point! Current Points: " << points << "\033[0m\n";
    points += 5;
    hasReadRizal=true;
    }
    else{
        cout<< "\033[3;1;91mNo more points added after first read!\033[0m";
    }

    cout << "\nPress Enter to go back...";
    cin.ignore(); 
    cin.get();    
    clearScreen();
}

void discretelearn() {
    clearScreen();
    cout<<"\033[1;95m====================\t";
      cout << "DISCRETE MATH\t";
             cout<< "====================\033[0m\n";

    string texts[] = {
         "Relation:\n",
    "A relation is a set of ordered pairs connecting elements from one set (domain) to another (range).\n",
    "Example: {(1,2), (2,3), (3,4)}\n\n",

     "Function:\n",
     "A function is a relation where each input has exactly one output.\n"
     "Example: {(1,2), (2,3), (3,4)} - Valid Function\n", 
    "Non-example: {(1,2), (2,3), (1,3)} - Not a function\n\n", 

     "Sequence:\n", 
    "An ordered list of numbers.\n",
    "- Arithmetic: difference between terms is constant (d).\n", 
     "  Example: 3, 7, 11, 15 (d = 4)\n",
     "- Geometric: multiplied by constant ratio (r).\n", 
    "  Example: 3, 6, 12, 24 (r = 2)\n\n",

     "Binary Numbers:\n",
    "Binary uses only 0s and 1s.\n"
    "Example: 1010 is valid; 234 is NOT binary.\n\n", 

    "Proposition:\n", 
    "A statement that is either TRUE or FALSE, but not both.\n",
    "Example of True: 2 + 2 = 4\n",
     "Example of False: The sky is green\n\n",

     "Truth Table:\n", 
     "Shows all possible inputs and outputs of logical operations.\n", 
    "Useful in logic and designing circuits.\n\n"
    };
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}

    
    
    if (!hasReadDiscrete){
    cout << "\033[3;1;92mYou earned +5 point! Current Points: " << points << "\033[0m\n";
    points += 5;
    hasReadDiscrete=true;
    }
    else{
        cout<< "\033[3;1;91mNo more points added after first read!\033[0m";
    }

    cout << "\nPress Enter to go back...";
    cin.ignore(); 
    cin.get();    
    clearScreen();
}

void stslearn() {
    clearScreen();
    cout<<"\033[1;93m ====================\t";
      cout << "STS\t";
             cout<< "====================\033[0m\n";

    string texts[] = {
        "Main Goal of Science:\n",
    "- To understand the natural world through observation and reasoning.\n\n", 

    "Technology:\n", 
     "- The application of scientific knowledge to solve problems.\n\n", 

    "Positive Effects of Technology:\n", 
     "- Faster communication, access to education, medical advances.\n\n", 

     "Society's Influence on Science and Technology:\n", 
    "- Society creates needs and challenges that drive innovation.\n\n", 

     "Ethical Issues in Technology:\n", 
       "- Data privacy, responsible AI use, environmental responsibility.\n\n", 

    "Relationship Between Science and Technology:\n", 
    "- Science discovers principles; technology applies them.\n\n", 

    "Examples of Technology Improving Life:\n", 
    "- Printing press, medical devices, transportation.\n\n",

     " Negative Effects of Technology:\n", 
    "- Pollution, deforestation, resource overuse.\n\n", 

    " Responsible Use of Technology:\n", 
    "- Using it to help others and protect nature.\n\n", 

     " Importance of STS:\n", 
    "- Helps people make responsible decisions about science and technology.\n\n"
    };
    
    for (int i = 0; i < sizeof(texts)/sizeof(texts[0]); i++) {
    typewriter(texts[i], 30);
}

    
    
    if (!hasReadSTS){
    cout << "\033[3;1;92mYou earned +5 point! Current Points: " << points << "\033[0m\n";
    points += 5;
    hasReadSTS=true;
    }
    else{
        cout<< "\033[3;1;91mNo more points added after first read!\033[0m";
    }

    cout << "\nPress Enter to go back...";
   cin.ignore(); 
    cin.get();    
    clearScreen();;
}

void quiz() {
int choice;
do {
cout<<"\033[1;37m====================\t";
      cout << "QUIZ SECTION\t";
             cout<< "====================\n\033[0m";
cout << "\033[39m1. Data Structures Quiz\n";
cout << "2. Information Management Quiz\n";
cout << "3. Rizal Quiz\n";
cout << "4. Discrete Math Quiz\n";
cout << "5. STS Quiz\n";
cout << "6. Back to Main Menu\n";
cout << "Enter your choice: ";
cin >> choice;
cout << "\033[0m";
clearScreen();
loading();
clearScreen();

if(cin.fail()) { 
        cin.clear(); 
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
        cout << "Invalid choice!\n";
        cout << "\nPress Enter to go back...";
        cin.get();
        clearScreen();
        continue; 
    }

switch(choice) {  
        case 1:  
            dataquiz();  
            break;  
        case 2:  
            infoquiz();  
            break;  
        case 3:  
            rizalquiz();  
            break;  
        case 4:  
            discretequiz();  
            break;  
        case 5:  
            stsquiz();  
            break;  
        case 6:  
            return;  
        default:  
            cout << "Invalid choice!\n";  
            system("pause");  
    }  
} while(choice != 6);

}

void dataquiz() {
    if(passeddata){
        cout<< "\033[3;1;91m\n\n\n\n\nYou already passed this quiz!";
        cout<<"You cannot take this quiz again!\n";
        cout << "\nPress Enter to go back...\033[0m";
    cin.ignore(); 
    cin.get();    
    clearScreen();
    return;
    }
    
    int score = 0;
    char answer;

    cout<<"\033[1;91m====================\t";
      cout << "DATA STRUCTURES QUIZ\t";
             cout<< "====================\033[0m\n";

    cout << "1. Which data structure follows LIFO?\n";
    cout << "A. Queue\nB. Stack\nC. Array\nD. Tree\nYour answer: ";
    cin >> answer;
    if (toupper(answer) == 'B') score++;
    

    cout << "\n2. Which allows adding/removing only at one end?\n";
    cout << "A. Stack\nB. Queue\nC. Linked List\nD. Graph\nYour answer: ";
    cin >> answer;
    if (toupper(answer) == 'A') score++;
    

    cout << "\n3. Best for hierarchical relationships?\n"
