// # Hotel-management-project-using-oops-concept-in-cpp

#include <bits/stdc++.h>
using namespace std ;
#define max 100 

//creating Customer class

class Customer
{
    public :
    char name[100] ;
    char address[100] ;
    char phone[12] ;
    char from_date[20] ;
    char to_date[20] ;
    float payment_advance ;
    int booking_id ;
};

//creating Room class

class Room
{
    public :
    char stype ;
    char ac ;
    int room_number ;
    int status ;
    int rent ;

    class Customer cust ;
    class Room Addroom(int rno) ;
    void Searchroom(int rno) ;
    void Displayroom(Room) ;
};

// declering rooms[max] and globalcount as global

class Room rooms[max] ;
int globalCount = 0 ;

//define Addroom() memberfunction to add rooms

Room Room::Addroom(int rno)
{
    class Room room ;
    room.room_number = rno ;
    cout<<"\nType Ac(y/n) :";
    cin>>room.ac ;
    cout<<"\nType room size(S/D) :" ;
    cin>>room.stype ;
    cout<<"\ndaily rent :" ;
    cin>>room.rent ;
    room.status = 0 ;

    cout<<"\nroom added successfully." ;
    return room ;
}

//define Searchroom() memberfunction to search rooms by room number

void Room::Searchroom(int rno)
{
    int i,found=0 ;
    for(i=0; i<globalCount; i++)
    {
        if(rooms[i].room_number == rno)
        {
            found = 1 ;
            break ;
        }
    }
    if(found == 1)
    {
        cout<<"\nroom details :" ;
        if(rooms[i].status == 1)
        {
            cout<<"\nroom is reserved." ;
        } 
        else
        {
            cout<<"\nroom is available." ;
        }
        Displayroom(rooms[i]) ;
    }
    else
    {
        cout<<"\nroom not found." ;
    }
}

//define Displayroom() memberfunction to diaply the room details

void Room::Displayroom(Room temproom)
{
    cout<<"\nroom number :" <<temproom.room_number ;
    cout<<"\nac :"<<temproom.ac ;
    cout<<"\nstype :"<<temproom.stype ;
    cout<<"\ndaily rent :"<<temproom.rent ;
}

//inherit class Hotelmngmt() from class Room() 

class Hotelmngmt : protected Room
{
    public :
    void Checkin() ;
    void Getavailroom() ;
    void Searchcustomer(char*p) ;
    void Checkout(int) ;
};

//define checkin() function for customer checkin details

void Hotelmngmt::Checkin()
{
    int i,found=0 ,rno ;
    class Room room ;

    cout<<"\nenter room number :" ;
    cin>>rno ;
    for(i=0 ; i<globalCount ; i++)
    {
        if(rooms[i].room_number == rno)
        {
            found = 1 ;
            break ;
        }
    }
    if(found == 1)
    {

        if(rooms[i].status == 1) 
        {
            cout<<"\nroom is already reserved." ;
            return ;
        }
        
        cout<<"\nenter booking id :" ;
        cin>>rooms[i].cust.booking_id ;
        cout<<"\nenter guest name :" ;
        cin>>rooms[i].cust.name ;
        cout<<"\nenter adress(only city) :" ;
        cin>>rooms[i].cust.address;
        cout<<"\nenter phone number :" ;
        cin>>rooms[i].cust.phone ;
        cout<<"\nenter from_date :" ;
        cin>>rooms[i].cust.from_date ;
        cout<<"\nenter to_date :" ;
        cin>>rooms[i].cust.to_date ;
        cout<<"\nenter advance payment :" ;
        cin>>rooms[i].cust.payment_advance ;

        rooms[i].status = 1 ;

        cout<<"\nguest checkin successfully." ;
    }

}

//define Getavailroom() function to get the available room details 

void Hotelmngmt::Getavailroom()
{
    int i,found = 0 ;
    for(i=0 ; i<globalCount ; i++)
    {
        if(rooms[i].status == 0)
        {
            Displayroom(rooms[i]) ;
            cout<<"\npress enter for next room ." ;
            found = 1 ;
        
        }
    }
    if(found == 0 )
    {
        cout<<"\nall rooms are reserved ." ;
    }
}

//define searchccustomer() function to search customer by name

void Hotelmngmt::Searchcustomer(char *pname)  
{  
    int i, found = 0;  
    for (i = 0; i < globalCount; i++)  
    {  
        if (rooms[i].status == 1 && strcmp(rooms[i].cust.name, pname) == 0)  
        {  
            cout << "\nCustomer Name: " << rooms[i].cust.name;  
            cout << "\nRoom Number: " << rooms[i].room_number;  
  
            cout << "\n\nPress enter for next record";  
            found = 1;        
        }  
    }  
    if (found == 0)  
    {  
        cout << "\nPerson not found.";   
    }  
} 

