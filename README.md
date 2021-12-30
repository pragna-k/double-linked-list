# double-linked-list
#include<stdio.h>
#include<stdlib.h>
struct clist
{
        int data;
        struct clist *right;
        struct clist *left;
};
typedef struct clist node;
node* create(node*first)
{
        int data;
        node* new,*prev;
        printf("enter data value");
        scanf("%d",&data);
        while(data!=-1)
        {
                new=(node*)malloc(sizeof(node));
                new->data=data;
                new->right=NULL;
                new->left=NULL;
                if(first==NULL)
                {
                        first=new;
                        prev=new;
                }
                else
                {
                        prev->right=new;
                        new->left=prev;
                        prev=new;
                }
                printf("enter data:");
                scanf("%d",&data);
        }
        return first;
}
void display(node *first)
{
        node *temp=first;
        while(temp!=NULL)
        {
                printf("%d",temp->data);
                temp=temp->right;
        }
}
int count(node *first)
{
        int c=0;
        node *temp=first;
        while(temp!=NULL)
        {
                c+=1;
                temp=temp->right;
        }
        return c;
}
void search(node *first,int ele)
{
        int flag=0;
        node *temp=first;
        while(temp!=NULL)
        {
                if(temp->data=ele)
                {
                        flag=1;
                        break;
                }
                if(flag==1)
                {
                printf("the element %d is found",ele);
        }
        else
        {
                printf("the element %d is not found",ele);
        }
}
node* begin_insert(node *first,int insel)
{
        node *new;
        new=(node*)malloc(sizeof(node));
        new->data=insel;
        new->right=NULL;
        new->left=NULL;
        new->right=first;
        first->left=new;
        first=new;
        return first;
}
node* last_insert(node *first,int insel)
{
        node *new,*temp=first;
        new=(node*)malloc(sizeof(node));
        new->data=insel;
        new->right=NULL;
        new->left=NULL;
        while(temp->right!=NULL)
        {
                temp=temp->right;
        }
        temp->right=new;
        new->left=temp;
        return first;
}
node *random_insert(node *first,int insel,int pos)
{
        int i;
        node *temp=first;
        node *temp1;
        node *new;
        new=(node*)malloc(sizeof(node));
        new->data=insel;
        new->right=NULL;
        new->left=NULL;
        if(first==NULL)
        {
        return 0;
        }
        else
        {
                for(i=1;i<pos;i++)
                {
                        temp1=temp;
                        temp=temp->right;
                }
                temp1->right=new;
                new->left=temp1;
                temp->left=new;
                new->right=temp;
                return first;
                }

}
node *begin_delete(node *first)
{
        first=first->right;
        first->left=NULL;
        return first;
        }
node *random_delete(node*first,int pos)
{
        int i;
        node *temp=first;
        node*temp1;
        for(i=1;i<pos;i++)
        {
                temp1=temp;
                temp=temp->right;
        }
        temp->right->left=temp1;
        temp1->right=temp->right;
        free(temp);
        return first;
}
void main()
{
        int insel,pos,ch,ele,c;
        node *head=NULL;
        printf("enter insele:");
        scanf("%d",&insel);
        printf("enter pos:");
        scanf("%d",&pos);
        printf("enter ele:");
        scanf("%d",&ele);
        while(1)
                {
                        printf("enter ch:");
                        scanf("%d",&ch);
                        switch(ch)
                        {
                             case 1:head=create(head);
                                       break;
                                case 2:display(head);
                                       break;
                                case 3:c=count(head);
                                       printf("number of nodes is %d",c);
                                       break;
                                case 4:search(head,ele);
                                       break;
                                case 5:head=begin_insert(head,insel);
                                       break;
                                case 6:head=last_insert(head,insel);
                                       break;
                                case 7:head=random_insert(head,insel,pos);
                                       break;
                                case 8:head=begin_delete(head);
                                       break;
                                case 9:head=random_delete(head,pos);
                                       break;
                                case 10:exit(0);
                        }
                }               }
}
