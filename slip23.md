Q.1 Write a C program to illustrate the concept of orphan process. Parent process creates a child and terminates before child has finished its task. So child process 
becomes orphan process. (Use fork(), sleep(), getpid(), getppid()).
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main() 
{
// fork() Create a child process
int pid = fork();
if (pid > 0) {
//getpid() returns process id
// while getppid() will return parent process id
printf("Parent process\n");
printf("ID : %d\n\n", getpid());
}
else if (pid == 0) {
printf("Child process\n");
// getpid() will return process id of child process
printf("ID: %d\n", getpid());
// getppid() will return parent process id of child process
printf("Parent -ID: %d\n\n", getppid());
sleep(10);
// At this time parent process has finished.
// So if u will check parent process id
// it will show different process id
printf("\nChild process \n");
printf("ID: %d\n", getpid());
printf("Parent -ID: %d\n", getppid());
}
else {
printf("Failed to create child process");
}
return 0;
}
Q.2 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the Optimal page replacement algorithm. 
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
