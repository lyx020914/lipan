# lipan
#include <stdio.h>
#include <malloc.h>
typedef char ElemType;
typedef struct LNode  
{
	ElemType data;
	struct LNode *next;		//指向后继结点
} LinkNode;					//声明单链表结点类型

void CreateListR(LinkNode *&L,ElemType a[],int n)  //尾插法建立单链
{
	LinkNode *s,*r;
	L=(LinkNode *)malloc(sizeof(LinkNode));  	//创建头结点
	L->data=a[0];
	r=L;					//r始终指向终端结点,开始时指向头结点
	for (int i=1;i<n;i++)
	{	
		s=(LinkNode *)malloc(sizeof(LinkNode));//创建新结点s
		s->data=a[i];
		r->next=s;			//将结点s插入结点r之后
		r=s;
	}
	r->next=NULL;			//终端结点next域置为NULL
}
void found1(LinkNode *L)
{
	if(L==NULL){
		return;
	}
	printf("%c ",L->data);
	found1(L->next);
}
void found2(LinkNode *L)
{
	if(L==NULL){
		return;
	}
	found2(L->next);
	printf("%c ",L->data);
}
int found3(LinkNode *L)
{
	while(L==NULL){
		return 0;
	}
	return 1+found3(L->next);
}
int found4(LinkNode *L)
{
	int n=0;
	if(L==NULL)
	    return 0;
	n=found4(L->next);
	return(L->data>='0'&&L->data<='9')?n+1:n;
}
int found5(LinkNode *L,char c)
{
	int i;
	if(L==NULL){
		return 0;
	}
	i=found5(L->next,c);
	return L->data==c?i+1:i;
}
void found7(LinkNode *&L,char c)
{
	LinkNode *Q;
	if(L==NULL)
	   return;
	Q=L;
	if(Q->data==c){
		L=Q->next;
		free(Q);
		found7(L,c);
	}
	else
	    found7(L->next,c);
}
void found6(LinkNode *&L, char c)
{
	if(L==NULL){
		return;
	}
	if(L->data==c){
		LinkNode *Q=L;
		L=L->next;
		free(Q);
		return ;
	}
	else
	    found6(L,c);
}
int main(void)
{
	int i;
	LinkNode *L;
	char a[100],c1;
	printf("  请输入字符串:");
	for(i=0; ;i++){
		a[i]=getchar();
		if(a[i]=='\n')
		   break;
	}
	CreateListR(L,a,i);
	printf("功能一 显示正向字符串:");
	found1(L);
	printf("\n功能二 显示反向字符串:");
	found2(L);
	int num1=0;
	num1=found3(L);
	printf("\n功能三 此字符串共含有%d个字符",num1);
	int num2=0;
	num2=found4(L);
	printf("\n功能四 此字符串中有%d个数字字符",num2);
	printf("\n 输入想统计的字符:");
	c1=getchar();
	getchar();
	int num3=found5(L,c1);
	printf("功能五 此字符串中有%d个字符“%c”",num3,c1);
	printf("\n 输入想要删除的字符:"); 
	c1=getchar();
	found6(L,c1);
	printf("功能六 此字符串第一个“%c”被删除后：",c1);
	found1(L);
	found7(L,c1);
	printf("\n功能七 此字符串所有的“%c”被删除后：",c1);
	found1(L);
	return 0;
}
