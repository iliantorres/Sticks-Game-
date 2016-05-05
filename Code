// Game of Sticks By Ilian Torres
// ----------> Program Description <---------- //
// This program was made to keep track of the score between two player
// in a game of sticks. The players must first give the inicial amount
// of sticks in the game (between 10-100). Then the program will give
// the player three opcions:
//      1) Player vs Player: The opcion ask the 1st player how many
//         sticks he collected (between 1-3). Then ask the 2nd player
//         the same question. While the players are getting sticks the
//         program substracts the number of sticks the player collected
//         from the total of sticks. The player that takes the last stick
//         is therefore the loser.
//      2) Player vs AI: This opcion is very much like the first only
//         instead of playing with a person the player will play with
//         an unexperienced AI. The AI will pick the sticks random
//         (obeying the rules of the game) and save the data when it wins.
//         Therefore the AI slowly learns while playing with the player.
//      3) Player vs AI: This opcion is very much like the second only
//         the AI has been put to play against the computer for 1000 rounds
//         that way the AI gets trained to play against the player.
// ----------> END of Program Description<---------- //
//


#include <iostream>
#include <time.h>
#include <vector>

using namespace std;


// Function Intro is the introdution of the game of sticks. Intro asks for
// the number of sticks and the opcion the player wishes to play however it has
// an imput validation so the user puts the designated amount.

void Intro(int &sticksT,int &opcion){
    cout << "How many sticks are there on the table initially (10-100)? ";
    cin >> sticksT;
    while (sticksT < 10 || sticksT > 100){
        cout << "Please enter a number between 10 and 100.\n";
        cout << "How many sticks are there on the table initially (10-100)? ";
        cin >> sticksT;
    }
    cout << "Options: \n"
         << "Play against a friend (1)\n"
         << "Play against the computer (2) \n"
         << "Play against a trained computer(3) \n"
         << "Which option do you take (1-3)? ";

    cin >> opcion;

    while (opcion<1 || opcion>3){
        cout<<"Invalid opcion. Try agian.\n"
           <<"Which option do you take (1-3)? ";
        cin>>opcion;
    }
}

// VerifySticks verify that the players obey the rules of how many sticks can be taken during of the game.

int VerifySticks(int sticks,int sticksT,int player){

    while (sticks<1 || sticks>3 || sticksT < sticks || (sticksT>1 && sticksT <= 3 && sticksT==sticks) ){
        if (sticksT == 1 || sticksT == 2){
            cout << "Player " << player <<" There is only one possible play, please enter 1: ";
            cin >> sticks;
        }
        else if (sticks>3 || sticks==0){
            cout <<"Please enter a number between 1 and 3\n";
            cout << "Player " << player << " : How many sticks do you take (1-3)? ";
            cin  >> sticks;
        }
        else{
            cout << "Player " << player <<" please enter a number less than " << sticksT << " but greater than 0: ";
            cin >> sticks;
        }
    }
    return sticks;
}

// VectorCreator creates two vectors.AIplays with vector sticksTotal with vector's vectors three zeros.
// and AItrained with vector sticksTotal with vector's vectors three ones;

void VectorCreator(vector < vector <int> > &AItrained,vector < vector <int> > &AIplays,int sticksTotal){
    vector <int> wins;
    for (int i =0;i<3; i++)
        wins.push_back(0);
    for (int i= 0;i<=sticksTotal;i++)
        AIplays.push_back(wins);
    for (int i=0;i<3;i++)
        AItrained.push_back(wins);
    for (int i=0; i<3;i++)
        wins[i]=1;
    for (int i= 3;i<=sticksTotal;i++)
        AItrained.push_back(wins);
}

// SetZero sets a vector's vector to all zeros.

void SetZero(vector  < vector <int> > &AIplays,int sticksTotal){
    for (int i= 0;i<=sticksTotal;i++){
        for (int j=0;j<3;j++)
            AIplays[i][j]=0;
    }
}


// UntrainedAI gets the number of sticksT in the game and finds the number of 1's 2's 3's in AItrained.
// Then depending if its greater, equal or less than 3 it adds the numbers. Then it takes a random number
// and mod it to the addition of the numbers. That number then is compared to know what the AI should
// return to the game. All the while AIplays is keeping trak of the number that was used.

int UntrainedAI(vector  < vector <int> > &AIplays,vector  < vector <int> > &AItrained,int sticksT){
    int randnumber;
    int number1=AItrained[sticksT][0];
    int number2=AItrained[sticksT][1];
    int number3=AItrained[sticksT][2];

    if (sticksT>3){

        randnumber=rand()%(number1+number2+number3);
    }
    else if (sticksT==3){

        randnumber=rand()%(number1+number2);
    }
    else //(sticksT==1 || sticksT==2)
        return 1;


    if (randnumber<number1){
        AIplays[sticksT][0]=1;
        return 1;
    }
    else if (randnumber<(number2+number1)){
        AIplays[sticksT][1]=1;
        return 2;
    }
    else {
        AIplays[sticksT][2]=1;
        return 3;
    }
}

