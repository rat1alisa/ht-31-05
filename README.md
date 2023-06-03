# ht-31-05

#include <iostream>
#include <algorithm>
using namespace std;

  
template <typename T>
class List
{
public:
    List();
    ~List();
    
    void push_back(T data);//удаление переднего элемента
    int GetSize () { return Size; };
    void pop_front();
    void clear();
    void push_front(T data);
    
    T& operator[](const int index);
    
private:
    
    template <typename T>
    class Node //1 элемент
    {
    public:
        Node *pNext;//указатель на следующий элемент
        T data;
        Node (T data = T(), Node *pNext = nullptr)
        {
            this -> data = data;
            this -> pNext = pNext;
        }
    };
    int Size;
    Node<T> *head;
    
};

template <typename T>
List<T>::List()//конструктор
{
    Size = 0;//кол-во элементов
    head = nullptr;//нулевой элемент
}

template <typename T>
List<T>::~List()//деструктор
{
    cout << "Destructor called";
    clear();
}

template <typename T>
List<T>::pop_front()
{
    Node<T> *temp = head;
	head = head->pNext;
	
	delete temp;
	Size--;
}

template <typename T>
void List<T>::push_back(T data)
{
    if (head == nullptr)
    {
        head = new Node<T>(data);
    }
    else
    {
        Node<T> *current = this->head;
        
        while(current -> pNext != nullptr)
        {
            current = current->pNext;
        }
        current-> pNext = new Node<T>(data);
    }
    Size++;
}

template <typename T>
void List<T>::clear()//удаление всех элементов
{
    while (Size)
	{
		pop_front();
	}
}

template <typename T>
T& List<T>::operator[](const int index)
{
    int counter = 0;
	Node<T> *current = this->head;
	while (current != nullptr)
	{
		if (counter == index)
		{
			return current->data;
		}
		current = current->pNext;
		counter++;
	}
}

template <typename T>
void List<T>::push_front(T data)//добавление вперед
{
    cout << "Enter new element - ";
	cin >> data;
    head = new Node<T>(data,head);
    Size++;
}
 
//---------------------------------------
  
class Exception
{
public:
	string err;
	Exception(string err)
	{
		err = "Error Occured!\n";
	}
	
	//constructor---
	Exception() {};
	~Exception() {};
	//destructor---
};

//---------------------------------------
int main()
{
    setlocale(LC_ALL, "RU");
    srand(time(NULL));
	List<int>lst;
	int ch;
	cout << "\tHEADER" << endl;
	cout << "1. Add to the end\n";
	cout << "2. Add to the front\n";
	cout << "3. List size\n";
	cout << "4. Delete element\n";
	cout << "5. Delete list\n";
	cout << "6. Print list\n";
	cout << "7. Other\n";
	do {
		cin >> ch;
		switch (ch) 
		{
		case 1: (ch == 1);//
		{
			lst.push_back(2);
			break;
		}
		case 2: (ch == 2);//
		{
			lst.push_front(2);
			break;
		}
		case 3: (ch == 3);
		{
		    try
		    {
		        cout << "List Size - " << lst.GetSize() << endl;
			    if (lst.GetSize() == 0)
					throw err;
		    }
			catch (Exception error)
			{
				error.err = "List Is Empty\n"; //!!!!!!!!!!!!!
				cout << error.err << endl;
			}
			break;
		}
		case 4: (ch == 4);
		{
			try
			{
				lst.pop_front();
				cout << "The first element has been removed\n";
				if (lst.GetSize() == 0)
					throw err;
			}
			catch (Exception error)
			{
				error.err = "List Is Empty, there is nothing to delete\n"; //!!!!!!!!!!!
				cout << error.err << endl;
			}
		}
		case 5: (ch == 5);
		{
			try 
			{
				if (lst.GetSize() == 0)
					throw err;
			}
			catch (Exception error)
			{
				error.err = "List Is Empty, there is nothing to delete\n"; //!!!!!!!!!!!!!!!!!!!!
				cout << error.err << endl;
			}
			lst.~List();
			break;
		}
		case 6: (ch == 6);
		{
			cout << "List: "; 
			for (int i = 0; i < lst.GetSize(); i++)
			{
				cout << lst[i] << ' | ';
			}
			cout << endl << endl;
			break;
		}
		case 7: (ch == 7);
		{
			break;
		}
		default:
		{
			cout << "ERROR";
		}
		}
	} while (ch != 7);
	system("pause");
	return 0;
}
