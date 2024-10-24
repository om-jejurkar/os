Q.1 Write a C program to implement the shell which displays the command prompt “myshell$”. It accepts the command, tokenize the command line and execute it by 
creating the child process. Also implement the additional command ‘typeline’ as typeline +n filename :- To print first n lines in the file.
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
if(strcmp(tok1,"type") == 0){
typeline(tok2,tok3);
continue;
}
}
}
Q.2 Write a C program to simulate Non-preemptive Shortest Job First (SJF) – scheduling. The arrival time and first CPU-burst of different jobs should be input to the 
system. Accept no. of Processes, arrival time and burst time. The output should give Gantt chart, turnaround time and waiting time for each process. Also find the average 
waiting time and turnaround time
#include<stdio.h>
#include<stdlib.h>
struct job{
int atime; //arraival time.
int btime; //brust time.
int ft; //finish time.
int tat; //Trun around time.
int wt; // waiting time.
}p[10];
int arr[10],brust[10],n,rq[10],no_rq=0,time=0;
int addrq();
int selectionjob();
int deleteq(int j);
int fsahll();
void main(){
int i,j;
printf("Enter the Process -: ");
scanf("%d",&n);
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the arrival time p%d -: ",i);
scanf("%d",&p[i].atime); //Assigning the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the arrival time p%d -: ",i);
printf("%d\n",p[i].atime); //Printing the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the brust time p%d -: ",i);
scanf("%d",&p[i].btime); //Assigning the brust time.
brust[i] = p[i].btime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the brust time p%d -: ",i);
printf("%d\n",p[i].btime); //Printing the brust time.
brust[i] = p[i].btime;
}
printf("\n");
addrq(); //Adding the process.
// Process start now.
printf("Gnatt Chart is -: ");
while(1){
j = selectionjob(); //sercah the process now.
if(j == -1){
printf("CPU is ideal");
time++;
addrq(); 
}else{
while(brust[j]!=0){
printf("\t j %d",j);
brust[j]--;
time++;
addrq();
}
p[j].ft = time;
}
if(fsahll() == 1)
break;
}
int Tat = 0,Twt =0;
printf("\n");
printf("\nProcess\t FT \t TAT \t WT");
for(i=0;i<n;i++){
p[i].tat = p[i].ft-p[i].atime;
p[i].wt = p[i].tat-p[i].btime;
printf("\n p%d \t %d \t %d \t %d",i,p[i].ft,p[i].tat,p[i].wt);
Tat += p[i].tat;
Twt += p[i].wt;
}
float avgtat = Tat /n;
float avgwt = Twt /n;
printf("\nAverage of wait time is -: %f",avgwt);
printf("\nAverage of trunaround time is -: %f",avgtat);
}
int addrq(){
int i;
for(i=0;i<n;i++){
if(arr[i] == time){
rq[no_rq] = i;
no_rq++;
}
}
}
int selectionjob(){
int i,j;
if(no_rq == 0)
return 1;
j = rq[0];
for(i=1;i<no_rq;i++)
if(brust[j]>brust[rq[i]])
j = rq[i];
deleteq(j);
return j;
}
int deleteq(int j){
int i;
for(i=0;i<no_rq;i++)
if(rq[i] == j)
break;
for(i= i+1;i<no_rq;i++)
rq[i-1] = rq[i];
no_rq--;
}
int fsahll(){
int i;
for(i=0;i<n;i++)
if(brust[i]!=0)
return -1;
return 1; 
}
