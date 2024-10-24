Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the FIFO page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 2, 4, 5, 6, 9, 4, 7, 3, 4, 5, 6, 7, 2, 4, 7, 1
#include<stdio.h>
int page[40];
int n,frame[5],ref[50],victim=-1,pf=0;
int searchp(int p)
{
int i;
for(i=0;i<n;i++)
if(frame[i]==p)
return i;
return -1;
}
int selectvictim()
{
victim++;
return victim%n;
}
int main()
{
int i,m;
printf("\nEnter the no. of pages -: ");
scanf("%d",&m);
printf("\nEnter the reference string -: ");
for(i=0;i<m;i++)
scanf("%d",&page[i]);
printf("\nEnter the no. of frames -: ");
scanf("%d",&n);
for(i=0;i<n;i++)
frame[i]=-1;
for(i=0;i<m;i++)
{
int k,j;
k=searchp(page[i]);
if(k==-1)
{
pf++;
k=selectvictim();
frame[k]=page[i];
}
printf("\n %d",page[i]);
for(j=0;j<n;j++)
printf("\t%d",frame[j]);
}
printf("\n");
printf("\nPage Fault -: %d",pf);
}
/*
Enter the no. of pages -: 16
Enter the reference string -: 2 4 5 6 9 4 7 3 4 5 6 7 2 4 7 1
Enter the no. of frames -: 3
2 2 -1 -1
4 2 4 -1
5 2 4 5
6 6 4 5
9 6 9 5
4 6 9 4
7 7 9 4
3 7 3 4
4 7 3 4
5 7 3 5
6 6 3 5
7 6 7 5
2 6 7 2
4 4 7 2
7 4 7 2
1 4 1 2
Page Fault -: 14
*/
Q.2 Write a program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following ‘list’ commands as 
myshell$ list f dirname :- To print names of all the files in current directory. 
myshell$ list i dirname :- To print names and inodes of the files in the current directory.
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
if(strcmp(tok2,"i")==0)
{
while((dir=readdir(dp))!= NULL)
printf("%s\t\t%d\n",dir->d_name,dir->d_ino);
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
