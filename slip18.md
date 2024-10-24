Q.1 Write the simulation program to implement demand paging and show the page scheduling and total number of page faults according to the LRU (using counter method) 
page replacement algorithm. Assume the memory of n frames. 
Reference String : 3,5,7,2,5,1,2,3,1,3,5,3,1,6,2
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
