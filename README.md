# Chess-game-AI-in-CPP
//I just wrote an AI for chess map situation in C++  and found it interesting to share it. I wrote it as a class and gave it some examples as functions and called them in main. You can change it however you want
/*established from user : Lord Sky - Windows 10 Enterprise - using : Visual Studio 2019 Enterprise ( C++ Console App form ) by Sepehr Lankarani*/
#include <iostream>
#include <conio.h>
using namespace std;

class chess
{
private:
	string map[8][8]; //array for whole the map
	int Wi; // vertical position of white king
	int Wj; // horizontal position of white king
	int Bi; // vertical position of black king
	int Bj; // horizontal position of black king
	bool wWin=0; // says whether white is winning or not
	bool bWin=0; // says whether black is winning or not
public:
	chess() // sets the default positions of a starting chess game

	/* The first B & W say whether the piece is white or black
		R: rook
		N: knight
		B: Bishop
		Q: queen
		K: king
		P: pawn
	*/
	{
		map[0][0] = "BR";
		map[0][1] = "BN";
		map[0][2] = "BB";
		map[0][3] = "BQ";
		map[0][4] = "BK";
		map[0][5] = "BB";
		map[0][6] = "BN";
		map[0][7] = "BR";
		for (int i = 0; i < 8; i++)
			map[1][i] = "BP";
		map[7][0] = "WR";
		map[7][1] = "WN";
		map[7][2] = "WB";
		map[7][3] = "WQ";
		map[7][4] = "WK";
		map[7][5] = "WB";
		map[7][6] = "WN";
		map[7][7] = "WR";
		for (int i = 0; i < 8; i++)
			map[6][i] = "WP";
		for (int i = 2; i < 6; i++)
			for (int j = 0; j < 8; j++)
				map[i][j] = "  ";
	}

