Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the MRU page replacement algorithm. 
Assume the memory of n frames. 
Reference String : 8, 5, 7, 8, 5, 7, 2, 3, 7, 3, 5, 9, 4, 6, 2
#include<stdio.h>
int main()
{
int ref_str[20],frame[10];
int f,n,i,k,fcount=0,avail;
printf("\nPls. Enter the no. of pages:");
scanf("%d",&n);
printf("\nEnter the Reference String:");
for(i=1;i<=n;i++)
scanf("%d",&ref_str[i]);
printf("\nEnter the no. of frames:");
scanf("%d",&f);
for(i=0;i<f;i++)
frame[i] = -1;
printf("\nRef String \t Frames \t page falut or hit\n");
for(i=1;i<=n;i++)
{
printf("%d",ref_str[i]);
avail = 0;
for(k=0;k<f;k++)
if(frame[k] == ref_str[i]) // check ref_string already in frame
{ 
avail =1;
for(k=0;k<f;k++)
printf("\t%d",frame[k]);
printf("\tH");
}
else if(frame[k] == -1) 
{ 
avail =1; 
fcount++;
frame[k] = ref_str[i];
for(k=0; k<f; k++)
printf("\t%d",frame[k]);
printf("\tF");
break;
}
if(avail == 0) // if ref_string is not in frame
{ 
for(k=0; k<f; k++)
{
if(frame[k] == ref_str[i-1] ) // check most recently used page (ref_str[i-1])
{
frame[k] = ref_str[i];
fcount++;
for(k=0;k<f;k++)
{
printf("\t%d",frame[k]);
}
printf("\tF");
}
}
}
printf("\n");
}
printf("\nTotal number of Page Fault: %d",fcount);
} 
Q.2 Write a programto implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following commands. 
myshell$ search f filename pattern :- To display first occurrence of pattern in the file. 
myshell$ search a filename pattern :- To search all the occurrence of pattern in the file.
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
