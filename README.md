# password-hiding
/*
The function can be used on unix and win32. When you input your password, the characters will be substituded by "*".
*/
#if defined(unix)
#include<curses.h>
#elif defined(_WIN32)
#include<conio.h>
#include<stdio.h>
#else
#error "Unknown OS"
#endif

#include <stdlib.h>
#define KEY_LEN 20


char * get_key()
{
	char ch;
	char *key=(char *)malloc(sizeof(char)*KEY_LEN);
	char *p=key;
	int i=0;*(p+i)='\0';
	
    while ((ch=getch())!='\r')
	{
    	if (ch=='\b')
		{
    		if (i>0)
			{
    			i=i-1;
    			*(p+i)='\0';
    			printf("\b \b");
			}
		}
		else
		{
			*(p+i)=ch;
			i++;
			*(p+i)='\0'; 
			printf("*");
		} 
	}
return key;
} 

int main()
{
  char *key;

#if defined(unix)
    initscr();
    cbreak();
    noecho();
    key=get_key(); 
//	printw("\n%s",key);

    getch();
    endwin();

#elif defined(_WIN32)
	key=get_key();
//	printf("\n%s",key);


#endif
}