	void situation() // says the situation of the game
	{
		bool wchanging=0,bchanging=0;
		kingLocator();
		wWinC(Bi, Bj);
		if (wWin == 1)
		{
			if (Bi - 1 >= 0)
			{
				wWinC(Bi - 1, Bj);
				if (wWin == 0)
					wchanging=1;
			}
		}
		if (wWin == 1)
			if (Bi + 1 <= 7)
			{
				wWinC(Bi + 1, Bj);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if (Bj - 1 >= 0)
			{
				wWinC(Bi, Bj - 1);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if (Bj + 1 <= 7)
			{
				wWinC(Bi, Bj + 1);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if ((Bi - 1 >= 0) && (Bj - 1 >= 0))
			{
				wWinC(Bi - 1, Bj - 1);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if ((Bi + 1 <= 7) && (Bj - 1 >= 0))
			{
				wWinC(Bi + 1, Bj - 1);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if ((Bi - 1 >= 0) && (Bj + 1 >= 7))
			{
				wWinC(Bi - 1, Bj + 1);
				if (wWin == 0)
					wchanging = 1;
			}
		if (wWin == 1)
			if ((Bi + 1 <= 7) && (Bj + 1 <= 7))
			{
				wWinC(Bi + 1, Bj + 1);
				if (wWin == 0)
					wchanging = 1;
			}

		bWinC(Wi, Wj);

		if (bWin == 1)
			if (Wi - 1 >= 0)
			{
				bWinC(Wi - 1, Wj);
				if (bWin == 0)
					bchanging=1;
			}
		if (bWin == 1)
			if (Bi + 1 <= 7)
			{
				bWinC(Wi + 1, Wj);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if (Wj - 1 >= 0)
			{
				bWinC(Wi, Wj - 1);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if (Wi + 1 <= 7)
			{
				bWinC(Wi, Wj + 1);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if ((Wi - 1 >= 0) && (Wj - 1 >= 0))
			{
				bWinC(Wi - 1, Wj - 1);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if ((Wi + 1 <= 7) && (Wj - 1 >= 0))
			{
				bWinC(Wi + 1, Wj - 1);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if ((Wi - 1 >= 0) && (Wj + 1 <= 7))
			{
				bWinC(Wi - 1, Wj + 1);
				if (bWin == 0)
					bchanging = 1;
			}
		if (bWin == 1)
			if ((Wi + 1 <= 7) && (Wj + 1 <= 7))
			{
				bWinC(Wi + 1, Wj + 1);
				if (bWin == 0)
					bchanging = 1;
			}

		if (wWin && wchanging == 0)
			cout << "White totally won\n\n";
		else if (wWin == 0 && wchanging > 0)
			cout << "White is winning but black can move to a different positions to change the results\n\n";
		else if (bWin && bchanging == 0)
			cout << "Black totally won\n\n";
		else if (bWin == 0 && bchanging > 0)
			cout << "Black is winning but white can move to a different positions to change the results\n\n";
		else if (bWin == 0 && wWin == 0)
			cout << "No one is winning yet\n\n";
		else if(bWin == 1 && wWin == 1)
			cout << "It's a total draw\n\n";

	}

	void kingLocator() // locates both black and white kings
	{
		for (int i = 0; i < 8; i++)
			for (int j = 0; j < 8; j++)
			{
				if (map[i][j] == "BK")
				{
					Bi = i;
					Bj = j;
				}
				else if (map[i][j] == "WK")
				{
					Wi = i;
					Wj = j;
				}
			}
	}
	


	void bWinC(int i , int j) // check if the white is winning
	{
		bWin = 0;
		bool empC = 1;
		//Up
		if (map[i - 1][j] == "BK")
			bWin = 1;
		else
			for (int pi = i - 1; pi >= 0&&empC==1; pi--)
			{
				if (map[pi][j] == "  ")
					empC = 1;
				else if (map[pi][j] != "  " && map[pi][j] != "BQ" && map[pi][j] != "BR")
					empC = 0;
				else if (map[pi][j] == "BQ" || map[pi][j] == "BR")
					bWin = 1;
			}
		//Down
		empC = 1;
		if (map[i + 1][j] == "BK")
			bWin = 1;
		else
			for (int pi = i + 1; pi < 8 && empC == 1; pi++)
			{
				if (map[pi][j] == "  ")
					empC = 1;
				else if (map[pi][j] != "  " && map[pi][j] != "BQ" && map[pi][j] != "BR")
					empC = 0;
				else if (map[pi][j] == "BQ" || map[pi][j] == "BR")
					bWin = 1;
			}
		//Left
		empC = 1;
		if (map[i][j - 1] == "BK")
			bWin = 1;
		else
			for (int pj = j - 1; pj >= 0 && empC == 1; pj--)
			{
				if (map[i][pj] == "  ")
					empC = 1;
				else if (map[i][pj] != "  " && map[i][pj] != "BQ" && map[i][pj] != "BR")
					empC = 0;
				else if (map[i][pj] == "BQ" || map[i][pj] == "BR")
					bWin = 1;
			}
		//Right
		empC = 1;
		if (map[i][j + 1] == "BK")
			bWin = 1;
		else
			for (int pj = j + 1; pj < 8 && empC == 1; pj++)
			{
				if (map[i][pj] == "  ")
					empC = 1;
				else if (map[i][pj] != "  " && map[i][pj] != "BQ" && map[i][pj] != "BR")
					empC = 0;
				else if (map[i][pj] == "BQ" || map[i][pj] == "BR")
					bWin = 1;
			}
		
		//Upper Right F
		empC = 1;
		if (map[i - 1][j + 1] == "BP")
			bWin = 1;
		else
			for (int pi = i - 1, pj = j + 1; pi >= 0 && pj < 8 && empC == 1; pi--, pj++)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "BB" && map[pi][pj] != "BQ")
					empC = 0;
				else if (map[pi][pj] == "BB" || map[pi][pj] == "BQ")
					bWin = 1;
			}
		//Upper Left F
		empC = 1;
		if (map[i - 1][j - 1] == "BP")
			bWin = 1;
		else
			for (int pi = i - 1, pj = j - 1; pi >= 0 && pj >= 0 && empC == 1; pi--, pj--)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "BB" && map[pi][pj] != "BQ")
					empC = 0;
				else if (map[pi][pj] == "BB" || map[pi][pj] == "BQ")
					bWin = 1;
			}
		//Downer Left
		empC = 1;
			for (int pi = i + 1, pj = j - 1; pi < 8 && pj >= 0 && empC == 1; pi++, pj--)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "BB" && map[pi][pj] != "BQ")
					empC = 0;
				else if (map[pi][pj] == "BB" || map[pi][pj] == "BQ")
					bWin = 1;
			}

		//Downer Right
		empC = 1;
			for (int pi = i + 1, pj = j + 1; pi < 8 && pj < 8 && empC == 1; pi++, pj++)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "BB" && map[pi][pj] != "BQ")
					empC = 0;
				else if (map[pi][pj] == "BB" || map[pi][pj] == "BQ")
					bWin = 1;
			}
		
		//Horse
			if (map[i - 1][j + 2] == "BN" || map[i - 1][j - 2] == "BN" || map[i + 1][j + 2] == "BN" || map[i + 1][j - 2] == "BN" || map[i - 2][j - 1] == "BN" || map[i + 2][j - 1] == "BN" || map[i - 2][j + 1] == "BN" || map[i + 2][j + 1] == "BN")
				bWin = 1;
	}	

	

	void wWinC(int i , int j) // checks if the black is winning
	{
		wWin = 0;
		bool empC = 1;
		//Up
		if (map[i - 1][j] == "WK")
			wWin = 1;
		else
			for (int pi = i - 1; pi >= 0 && empC == 1; pi--)
			{
				if (map[pi][j] == "  ")
					empC = 1;
				else if (map[pi][j] != "  " && map[pi][j] != "WQ" && map[pi][j] != "WR")
					empC = 0;
				else if (map[pi][j] == "WQ" || map[pi][j] == "WR")
					wWin = 1;
			}
		//Down
		empC = 1;
		if (map[i + 1][j] == "WK")
			wWin = 1;
		else
			for (int pi = i + 1; pi < 8 && empC == 1; pi++)
			{
				if (map[pi][j] == "  ")
					empC = 1;
				else if (map[pi][j] != "  " && map[pi][j] != "WQ" && map[pi][j] != "WR")
					empC = 0;
				else if (map[pi][j] == "WQ" || map[pi][j] == "WR")
					wWin = 1;
			}
		//Left
		empC = 1;
		if (map[i][j - 1] == "WK")
			wWin = 1;
		else
			for (int pj = j - 1; pj >= 0 && empC == 1; pj--)
			{
				if (map[i][pj] == "  ")
					empC = 1;
				else if (map[i][pj] != "  " && map[i][pj] != "WQ" && map[i][pj] != "WR")
					empC = 0;
				else if (map[i][pj] == "WQ" || map[i][pj] == "WR")
					wWin = 1;
			}
		//Right
		empC = 1;
		if (map[i][j + 1] == "BK")
			wWin = 1;
		else
			for (int pj = j + 1; pj < 8 && empC == 1; pj++)
			{
				if (map[i][pj] == "  ")
					empC = 1;
				else if (map[i][pj] != "  " && map[i][pj] != "WQ" && map[i][pj] != "WR")
					empC = 0;
				else if (map[i][pj] == "WQ" || map[i][pj] == "WR")
					wWin = 1;
			}

		//Upper Right F
		empC = 1;
			for (int pi = i - 1, pj = j + 1; pi >= 0 && pj < 8 && empC == 1; pi--, pj++)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "WB" && map[pi][pj] != "WQ")
					empC = 0;
				else if (map[pi][pj] == "WB" || map[pi][pj] == "WQ")
					wWin = 1;
			}
		//Upper Left F
		empC = 1;
			for (int pi = i - 1, pj = j - 1; pi >= 0 && pj >= 0 && empC == 1; pi--, pj--)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "WB" && map[pi][pj] != "WQ")
					empC = 0;
				else if (map[pi][pj] == "WB" || map[pi][pj] == "WQ")
					wWin = 1;
			}
		//Downer Left
		empC = 1;
		if (map[i + 1][j + 1] == "WP")
			wWin = 1;
		else
			for (int pi = i + 1, pj = j - 1; pi < 8 && pj >= 0 && empC == 1; pi++, pj--)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "WB" && map[pi][pj] != "WQ")
					empC = 0;
				else if (map[pi][pj] == "WB" || map[pi][pj] == "WQ")
					wWin = 1;
			}

		//Downer Right
		empC = 1;
		if (map[i + 1][j + 1] == "WP")
			wWin = 1;
		else
			for (int pi = i + 1, pj = j + 1; pi < 8 && pj < 8 && empC == 1; pi++, pj++)
			{
				if (map[pi][pj] == "  ")
					empC = 1;
				else if (map[pi][pj] != "  " && map[pi][pj] != "WB" && map[pi][pj] != "WQ")
					empC = 0;
				else if (map[pi][pj] == "WB" || map[pi][pj] == "WQ")
					wWin = 1;
			}
		//Horse
		if (map[i - 1][j + 2] == "WN" || map[i - 1][j - 2] == "WN" || map[i + 1][j + 2] == "WN" || map[i + 1][j - 2] == "WN" || map[i - 2][j - 1] == "WN" || map[i + 2][j - 1] == "WN" || map[i - 2][j + 1] == "WN" || map[i + 2][j + 1] == "WN")
			bWin = 1;
	}

	void show() // shows all the current positions on the map
	{
		for (int i = 0; i < 8; i++)
		{
			for (int j = 0; j < 8; j++)
				cout << map[i][j]<<' ';
			cout << endl;
		}
	}
	
	void test1()
	{
		map[3][4] = "WK";
		map[7][4] = "  ";
		map[4][5] = "BB";
		map[6][4] = "  ";
		map[1][6] = "  ";
		map[0][5] = "  ";
	}

	void test2()
	{
		map[3][4] = "BK";
		map[0][4] = "  ";
		map[2][5] = "WB";
		map[7][2] = "  ";
		map[1][4] = "  ";
		map[2][3] = "WQ";
		map[7][6] = "  ";
		map[5][5] = "WN";
	}
	
};

int main()
{
	chess a,b;
	a.test1();
	a.situation();
	a.show();
	_getch();
	system("CLS");
	b.test2();
	b.situation();
	b.show();
	_getch();
	return 0;
}
