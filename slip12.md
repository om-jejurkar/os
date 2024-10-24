Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the LRU page replacement algorithm. Assume 
the memory of n frames. 
Reference String : 3, 4, 5, 6, 3, 4, 7, 3, 4, 5, 6, 7, 2, 4, 6
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
/*
Enter the no. of frames -: 3
Enter the no. of pages -: 15
Enter the page(reference string) -: 3 4 5 6 3 4 7 3 4 5 6 7 2 4 6
pg=3 | 3 -1 -1
pg=4 | 3 4 -1
pg=5 | 3 4 5
pg=6 | 6 4 5
pg=3 | 6 3 5
pg=4 | 6 3 4
pg=7 | 7 3 4
pg=3 | 7 3 4
pg=4 | 7 3 4
pg=5 | 5 3 4
pg=6 | 5 6 4
pg=7 | 5 6 7
pg=2 | 2 6 7
pg=4 | 2 4 7
pg=6 | 2 4 6
Page Fault is -:13
*/
Q.2 Write a program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following ‘list’ commands as
myshell$ list f dirname :- To print names of all the files in current directory. 
myshell$ list n dirname :- To print the number of all entries in the current directory
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
if(strcmp(tok2,"n")==0)
{
while((dir=readdir(dp))!= NULL)
c++;
printf("no of files directory : %d ",c);
}
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
