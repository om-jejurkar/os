Q.1 Write a programto implement the toy shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by 
creating the child process. Additionally it should interpret the following commands.
count c filename :- To print number of characters in the file.
count w filename :- To print number of words in the file.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include <string.h>
void count(char *tok2 ,char *tok3)
{
int l=0,w=0,c=0;
FILE *fp;
fp = fopen(tok3,"r");
if(fp==NULL)
printf("\n file not exist");
else
{
while(!feof(fp))
{
char ch;
ch = fgetc(fp);
if(ch == ' ' )
w++;
else if(ch == '\n')
{
w++;
l++;
}
else
c++;
}
if(strcmp(tok2,"w") == 0)
printf("\n word count :%d",w);
if(strcmp(tok2,"c") == 0)
printf("\n character count :%d",c);
}
}
int main(int argc , char *argv[])
{
char command[30],tok1[30],tok2[30],tok3[30];
while(1)
{
printf("\n MyShell:");
gets(command);
int ch = sscanf(command,"%s%s%s",tok1,tok2,tok3);
if(ch == 3)
{
if(strcmp(tok1,"count")==0)
count(tok2,tok3);
continue;
}
}
}
Q.2 Write the program to simulate Non preemptive priority scheduling. The arrival time and first CPU-burst of different jobs should be input to the system. Accept no. of 
Processes, arrival time and burst time. The output should give Gantt chart, turnaround time and waiting time for each process. 
Also find the average waiting time and turnaround time.
#include<stdio.h>
#include<stdlib.h>
struct job{
int atime; // arraival time.
int btime; //brust time.
int ft; //finish time.
int tat; //Trun around time.
int wt; // waiting time.
int pri; //Priority varilable is add.
}p[10];
int arr[10],brust[10],n,rq[10],no_rq=0,time=0,j=-1;
void main(){
int i,j;
printf("Enter the job number:");
scanf("%d",&n);
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the arrival time p%d:",i);
scanf("%d",&p[i].atime); //Assigning the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the arrival time p%d:",i);
printf("%d",p[i].atime); //Assigning the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the brust time p%d:",i);
scanf("%d",&p[i].btime); //Assigning the brust time.
brust[i] = p[i].btime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the brust time p%d:",i);
printf("%d",p[i].btime); //Assigning the brust time.
brust[i] = p[i].btime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Priority p%d:",i);
scanf("%d",&p[i].pri); //Assigning the Priority.
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Priority p%d:",i);
printf("%d",p[i].pri); //Assigning the Priority.
}
printf("\n");
addrq(); //Adding the process.
// Process start now.
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
printf("\nJob \t FT \t TAT \t WT");
for(i=0;i<n;i++){
p[i].tat = p[i].ft-p[i].atime;
p[i].wt = p[i].tat-p[i].btime;
printf("\n JOb %d \t %d \t %d \t %d",i,p[i].ft,p[i].tat,p[i].wt);
Tat += p[i].tat;
Twt += p[i].wt;
}
float avgtat = Tat /n;
float avgwt = Twt /n;
printf("\nAverage of trun around time is:%f",avgtat);
printf("\nAverage of wait time is:%f",avgwt);
}
int addrq(){
int i;
for(i=0;i<n;i++){
if(arr[i] == time){
if(j!=-1 && p[i].pri>p[j].pri){
rq[no_rq] = i;
j = i;
}else{
rq[no_rq++] = i;
}
}
}
}
int selectionjob(){
int i,k;
if(no_rq == 0)
return -1;
k = rq[0];
for(i=1;i<no_rq;i++)
if(p[k].pri<p[rq[i]].pri){
k = rq[i];
}
deleteq(k);
return k;
}
int deleteq(int k){
int i;
for(i=0;i<no_rq;i++)
if(rq[i] == k)
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
