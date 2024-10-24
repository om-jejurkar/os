Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the FIFO page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 8, 5, 7, 8, 5, 7, 2, 3, 7, 3, 5, 9, 4, 6, 2
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
Enter the no. of pages -: 15
Enter the reference string -: 8 5 7 8 5 7 2 3 7 3 5 9 4 6 2
Enter the no. of frames -: 3
8 8 -1 -1
5 8 5 -1
7 8 5 7
8 8 5 7
5 8 5 7
7 8 5 7
2 2 5 7
3 2 3 7
7 2 3 7
3 2 3 7
5 2 3 5
9 9 3 5
4 9 4 5
6 9 4 6
2 2 4 6
Page Fault -: 10
*/
Q.2 Write a program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following commands. 
myshell$ search f filename pattern :- To display first occurrence of pattern in the file. 
myshell$ search a filename pattern :- To search all the occurrence of 
pattern in the file.
#include<stdio.h>
#include<unistd.h>
#include<string.h>
#include<stdlib.h>
void search(char *tok2,char *tok3,char *tok4)//tok2:command tok3:pattern tok4:Textfilename
{
FILE *fp;
int lineno=0,count=0;
char str[50];
fp=fopen(tok4,"r");
if(fp==NULL)
{
printf("File does not exist");
exit(0);
}
else
{
if(strcmp(tok2,"f")==0)//First occurance of pattern
{
while(!feof(fp))
{
fgets(str,50,fp);
lineno++;
if(strstr(str,tok3))
{
printf("First occurance of '%s' is on line : %d\n",tok3,lineno);
break;
}
}
}
if(strcmp(tok2,"a")==0)//Total occurances of pattern
{
while(!feof(fp))
{
fgets(str,50,fp);
lineno++;
if(strstr(str,tok3))
{
printf("\n Total Occurance of pattern:\n %d %s\n",lineno,str);
} 
}
}
}
}
void main(int argc,char *argv[])
{
char cmd[20],tok1[20],tok2[20],tok3[20],tok4[20];
while(1)
{
printf("\nMyShell$:");
gets(cmd);
if(strcmp(tok1,"exit")==0)
exit(0);
int ch=sscanf(cmd,"%s%s%s%s",tok1,tok2,tok3,tok4);
if(ch==4)
{
if(strcmp(tok1,"search")==0)
{
search(tok2,tok3,tok4);
continue;
}
}
}
}