// AddAndSubtract add and subtract vectors depending if the computer won or lost.

void AddAndSubtract(int player,int sticksTotal,int &sticksT,vector < vector <int> > &AItrained,vector < vector <int> > &AIplays){
    if (player == 1){
        for (int i=0;i<=sticksTotal;i++){
            for (int j=0;j<3;j++)
                AItrained[i][j]=AItrained[i][j]+AIplays[i][j];
        }
    }

    else{
        for (int i=0;i<=sticksTotal;i++){
            for (int j=0;j<3;j++)
                if (AItrained[i][j]>1)
                    AItrained[i][j]=AItrained[i][j]-AIplays[i][j];
        }
    }
    sticksT=sticksTotal;
    SetZero(AIplays,sticksT);

}

// TrainingAI trains the AI using the function UntrainedAI for 1000 rounds.

void trainingAI(vector  < vector <int> > AIplays,vector  < vector <int> > &AItrained,int sticksT,int sticksTotal){
    int  count=0,player=1,sticks;
    vector < vector <int> > AIplays2;
    vector < vector <int> > AItrained2;

    VectorCreator(AItrained2,AIplays2, sticksTotal);


    for (int i=0;i<1000;i++){
        while (sticksT > 0){
            count = count + 1;
            if (count%2 == 1){
                player = 1;
                sticks=UntrainedAI(AIplays2,AItrained2,sticksT);
            }
            else{
                player = 2;
                sticks=UntrainedAI(AIplays,AItrained,sticksT);
            }

            sticksT = sticksT - sticks;
        }
        if (player==1){
            AddAndSubtract(player, sticksTotal, sticksT, AItrained, AIplays);
            player=2;
            AddAndSubtract(player, sticksTotal,sticksT, AItrained2, AIplays2);
        }
        else{
            AddAndSubtract(player=2, sticksTotal,sticksT, AItrained, AIplays);
            player=1;
            AddAndSubtract(player=1, sticksTotal,sticksT, AItrained2, AIplays2);
        }

    }
}

// PlayAgain ask the user to if he wants to play again.

void PlayAgain(int &again){
    cout << "Play again (1 = yes, 0 = no)?: ";
    cin >> again;
    while ( again<0 || again>1){
        cout << "Invalid Entry. Please enter 1 for yes or 0 for no: ";
        cin >> again;
    }
}



int main() {
    int sticksT=0,count=0,again=1,opcion=0;
    int sticks,player,sticksTotal;
    vector < vector <int> > AIplays;
    vector < vector <int> > AItrained;

    srand(clock());

    cout << "Welcome to the game of sticks!\n";

    Intro(sticksT,opcion);
    sticksTotal=sticksT;
    if(opcion == 2 || opcion == 3)
        VectorCreator(AItrained,AIplays, sticksTotal);
    while (opcion==1 && again==1){
        while (sticksT > 0){
            cout << endl;
            count = count + 1;
            if (sticksT == 1)
                cout << "There is 1 stick on the board." <<endl;
            else
                cout << "There are " << sticksT << " sticks on the board. " << endl;
            if (count%2 == 1)
                player=1;
            else
                player=2;
            cout << "Player " << player << " : How many sticks do you take (1-3): ";
            cin >> sticks;
            sticks=VerifySticks(sticks,sticksT,player);
            sticksT = sticksT - sticks;
        }
        if (player == 1){
            cout << "Player 1, you lose." << endl;

        }
        else
            cout << "Player 2, you lose." << endl;

        PlayAgain(again);
        sticksT=sticksTotal;
        count=0;
    }

    while ((opcion==2 || opcion ==3) && again==1){
        SetZero(AIplays,sticksT);
        int blah=0,blah2=0;
        if (opcion == 3){
            cout << "Training AI please wait..." << endl;
            trainingAI(AIplays,AItrained,sticksT,sticksTotal);
            while (blah<21){
                cout<<blah<<" ";
                while(blah2<3){
                cout<< AItrained[blah][blah2]<<" ";
                blah2=blah2+1;
                }
                cout<< endl;
                blah=blah+1;
            }
        }
        while (sticksT > 0){
            cout << endl;
            count = count + 1;
            if (sticksT == 1)
                cout << "There is 1 stick on the board." <<endl;
            else
                cout << "There are " << sticksT << " sticks on the board. "<<endl;;

            if (count%2 == 1){
                player = 1;
                cout << "Player 1 : How many sticks do you take (1-3): ";
                cin >> sticks;
                sticks=VerifySticks(sticks,sticksT,player);
            }
            else{
                player = 2;
                sticks=UntrainedAI(AIplays,AItrained,sticksT);
                cout << "AI selects " << sticks;
            }
            cout<<endl;
            sticksT = sticksT - sticks;
        }

        if (player == 1)
            cout << "You lose." << endl;
        else
            cout << "AI loses." << endl;

        AddAndSubtract(player, sticksTotal,sticksT, AItrained, AIplays);
        sticksT=sticksTotal;
        count=0;
        SetZero(AIplays,sticksT);
        PlayAgain(again);
    }
}

