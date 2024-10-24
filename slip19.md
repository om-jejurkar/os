Q.1 Write a C program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating 
the child process. Additionally it should interpret the following ‘list’ commands as myshell$ list f dirname :- To print names of all the files in current directory.
#include<stdio.h>
#include<unistd.h>
#include<string.h>
#include<stdlib.h>
#include<dirent.h>
void list(char *tok2, char *tok3)
{
DIR *dp;
int c =0;
struct dirent *dir;
dp = opendir(tok3);
if(dp == 0)
printf("%s directory not exit",tok3);
else
{
if(strcmp(tok2,"f")==0)
{
while((dir=readdir(dp))!= NULL)
printf("%s \n ",dir->d_name);
}
}
} 
int main(int argc , char * argv[])
{
char tok1[20],tok2[20],tok3[20];
int choice,f;
char cmd[40];
while(1)
{
printf("\n Myshell$");
gets(cmd);
if(strcmp(cmd, "exit")==0)
exit(0);
int choice = sscanf(cmd,"%s%s%s",&tok1,&tok2,&tok3);
if(choice==3)
{
if(strcmp(tok1,"list")==0)
list(tok2,tok3);
continue;
}
}
}
Q.2 Write the simulation program for Round Robin scheduling for given time quantum. The arrival time and first CPU-burst of different jobs should be input to the system. 
Accept no. of Processes, arrival time and burst time. The output should give the Gantt chart, turnaround time and waiting time for each process. Also display the average 
turnaround time and average waiting time.
#include<stdio.h>
#include<stdlib.h>
int main() 
{ 
int i, limit, total = 0, x, counter = 0, time_quantum; 
int wait_time = 0, turnaround_time = 0, arrival_time[10], burst_time[10], temp[10]; 
float average_wait_time, average_turnaround_time;
printf("\nEnter Total Number of Processes:\t"); 
scanf("%d", &limit); 
x = limit; 
for(i = 0; i < limit; i++) 
{
printf("\nEnter Details of Process[%d]\n", i + 1);
printf("Arrival Time:\t");
scanf("%d", &arrival_time[i]);
printf("Burst Time:\t");
scanf("%d", &burst_time[i]); 
temp[i] = burst_time[i];
} 
printf("\nEnter Time Quantum:\t"); 
scanf("%d", &time_quantum); 
printf("\nProcess ID\t\tBurst Time\t Turnaround Time\t Waiting Time\n");
for(total = 0, i = 0; x != 0;) 
{ 
if(temp[i] <= time_quantum && temp[i] > 0) 
{ 
total = total + temp[i]; 
temp[i] = 0; 
counter = 1; 
} 
else if(temp[i] > 0) 
{ 
temp[i] = temp[i] - time_quantum; 
total = total + time_quantum; 
} 
if(temp[i] == 0 && counter == 1) 
{ 
x--; 
printf("\nProcess[%d]\t\t%d\t\t %d\t\t\t %d", i + 1, burst_time[i], total - arrival_time[i], total - arrival_time[i] - burst_time[i]);
wait_time = wait_time + total - arrival_time[i] - burst_time[i]; 
turnaround_time = turnaround_time + total - arrival_time[i]; 
counter = 0; 
} 
if(i == limit - 1) 
{
i = 0; 
}
else if(arrival_time[i + 1] <= total) 
{
i++;
}
else
{
i = 0;
}
} 
average_wait_time = wait_time * 1.0 / limit;
average_turnaround_time = turnaround_time * 1.0 / limit;
printf("\n\nAverage Waiting Time:\t%f", average_wait_time); 
printf("\nAvg Turnaround Time:\t%f\n", average_turnaround_time); 
return 0; 
}
