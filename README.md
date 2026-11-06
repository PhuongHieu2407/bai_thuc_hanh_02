# bai_thuc_hanh_02
bài_1 nhập và in một mảng 1 chiều các số thực
#include <stdio.h>
#include <stdlib.h>
void nhap(int *a,int n){
	int i;
	for(i=0;i<n;i++){
		printf("Nhap phan tu thu %d:",i);
		scanf("%d",a+i);
	}
}
void in(int*a,int n){
	int i;
	for(i=0;i<n;i++){
		printf("%d, ",*(a+i));
	}
}
int main(){
	int *a;
	int n;
	printf("Nhap so phan tu:");
	scanf("%d",&n);
	a=(int*) malloc(n*sizeof(int));
	nhap(a,n);
	printf("\nDL ban dau\n");
	in(a,n);
	free(a);
	a=NULL;
}


bài_2 Nhập và in một mảng 2 chiều các số thực
#include <stdio.h>
#include <stdlib.h>

int main() {
 int h, c;
 printf("Nhap so hang va so cot: ");
 scanf("%d%d", &h, &c);
 
 int **ma = (int **)malloc(h * sizeof(int *));
 if (ma == NULL) {
 printf("Khong du bo nho!\n");
 return 1;
 }

 for (int i = 0; i < h; i++) {
 ma[i] = (int *)malloc(c * sizeof(int));
 if (ma[i] == NULL) {
 printf("Khong du bo nho tai dong %d!\n", i);
 return 1;
 }
 }

 for (int i = 0; i < h; i++) {
 for (int j = 0; j < c; j++) {
 scanf("%d", &ma[i][j]);
 }
 }

 
 printf("Ma tran %dx%d vua tao:\n", h, c);
 for (int i = 0; i < h; i++) {
 for (int j = 0; j < c; j++) {
 printf("%d\t", ma[i][j]);
 }
 printf("\n");
 }

 for (int i = 0; i < h; i++) {
 free(ma[i]);
 }
 free(ma);

 return 0;
}
bài_3 Nhập và in ds sinh viên
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct{
	char hoten[30];
	int maSV;
	float d1,d2,d3;
}SV;
void nhap(SV *ds,int n){
	int i;
	for(i=0;i<n;i++){
		getchar();
		fgets((ds+i)->hoten,sizeof((ds+i)->hoten),stdin);
		(ds+i)->hoten[strcspn((ds+i)->hoten,"\n")]='\0';
		scanf("%d",&(ds+i)->maSV);
		scanf("%f",&(ds+i)->d1);
		scanf("%f",&(ds+i)->d2);
		scanf("%f",&(ds+i)->d3);
	}
}
void in(const SV *ds,int n){
	int i;
	for(i=0;i<n;i++){
		printf("%s %d %.2f %.2f %.2f\n, ",
		(ds+i)->hoten,
		(ds+i)->maSV,
		(ds+i)->d1,
		(ds+i)->d2,
		(ds+i)->d3);
	}
}
int main(){
	int n;
	printf("Nhap so luong sinh vien:");
	if(scanf("%d",&n)!=1||n<=0){
		printf("So luong sinh vien khong hop le\n");
		return 1;
	}
	SV *dsSV=(SV *)malloc(n * sizeof(SV));
	if(dsSV==NULL){
		printf("Khong the cap phat bo nho");
		return 1;
	}
	nhap(dsSV,n);
	in(dsSV,n);
	free(dsSV);
	dsSV=NULL;
	return 0;
}
bài 4 Khai báo cấu trúc dữ liệu
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct{
	char hoten[30];
	int maSV;
	float d1,d2,d3;
}Data;
typedef struct tagNode{
	Data infor;
	struct tagNode *link;
}Node;
typedef struct {
	Node*pHead;Node*pTail;
	int spt;
}LList;
void nhap(Data *x){
	printf("Nhap ma:");
	scanf("%d",&(x->maSV));
	if(x->maSV>0){
		printf("Nhap ten:");
		scanf("%s",x->hoten);
		printf("Nhap diem 1:");
		scanf("%.2f",&(x->d1));
		printf("Nhap diem 2:");
		scanf("%.2f",&(x->d2));
		printf("Nhap diem 3:");
		scanf("%.2f",&(x->d3));
	}
}
void in(Data x){
		printf("%s %d %.2f %.2f %.2f\n",
		x.hoten,
		x.maSV,
		x.d1,
		x.d2,
		x.d3);
}
void initL(LList *L){
	L->pHead=NULL;
	L->pTail=NULL;
	L->spt=0;
}
void insertHead(LList *L,Data x){
	Node *pp;
	pp=(Node*) malloc(sizeof(Node));
	pp->infor=x;
	pp->link=NULL;
}
void tao_ds(LList *L){
	initL(L);
	Data x;
	do{
		nhap(&x);
		if(x.maSV>0) insertHead(L,x);
	}while (x.maSV>0);
}
void duyet_ds(LList L){
	Node *pp=L.pHead;
	while(pp!=NULL){
		in(pp->infor);
		pp=pp->link;
	}
}
int main(){
	LList ds1;
	initL(&ds1);
	tao_ds(&ds1);
	duyet_ds(ds1);
}


