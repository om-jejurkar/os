

Q.2 Write a C program to simulate FCFS CPU-scheduling. The arrival time and first CPU-burst of different jobs should be input to the system. Accept no. of 
Processes, arrival time and burst time. The output should give Gantt chart, turnaround time and waiting time for each process. Also find the average 
waiting time and turnaround time.
#include<stdio.h>
#include<stdlib.h>
struct job{
int atime; // Arraival time.
int btime; // Brust time.
int ft; // Finish time.
int tat; // Trun around time.
int wt; // waiting time.
}p[10];
int arr[10],brust[10],n,rq[10],no_rq=0,time=0;
int addrq();
int selectionjob();
int deleteq(int j);
int fsahll();
void main()
{
int i,j;
printf("Enter the Process -: ");
scanf("%d",&n);
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Arrival time p%d -: ",i);
scanf("%d",&p[i].atime); //Assigning the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Arrival time p%d -: ",i);
printf("%d\n",p[i].atime); //Printing the arrival time.
arr[i] = p[i].atime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Brust time p%d -: ",i);
scanf("%d",&p[i].btime); //Assigning the brust time.
brust[i] = p[i].btime;
}
printf("\n");
for(i = 0;i<n;i++){
printf("Enter the Brust time p%d -: ",i);
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
printf("\n P%d \t %d \t %d \t %d",i,p[i].ft,p[i].tat,p[i].wt);
Tat += p[i].tat;
Twt += p[i].wt;
}
float avgtat = Tat /n;
float avgwt = Twt /n;
printf("\nAverage of wait time is -: %f",avgwt);
printf("\nAverage of trun around time is -: %f",avgtat);
printf("\n");
}
int addrq()
{
int i;
for(i=0;i<n;i++){
if(arr[i] == time){
rq[no_rq] = i;
no_rq++;
}
}
}
int selectionjob()
{
int i,j;
if(no_rq == 0)
return 1;
j = rq[0];
deleteq(j);
return j;
}
int deleteq(int j)
{
int i;
for(i=0;i<no_rq;i++)
if(rq[i] == j)
break;
for(i= i+1;i<no_rq;i++)
rq[i-1] = rq[i];
no_rq--;
}
int fsahll()
{
int i;
for(i=0;i<n;i++)
if(brust[i]!=0)
return -1;
return 1; 
}
