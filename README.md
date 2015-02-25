# base-maze-game
A simple baze mase capture the flag game in c++. 
//C.Galicia Colour Maze (Capture the Flag) started on 10-13-2014
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
#include <windows.h>


//////////////////////////////
struct Position 
{
	int x;
	int y;
};
/////////////////////////////
struct Position player; 
struct Position target;
struct Position enemy1, enemy2; 
char direction1=1, direction2=1;
//////////////////////////////
void HandleEnemy();
int Modulo(int nb, int mod); 
void HandlePlayer(char input);
void DrawMap();
////////////////////////////
void main()
{
	//initialize starting position for player, enemy, and target 
	player.x=2, player.y=5; 
	target.x=3, target.y=0; 
	enemy1.x=0, enemy1.y=1;
	enemy2.x=5, enemy2.y=3; 
	/*Game Loop */
	SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 9);
while (1)
{
	DrawMap();

	char input;
	printf("Test your might:l(Left),r(Right),u(Up),d(Down) and e(Exit)\n");
	input = getch();
	if (input == 'e')
		goto Exit;
	else
	{
		HandlePlayer(input);
		HandleEnemy();


		system("cls");
		  /* colliding with an enemy */
	 if ((player.x == enemy1.x && player.y == enemy1.y) ||
		(player.x == enemy2.x && player.y == target.y))
	 {
		 printf("Game Over\n");
		 system("pause"); 
		
	 }
	    /*Targert reached*/
	 else if (player.x == target.x && player.y == target.y)
	 {
		 printf("Flawless Victory\n");
		 system("pause"); 
		 
		
	 }
	}
}
Exit:      /* Label */
  printf("\n");
}

///////////////////////////////
void HandlePlayer(char input)
{
	int tempx=player.x,
	   tempy=player.y; 
	if (input=='l') 
	   tempx--; 
	else if (input=='r') 
		tempx++;
	else if(input=='u') 
		tempy--;
	else if(input=='d') 
		tempy++;
	
	player.x = Modulo(tempx, 6);
	player.y=  Modulo(tempy, 6);
}
///////////////////////////////
void HandleEnemy()
{
	//Enemy 1
	if (direction1)
	   enemy1.x++; 
	else
		enemy1.x--; 
	
	if (enemy1.x==0 || enemy1.x==5)
		direction1 =!direction1; 

	//Enemy2
	if (direction2)
		enemy2.x -=2; 
	else
		enemy2.x += 2; 
	if (enemy2.x<=0 || enemy2.x>=5)
	{
		if (direction2)
			enemy2.x++; 
		else
			enemy2.x--;
		direction2 = !direction2;
	}
}
////////////////////////////////
int Modulo(int nb, int mod)
{
	if (nb < 0)
	   nb +=mod;
	return nb % mod;
}


void DrawMap()
{
	int y = 0;
	for (y = 0; y<6; y++) /* draws rows */
	{
	printf("\t-----------------\n"); 
	printf("\t");

	int x = 0;
	for (x = 0; x<7; x++)  /*draw columns */
	{
		printf("|");

		 /*Target position               */
	   if  (x == target.x && y == target.y)
		printf("T "); 
	   
	    /*Enemy1 position                 */
	 else if (x == enemy1.x && y == enemy1.y)
		 printf("<>");
	   
	   /*Enemy2 position                 */
	 else if (x == enemy2.x && y == enemy2.y)
		 printf("<>");
	 
	 /*Player position                   */
	 else if (x == player.x && y ==player.y)
		 printf("=^.^= ");

	 else
	   printf("  ");
	}
	printf("\n");
	}
	printf("\t-----------------\n");
	printf("\n");
}








