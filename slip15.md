Q.1 Write a C program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating 
the child process. Additionally it should interpret the following ‘list’ commands as myshell$ list f dirname :- To print names of all the files in current directory.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<dirent.h>
//struct dirent{
// char d_name[20];
// int ino;
//};
void list(char *tok2,char *tok3){
int c = 0;
struct dirent *dir;
// dir -> d_name, dir->ino 
DIR *dr;
dr = opendir(tok3);
if(dr == NULL){
printf("Dir does not exist.");
}
if(strcmp(tok2,"f") == 0){
while(dir = readdir(dr))
printf("\n%s",dir->d_name);
}else if(strcmp(tok2,"n") == 0){
while(dir = readdir(dr))
c++;
printf("\nttoal number of files :%d",c);
}else if(strcmp(tok2,"i") == 0){
while(dir = readdir(dr))
printf("\n%s\t%d",dir->d_name,dir->d_ino);
}
}
int main(){
char tok1[10],tok2[10],tok3[10],tok4[10],cmd[30];
int choice;
while(1){
printf("\n$shell$:");
gets(cmd);
if(strcmp(cmd,"exit") == 0){
exit(0);
}
int choice = sscanf(cmd,"%s%s%s%s",&tok1,&tok2,&tok3,&tok4);
if(choice == 3){
if(strcmp(tok1,"list") == 0){
list(tok2,tok3);
continue;
}
}
}
}
Q.2 Write the program to simulate preemptive Shortest Job First (SJF) – scheduling. The arrival time and first CPU-burst of different jobs should be input to the system. 
Accept no. of Processes, arrival time and burst time. The output should give Gantt chart, turnaround time and waiting time for each process. Also find the average waiting 
time and turnaround time
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>
struct job
{
bool isc;
int at; // Arraival time.
int bt; // Brust time.
int st; // Start time
int wt; // Wait time.
int nst; // New start time.
int oft; // Old finish time.
int pcount;// Process to be count.
int ft; // Finish time.
int tat; // Trun around time.
}p[100];
int n,arr[100],tm=0,arrv=0,count=0;
int selecta();
int process(int s);
float Tat,Wt;
void main(){
int i,k=0,a[100];
printf("How many Process -: ");
scanf("%d",&n);
printf("Enter -: \nProcess BT AT\n");
for(i=1;i<=n;i++){
printf("p%d\t",i);
scanf("%d%d",&p[i].bt,&p[i].at);
p[i].isc=false;
p[i].pcount=0;
count += p[i].bt;
p[i].wt=0;
}
printf("Process BT AT \n");
for(i=1;i<=n;i++)
printf("p%d %d %d\n",i,p[i].bt,p[i].at);
printf("\nGantt chart -: \n");
for(i=1;i<=n;i++)
{
if(p[i].at==0)
{
a[++k]=i;
}
}
int minbrust(int a[],int k);
while(tm!=count)
{
selecta();
if(arrv==0)
{
printf("|idl");
tm+=1;
count+=1;
}
else
{
minbrust(arr,arrv);
arrv=0;
}
}
printf("\n");
printf("\nProcess\tBT\tAT \tST\tWT\tFT\tTAT\n");
for(i=1;i<=n;i++)
printf("P%d\t%d\t%d\t%d\t%d\t%d\t%d\n",i,p[i].bt,p[i].at,p[i].st,p[i].wt,p[i].ft,p[i].tat);
printf("\nAvg wait time -: %f",Wt/n);
printf("\nAvg TAT -: %f\n",Tat/n);
}
int minbrust(int a[],int k){
int min=p[a[1]].bt,i,m=a[1];
for(i=1;i<=k;i++)
{
if(p[a[i]].bt<min)
{
min=p[a[i]].bt;
m=a[i];
}
}
process(m);
}
int process(int s)
{
int k;
p[s].pcount++;
if(p[s].pcount==1)
{
p[s].wt=p[s].st-p[s].at;
p[s].st=tm;
}
p[s].nst=tm;
tm++;
k=p[s].nst-p[s].oft;
p[s].oft=tm;
if(k>0)
p[s].wt+=k;
if(p[s].pcount==p[s].bt)
{
p[s].isc=true;
p[s].ft=tm;
p[s].tat=p[s].ft-p[s].at;
Tat+=p[s].tat;
Wt+=p[s].wt;
}
printf("p%d ",s);
}
int selecta(){
int i;
for(i=1;i<=n;i++)
{
if(p[i].at<=tm && p[i].isc==false)
arr[++arrv]=i; 
}
}
