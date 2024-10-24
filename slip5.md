Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the optimal page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 8, 5, 7, 8, 5, 7, 2, 3, 7, 3, 5, 9, 4, 6, 2
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
/*
Enter number of frames -: 3
Enter number of pages -: 15
Enter page reference string -: 8 5 7 8 5 7 2 3 7 3 5 9 4 6 2
pg=8 |8 
pg=8 |-1
pg=8 |-1
pg=5 |8
pg=5 |5
pg=5 |-1
pg=7 |8
pg=7 |5
pg=7 |7
pg=8 |8
pg=8 |5
pg=8 |7
pg=5 |8
pg=5 |5
pg=5 |7
pg=7 |8
pg=7 |5
pg=7 |7
pg=2 |2
pg=2 |5
pg=2 |7
pg=3 |3
pg=3 |5
pg=3 |7
pg=7 |3
pg=7 |5
pg=7 |7
pg=3 |3
pg=3 |5
pg=3 |7
pg=5 |3
pg=5 |5
pg=5 |7
pg=9 |9
pg=9 |5
pg=9 |7
pg=4 |4
pg=4 |5
pg=4 |7
pg=6 |6
pg=6 |5
pg=6 |7
pg=2 |2
pg=2 |5
pg=2 |7
Total Page Faults -: 9
*/
Q.2 Write a program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following commands. 
myshell$ search f filename pattern :- To display first occurrence of pattern in the file. 
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
