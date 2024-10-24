Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the Optimal page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 7, 5, 4, 8, 5, 7, 2, 3, 1, 3, 5, 9, 4, 6,
#include<stdio.h>
int main()
{
int no_of_frames,no_of_pages,frames[10],pages[30],temp[10],flag1,flag2,flag3,i,j,k,pos,max,faults=0;
printf("Enter number of frames -: ");
scanf("%d",&no_of_frames);
printf("Enter number of pages -: ");
scanf("%d",&no_of_pages);
printf("Enter page reference string -: ");
for(i=0;i<no_of_pages;i++)
{
scanf("%d",&pages[i]);
}
for(i=0;i<no_of_frames;i++)
{
frames[i]=-1;
}
for(i=0;i<no_of_pages;i++)
{
flag1=flag2=0;
for(j=0;j<no_of_frames;j++)
{
if(frames[j]==pages[i])
{
flag1=flag2=1;
break;
}
}
if(flag1==0)
{
for(j=0;j<no_of_frames;j++)
{
if(frames[j]==-1)
{
faults++;
frames[j]=pages[i];
flag2=1;
break;
}
}
}
if(flag2==0)
{
flag3=0;
for(j=0;j<no_of_frames;j++)
{
temp[j]=-1;
for(k=i+1;k<no_of_pages;k++)
{
if(frames[j]==pages[k])
{
temp[j]=k;
break;
}
}
}
for(j=0;j<no_of_frames;j++)
{
if(temp[j]==-1)
{
pos=j;
flag3=1;
break;
}
}
if(flag3==0)
{
max=temp[0];
pos=0;
for(j=1;j<no_of_frames;j++)
{
if(temp[j]>max)
{
max=temp[j];
pos=j;
}
}
}
frames[pos]=pages[i];
faults++;
}
printf("\n");
for(j=0;j<no_of_frames;j++)
{
printf("\n pg=%d |",pages[i]);
printf("%d\t",frames[j]);
}
}
printf("\n Total Page Faults -: %d",faults);
return 0;
}
Q.2 Write the program to simulate FCFS CPU-scheduling. The arrival time and first CPU-burst of different jobs should be input to the system. Accept no. of 
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