//define checkout function and it also generates bill 

void Hotelmngmt::Checkout(int roomNum)  
{  
    int i, found = 0, days, rno;  
    float billAmount = 0;  
    for (i = 0; i < globalCount; i++)  
    {  
        if (rooms[i].status == 1 && rooms[i].room_number == roomNum)  
        {    
            found = 1;  
            
            break;  
        }  
    }  
    if (found == 1)  
    {  
        cout << "\nEnter Number of Days:\t";  
        cin >> days;  
        billAmount = days * rooms[i].rent;  
  
        cout << "\n\t######## CheckOut Details ########\n";  
        cout << "\nCustomer Name : " << rooms[i].cust.name;  
        cout << "\nRoom Number : " << rooms[i].room_number;  
        cout << "\nAddress : " << rooms[i].cust.address;  
        cout << "\nPhone : " << rooms[i].cust.phone;  
        cout << "\nTotal Amount Due : " << billAmount << " /";  
        cout << "\nAdvance Paid: " << rooms[i].cust.payment_advance << " /";  
        cout << "\n*** Total Payable: " << billAmount - rooms[i].cust.payment_advance << "/ only";  
  
        rooms[i].status = 0;  
    } 
}

//create function managerooms to add or search rooms

void Managerooms()  
{  
    class Room room;  
    int opt, rno, i, flag = 0;  
    char ch;  
    do  
    {  
        system("cls");  
        cout << "\n### Manage Rooms ###";  
        cout << "\n1. Add Room";  
        cout << "\n2. Search Room";  
        cout << "\n3. Back to Main Menu";  
        cout << "\n\nEnter Option: ";  
        cin >> opt;  
  
        // switch statement  
        switch (opt)  
        {  
        case 1:  
            cout << "\nEnter Room Number: ";  
            cin >> rno;  
            i = 0;  
            for (i = 0; i < globalCount; i++)  
            {  
                if (rooms[i].room_number == rno)  
                {  
                    flag = 1;  
                }  
            }  
            if (flag == 1)  
            {  
                cout << "\nRoom Number is Present.\nPlease enter unique Number";  
                flag = 0;    
            }  
            else  
            {  
                rooms[globalCount] = room.Addroom(rno);  
                globalCount++;  
            }  
            break;  
        case 2:  
            cout << "\nEnter room number: ";  
            cin >> rno;  
            room.Searchroom(rno);  
            break;  
        case 3:  
            // nothing to do  
            break;  
        default:  
            cout << "\nPlease Enter correct option";  
            break;  
        }  
    } while (opt != 3);  
}  



int main()  
{  
    class Hotelmngmt hm;  
    int i, j, opt, rno;  
    char ch;  
    char pname[100];  
  
    do  
    {   
        cout << "######## Hotel Management #########\n";  
        cout << "\n1. Manage Rooms";  
        cout << "\n2. Check-In Room";  
        cout << "\n3. Available Rooms";  
        cout << "\n4. Search Customer";  
        cout << "\n5. Check-Out Room";    
        cout << "\n6. Exit";  
        cout << "\n\nEnter Option: ";  
        cin >> opt;  
        switch (opt)  
        {  
        case 1:  
            Managerooms();  
            break;  
        case 2:  
            if (globalCount == 0)  
            {  
                cout << "\nRooms data is not available.\nPlease add the rooms first.";  
            }  
            else  
                hm.Checkin();  
            break;  
        case 3:  
            if (globalCount == 0)  
            {  
                cout << "\nRooms data is not available.\nPlease add the rooms first.";    
            }  
            else  
                hm.Getavailroom();  
            break;  
        case 4:  
            if (globalCount == 0)  
            {  
                cout << "\nRooms are not available.\nPlease add the rooms first.";   
            }  
            else  
            {  
                cout << "Enter Customer Name: ";  
                cin >> pname;  
                hm.Searchcustomer(pname);  
            }  
            break;  
        case 5:  
            if (globalCount == 0)  
            {  
                cout << "\nRooms are not available.\nPlease add the rooms first.";   
            }  
            else  
            {  
                cout << "Enter Room Number : ";  
                cin >> rno;  
                hm.Checkout(rno);  
            }  
            break;  
        case 6:  
            cout << "\nTHANK YOU! FOR USING SOFTWARE";  
            break;  
        default:  
            cout << "\nPlease Enter correct option";  
            break;  
        }  
    } while (opt != 6);  
    
} 
