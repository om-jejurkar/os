Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the MFU page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 8, 5, 7, 8, 5, 7, 2, 3, 7, 3, 5, 9, 4, 6, 2
#include<stdio.h>
struct node
{
int pno,freq;
}frames[20];
int n;
int page_found(int pno)
{
int fno;
for(fno=0;fno<n;fno++)
if(frames[fno].pno==pno)
return fno;
return -1;
}
int get_free_frame()
{
int fno;
for(fno=0;fno<=n;fno++)
if(frames[fno].pno==-1)
return(fno);
return(-1);
}
int get_mfu_frame()
{
int fno;
int selfno=0;
for(fno=1;fno<n;fno++)
if(frames[fno].freq>frames[selfno].freq)
selfno=fno;
return selfno;
}
void main()
{
int p_request[1000];
int size;
int page_fault=0,i,j,fno;
printf("\n Enter how many pages -: ");
scanf("%d",&size);
printf("\n Enter Reference string -: ");
for(i=0;i<size;i++)
scanf("%d",&p_request[i]);
printf("\n How many frames -: ");
scanf("%d",&n);
for(i=0;i<n;i++)
{
frames[i].pno=-1;
frames[i].freq=0;
}
printf("\n Page No Page Frames Page Fault");
printf("\n-------------------------------------------------------");
for(i=0;i<size;i++)
{
j=page_found(p_request[i]);
if(j==-1)
{
j=get_free_frame();
if(j==-1)
j=get_mfu_frame();
page_fault++;
frames[j].pno=p_request[i];
frames[j].freq=1;
printf("\n %d\t",p_request[i]);
for(fno=0;fno<n;fno++)
printf("%d\t",frames[fno].pno);
printf(" : YES ");
}
else
{
printf("\n%d\t",p_request[i]);
frames[j].freq++;
for(fno=0;fno<n;fno++)
printf("%d\t",frames[fno].pno);
printf(" : NO ");
}
}
printf("\n------------------------------------------------------");
printf("\n Number of Page_Falts -: %d",page_fault);
}
/*
Enter how many pages -: 15
Enter Reference string -: 8 5 7 8 5 7 2 3 7 3 5 9 4 6 2
How many frames -: 3
Page No Page Frames Page Fault
-------------------------------------------------------
8 8 -1 -1 : YES
5 8 5 -1 : YES
7 8 5 7 : YES
8 8 5 7 : NO
5 8 5 7 : NO
7 8 5 7 : NO
2 2 5 7 : YES
3 2 3 7 : YES
7 2 3 7 : NO
3 2 3 7 : NO
5 2 3 5 : YES
9 2 9 5 : YES
4 4 9 5 : YES
6 6 9 5 : YES
2 2 9 5 : YES
------------------------------------------------------
Number of Page_Falts -: 10
*/
Q.2 Write a program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following commands. 
myshell$ search a filename pattern :- To search all the occurrence of pattern in the file. 
myshell$ search c filename pattern :- To count the number of occurrence 
of pattern in the file.
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
if(strcmp(tok2,"c")==0)//Total number of occurances of pattern
{
while(!feof(fp))
{
fgets(str,50,fp);
if(strstr(str,tok3))
{
count++;
}
}
printf("Total number occurance of pattern(%s) is : %d\n",tok3,count);
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
