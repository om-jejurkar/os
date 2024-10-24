#include<stdio.h>
int pf=0,pg;
int f,frame[5],ref[50],victim=0,time[50];
int searchpage(int p)
{
int i;
for(i=0;i<f;i++)
if(frame[i]==p)
return i;
return -1;
}
int selectvictim()
{
int min=0,i;
for(i=1;i<f;i++)
{
if(time[i]<time[min])
min=i;
}
return min;
}
void main()
{
int i;
printf("\n Enter the no. of frames -: ");
scanf("%d",&f);
for(i=0;i<f;i++)
frame[i]=-1;
for(i=0;i<f;i++)
time[i]=-1;
printf("\n Enter the no. of pages -: ");
scanf("%d",&pg);
printf("\n Enter the page(reference string) -: ");
for(i=0;i<pg;i++)
scanf("%d",&ref[i]);
for(i=0;i<pg;i++)
{
int k,j;
k=searchpage(ref[i]);
if(k==-1)
{
pf++;
k=selectvictim();
frame[k]=ref[i];
}
time[k]=i;
printf("\n pg=%d |",ref[i]);
for(j=0;j<f;j++)
printf("\t%d",frame[j]);
}
printf("\n Page Fault is -:%d",pf);
}



Q.2 Write a C program to implement the shell which displays the command prompt “myshell$”. It accepts the command, tokenize the command line and execute it by 
creating the child process. Also implement the additional command ‘typeline’ as 
typeline +n filename :- To print first n lines in the file.
typeline -a filename :- To print all lines in the file.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
void typeline(char *tok2,char *tok3){
char ch,str[30];
int lc=0,s,count=0;
FILE *fp;
fp = fopen(tok3,"r");
if(fp == NULL){
printf("File does not exist.\n");
}else{
printf("File exist\n");
}
if(strcmp(tok2,"a") == 0){
while(!feof(fp)){
ch = fgetc(fp);
printf("%c",ch);
}
}
else{
int n = atoi(tok2);
if(n>0){
while(lc<n){
ch = fgetc(fp);
if(ch == '\n')
lc++;
printf("%c",ch);
}
}
if(n<0){
while(!feof(fp)){
ch = fgetc(fp);
if(ch == '\n')
lc++;
}
s = lc + n;
s++;
fseek(fp,0,SEEK_SET);
while(!feof(fp)){
ch = fgetc(fp);
while (count!=s)
{
ch = fgetc(fp);
if(ch == '\n')
count++;
}
printf("%c",ch);
}
}
}
}
int main(){
char tok1[10],tok2[10],tok3[10],tok4[10],cmd[30];
int choice;
while(1){
printf("\n$MYShell$:");
gets(cmd);
if(strcmp(cmd,"exit") == 0){
exit(0);
}
int choice = sscanf(cmd,"%s%s%s%s",&tok1,&tok2,&tok3,&tok4);
if(strcmp(tok1,"typeline") == 0){
typeline(tok2,tok3);
continue;
}
}
}
