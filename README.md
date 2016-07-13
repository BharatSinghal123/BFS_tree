#include <stdio.h>
#include <stdlib.h>
struct node_tree{
    int data;
    struct node_tree* right;
    struct node_tree* left;
};
struct node{
    struct node_tree* data;
    struct node* next;
};
struct queue{
    struct node* rear;
    struct node* front;
};
struct queue* create_queue(){
    struct queue* q = (struct queue*)malloc(sizeof(struct queue));
    q->rear = q->front = NULL;
    return q;
}
struct node_tree* dequeue(struct queue* q){
    if(q->front == NULL)
        return ;
    struct node * temp = q->front->next;
    q->front = q->front->next;
    free(temp);
    return q->front->data;
}
void enqueue(struct queue* q,struct node_tree* d){
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = d;
    temp->next = NULL;
    if(q->front == NULL && q->rear == NULL)
        q->front = q->rear = temp;
    else{
        q->rear->next = temp;
        q->rear = temp;
    }
}
struct node_tree* create_node(int k){
    struct node_tree* root = (struct node_tree*)malloc(sizeof(struct node_tree));
    root->data = k;
    root->right = NULL;
    root->left = NULL;
    return root;
};

void level_traversal(struct node_tree* root){
    struct queue* q = create_queue();
    enqueue(q,root);
    struct node_tree* temp = root;
    while(q->front != NULL){
        printf("%d ",temp->data);
        if(temp->left != NULL)
        enqueue(q,temp->left);
        if(temp->right != NULL)
        enqueue(q,temp->right);
        temp = dequeue(q);

    }
}
//void peek(struct queue* q){
//    printf("%d ",q->front->data);
//}
int main()
{
    struct node_tree * a = create_node(1);
    a->left = create_node(2);
    a->right = create_node(3);
    a->left->left = create_node(4);
    a->left->right = create_node(5);
    a->right->right = create_node(6);
    a->right->left = create_node(7);
    a->right->right->left = create_node(8);
    level_traversal(a);


}
