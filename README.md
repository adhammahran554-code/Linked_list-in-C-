#include <iostream>
using namespace std;


class Linked_List
{
private:
    struct Node
    {
        int item;
        Node* Next;
    };

    Node* first;
    Node* last;
    int length;
public:
    Linked_List()
    {
        first = NULL;
        last = NULL;
        length = 0;
    }

    bool IsEmpty();
    void Push_Front(int element);
    void Push_Bach(int element);
    void Push_At(int pos, int element);
    void Pop_Front();
    void Pop_Back();
    void pop_Element(int element);
    void Print();

};




bool Linked_List::IsEmpty()
{
    return first == NULL;
}

void Linked_List::Push_Front(int element)
{
    Node* newnode = new Node;
    newnode->item = element;
    if (length == 0)
    {
        first = newnode;
        last = newnode;
        newnode->Next = NULL;
    }
    else
    {
        newnode->Next = first;
        first = newnode;
    }
    length++;
}

void Linked_List::Push_Bach(int element)
{
    Node* newnode = new Node;
    newnode->item = element;

    if (length == 0)
    {
        first = newnode;
        last = newnode;
        newnode->Next = NULL;
    }

    else
    {
        last->Next = newnode;
        last = newnode;
        last->Next = NULL;
    }
    length++;

}

void Linked_List::Push_At(int pos, int element)
{
    if (pos < 0 || pos > length)
        cout << "OUT OF RANGE......!" << endl;
    else if (pos == 0)
        Push_Front(element);
    else if (pos == length)
        Push_Bach(element);
    else
    {
        Node* newnode = new Node;
        newnode->item = element;
        Node* cur = first;
        for (int i = 1; i < pos; i++)
        {
            cur = cur->Next;
        }
        newnode->Next = cur->Next;
        cur->Next = newnode;
        length++;
    }
}

void Linked_List::Pop_Front()
{
    if (IsEmpty())
    {
        cout << "THE LIST IS EMPTY.....!" << endl;
        return;
    }
    else if (length == 1)
    {
        delete first;
        first = NULL;
        last = NULL;
    }

    else
    {
        Node* cur = first;
        first = first->Next;
        delete cur;
    }
    length--;
}

void Linked_List::Pop_Back()
{
    if (IsEmpty())
    {
        cout << "THE LIST IS EMPTY.....!" << endl;
        return;
    }
    else if (length == 1)
    {
        delete first;
        first = NULL;
        last = NULL;
    }

    else
    {
        Node* cur = first->Next;
        Node* prev = first;

        while (cur != last)
        {
            prev = cur;
            cur = cur->Next;
        }
        prev->Next = NULL;
        last = prev;
        delete cur;
    }
    length--;
}

void Linked_List::pop_Element(int element)
{
    if (IsEmpty())
    {
        cout << "THE LIST IS EMPTY.....!" << endl;
        return;
    }
    if (first->item == element)
    {
        Pop_Front();
        return;
    }
        

    else if (last->item == element)
    {
        Pop_Back();
        return;
    }

    else
    {
        Node* cur = first->Next;
        Node* prev = first;
        while (cur != NULL)
        {
            if (cur->item == element)
            {
                prev->Next = cur->Next;
                if (last == cur)
                    last = prev;

                delete cur;
                length--;
                return;
            }
            
            prev = cur;
            cur = cur->Next;
        }

        cout << "CANN`T GET THE ELEMENT.....!" << endl;
    }
}

void Linked_List::Print()
{
    Node* cur = first;
    while (cur != NULL)
    {
        cout << cur->item << " ";
        cur = cur->Next;
    }
}






int main()
{
    Linked_List lk;
    lk.Push_Front(50);
    lk.Push_Front(40);
    lk.Push_Front(30);
    lk.Push_Bach(60);
    lk.Push_At(0, 20);
    lk.Push_At(5, 70);
    lk.Push_At(2, 35);
    lk.Push_At(10, 100);
    lk.Pop_Front();
    lk.Pop_Back();
    lk.pop_Element(40);
    lk.Print();
}


