
# Demo


//library management system it can update by number(ISBN)
#include <iostream>
#include<fstream>

#include<cstring>
#include <cstdlib>
#include<iomanip>
const int size=2;
using namespace std;
struct Book
{
    char title[20];
    char author[20];
    int bn;
};
void write(Book b[],int size);
void display();
void menu();
void searchh_by_number(int bn);
void searchh_by_title(char title[],int sizee);
void searchh_by_author(char author[],int sizee);
void update_by_number(int bn);
void deletee_by_number(int bn);
void intro();

int main()
{

    system("color 4A");
    intro();
    system("cls");
    menu();
    int choice;
    cout<<"enter your choice: ";
    cin>>choice;
    system("cls");
 while(choice!=0)
    {

    switch(choice)
    {

    case 1:
      {

       Book b[2];
        cout<<"enter the information: \n";
        for(int i=0; i<2; i++)
        {
            cout<<"enter the title: \n";
            cin.ignore();
            cin.getline(b[i].title,20);
            cout<<"enter the author: \n";
            cin.ignore();
            cin.getline(b[i].author,20);
            cout<<"enter the book number: \n";
           cin>>b[i].bn;
           
        }
        write(b,2);
        break;
      }
    case 2:
        display();
        
        break;
    case 3:
        int bn;
        cout<<"enter the book number: ";
        cin.ignore();
        cin>>bn;
        searchh_by_number(bn);

        break;
    case 4:
        char title[20];
        cout<<"enter the book title: ";
        cin.ignore();
        cin.getline(title,20);
        searchh_by_title(title,20);

        break;
    case 5:
     char author[20];
        cout<<"enter the author: ";
        cin.ignore();
        cin.getline(author,20);
        searchh_by_author(author,20);

        break;
    case 6:
        cout<<"enter a number to search and update: \n";
        cin>>bn;
        update_by_number(bn);

        break;

    case 7:
      cout<<"enter a number to search and delete: \n";
        cin>>bn;
        deletee_by_number(bn);

        break;
      default:cout<<"wrong choice"<<endl;
     
     }
     cout<<"Enter your choice again"<<endl;
cin>>choice;
}
return 0;
}

void write(Book b[],int size)
{
    ofstream out("data.txt",ios::app);
    for(int i=0; i<size; i++)
    out.write((char*)&b[i],sizeof(b[i]));
}

void display()

{
    ifstream in("data.txt");
    Book b;
    in.read((char*)&b,sizeof(b));
   
    
    cout<<"\n\n Information about the book\n\n";
    cout<<"================================================================\n";

    cout<<" Title           Author          ISBN\n";
    cout<<"================================================================\n";
     
    while(!in.eof())
    {
        cout<<b.title<<setw(10)<<""<<b.author<<setw(10)<<" "<<b.bn<<setw(6)<<" "<<endl;
        cout<<endl;
        

        in.read((char*)&b,sizeof(b));
       
    }
    in.close();
}
void menu()
{
    cout<<"\t\tMENU\t\t\n";
    cout<<"enter 1 to write to the file \n";
    cout<<"enter 2 to read(display) from file \n";
    cout<<"enter 3 to search book by it's number\n";
    cout<<"enter 4 to search book by title\n";
    cout<<"enter 5 to search book by author\n";
    cout<<"enter 6 to update book by number\n";
    cout<<"enter 7 to delete book by number\n\n\n";
}

void searchh_by_number(int bn)
{
    Book b;
    ifstream in("data.txt");

    int flag=0;
    in.read((char*)&b,sizeof(b));
    while(!in.eof())
    {
        if(bn==b.bn)
        {
            flag=1;
            break;
        }
        in.read((char*)&b,sizeof(b));
    }
    if(flag==1)
    {
        cout<<"the book is found!\n\n\n";
        cout<<"Book title:  "<<b.title<<endl;
        cout<<"Book author: "<<b.author<<endl;
        cout<<"Book number: "<<b.bn<<endl;
    }
    else
        cout<<"The book by this number is not found! \n";
}

void searchh_by_title(char title[],int sizee)
{
    Book b;
    ifstream in("data.txt");
    int flag=0;
    in.read((char*)&b,sizeof(b));
    while(!in.eof())
    {
        char c;
        c=strcmp(title,b.title);
        if(c==0)
        {
            flag=1;
            break;
        }
        in.read((char*)&b,sizeof(b));
    }
    if(flag==1)
    {
        cout<<"the book is found!\n\n\n";
        cout<<"Book title:  "<<b.title<<endl;
        cout<<"Book author: "<<b.author<<endl;
        cout<<"Boo number: "<<b.bn<<endl;
    }
    else

        cout<<"The book by this title is not found! \n";
}

void searchh_by_author(char author[],int sizee)
{
    Book b;
    ifstream in("data.txt");
    int flag=0;
    in.read((char*)&b,sizeof(b));
    while(!in.eof())
    {

        char c;
        c=strcmp(author,b.author);
        if(c==0)
        {
            flag=1;
            break;
        }
        in.read((char*)&b,sizeof(b));
    }
    if(flag==1)
    {
        cout<<"the book is found!\n\n\n";
        cout<<"Book title:  "<<b.title<<endl;
        cout<<"Book author: "<<b.author<<endl;
        cout<<"Book number: "<<b.bn<<endl;
    }
    else

        cout<<"The book by this title is not found! \n";
}

void update_by_number(int bn)
{
    Book b;
    ifstream in("data.txt");

    int flag=0;
    in.read((char*)&b,sizeof(b));
    while(!in.eof())
    {
        if(bn==b.bn)
        {
            flag=1;
            break;
        }
        in.read((char*)&b,sizeof(b));
    }
    ofstream out("data.txt",ios::out|ios::in);
    if(flag==1)
    {
        int i=in.tellg();
        out.seekp(i-sizeof(b));

        cout<<"enter the new information: \n";
        cout<<"enter the title: \n";
        cin.ignore();
        cin.getline(b.title,20);
        cout<<"enter the author: \n";
        cin.getline(b.author,20);
        cout<<"enter the book number: \n";
        cin>>b.bn;
        out.write((char*)&b,sizeof(b));
        }
    else
    cout<<"update is not possible by this number";
}
void deletee_by_number(int bn)
{
    Book b;
    ifstream in("data.txt");

    int flag=0;
    in.read((char*)&b,sizeof(b));
    while(!in.eof())
    {
        if(bn==b.bn)
        {
            flag=1;
            break;
        }
        in.read((char*)&b,sizeof(b));
    }
    ofstream out("data.txt",ios::out|ios::in);
    if(flag==1)
    {
        int i=in.tellg();
        out.seekp(i-sizeof(b));
        strcpy(b.title,"");
        strcpy(b.author,"");
        b.bn=0;
        out.write((char*)&b,sizeof(b));
    }
}
  void intro()
{
    cout<<"*************************************\n";
    cout<<"Well come to menelik secodary school"<<endl;
    cout<<"\n\n*********************************\n";
    cout<<endl;
    cout<<"press any key to continue!!!";
    cin.get();

}
