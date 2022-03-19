# BST
#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node *left_child;
    struct node *right_child;
};
 struct node *newnode(int x)
{
    struct node *p;
    p=malloc(sizeof(struct node));
    p->data=x;
    p->left_child=NULL;
    p->right_child=NULL;
    return p;
}
struct node *insert(struct node *root,int x)
{
   if(root==NULL)
   {
       return newnode(x);
    }
    else if(x>root->data)
    {
         root->right_child=insert(root->right_child,x);
    }
    else
    {
        root->left_child=insert(root->left_child,x);
    }
}
void in_order(struct node *root)
{ 
    if(root!=NULL)
    {
        printf("%d",root->data);
        in_order(root->left_child);
        in_order(root->right_child);
    }
   
}
void pre_order(struct node *root)
{
    if(root!=NULL)
    {
        pre_order(root->left_child);
         printf("%d",root->data);
        pre_order(root->right_child);
    }
}
void post_order(struct node *root)
{
     if(root!=NULL)
    {
        post_order(root->left_child);
        post_order(root->right_child);
         printf("%d",root->data);
    } 
}
struct node *search(struct node *root,int x)
{
    if(root==NULL||root->data==x)
    {
    return root;
    }
    else if(x>root->data)
    {
        return root->right_child=search(root->right_child,x);
    }
    else
    {
     return root->left_child=search(root->left_child,x);
    }
}
struct node *find_min(struct node*root)
{
    if(root==NULL)
    {
    return NULL;
    }
    else (root->left_child!=NULL);
    {
    return root->left_child=find_min(root->left_child);
    return root;
    }
}
struct node *delete(struct node*root,int x)
{
    if(root==NULL)
    {
    return root;
    }
    if(x>root->data)
    {
     return root->right_child=delete(root->right_child,x);
    }
    else 
    {
     return root->left_child=delete(root->left_child,x);
    }
     if(root->left_child==NULL&&root->right_child==NULL)
         {
             free(root);
             return NULL;
         }
         else if(root->left_child==NULL||root->right_child==NULL)
         {
             struct node *temp;
             if(root->left_child==NULL)
             {
             return root->right_child;
             }
             else
             {
             return root->left_child;
             }
             free(root);
            return root;
         }
         else
         {
             struct node *temp=find_min(root->right_child);
             root->data=root->right_child;
             root->data=temp->data;
             root->right_child=delete(root->right_child,temp->data);
         }
}
int main()
{
    struct node *root;
    root=newnode(20);
    insert(root,5);
    insert(root,13);
    insert(root,23);
    insert(root,56);
    insert(root,67);
    insert(root,87);
    insert(root,7);
    insert(root,6);
    insert(root,17);
    insert(root,61);
    printf("enter the in_order traversal is\n");
    in_order(root);
    printf("enter the pre_order traversal is\n");
    pre_order(root);
    printf("enter the post_order traversal is\n");
    post_order(root);
    root=delete(root,7);
    root=delete(root,6);
    printf("enter the in_order traversal after deletion is:\n");
    in_order(root);
    printf("enter the pre_order traversal after deletion is:\n");
    pre_order(root);
    printf("enter the post_order traversal after deletion is:\n");
    post_order(root);
    return 0;
}
