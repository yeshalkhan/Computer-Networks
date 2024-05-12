#include <iostream>
#include <vector>
#include <string>
using namespace std;

void generalGraph(vector<vector<char>>& graph, const string binary, int cols, int space, bool drawXAxis)
{
    cout << "\nAmplitude\n\n";
    graph[0][0] = '^';
    int j = 4, len = binary.length();

    //display bit pattern on top
    for (int i = 0; i < len; i++)
    {
        graph[0][j] = binary[i];
        j = j + space;
    }

    //for 2 vertical lines
    graph[4][0] = graph[1][0] = graph[2][0] = graph[3][0] = graph[5][0] = graph[6][0] =
        graph[4][2] = graph[1][2] = graph[2][2] = graph[3][2] = graph[5][2] = graph[6][2] = '|';

    if (drawXAxis)
    {   //to draw x-axis at the middle
        for (int j = 3; j < cols; j++)
            graph[3][j] = '_';
    }
}

void printMatrix(vector<vector<char>>& graph, int rows, int cols)
{
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
            cout << graph[i][j];
        cout << endl;
    }
}

void NRZ_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 20 + 3 * len;      //3 columns for each bit & 20 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 3, false);

    //draw signal 
    int j = 3;
    for (int i = 0; i < len; i++)
    {
        //check the previous bit, if it is different from current bit then draw a vertical line
        if (i > 0 && binary[i - 1] != binary[i])
            graph[3][j] = graph[2][j] = '|';

        if (i > 0)  //space after each bit to distinguish between bits
            j++;    

        //if bit is 0, draw line on x-axis else above x-axis
        if (binary[i] == '0')
            graph[3][j++] = graph[3][j++]  = '_';
        else
            graph[1][j++] = graph[1][j++]  = '_';
        
    }

    j = j + 3;
    graph[3][j++] = graph[3][j++] = graph[3][j++] = graph[3][j++] = '-';
    graph[3][j++] = '>';
    graph[3][j++] = 'T'; graph[3][j++] = 'i'; graph[3][j++] = 'm'; graph[3][j++] = 'e';
    printMatrix(graph, rows, cols);
    cout << endl << endl;
}

void NRZ_L_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 10 + 3 * len;      //3 columns for each bit & 10 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 3, true);

    //draw signal 
    int j = 3;
    for (int i = 0; i < len; i++)
    {
        //check the previous bit, if it is different from current bit then draw a vertical line
        if (i > 0 && binary[i - 1] != binary[i])
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';

        if (i > 0)  //space after each bit to distinguish between bits
            j++;
        
        //if bit is 0, draw line above x-axis else below x-axis
        if (binary[i] == '0')
            graph[1][j++] = graph[1][j++] = '_';
        else
            graph[5][j++] = graph[5][j++] = '_';
    }

    printMatrix(graph, rows, cols);
    cout << "\n  ---->Time\n\n";
}

void NRZ_I_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 10 + 3 * len;      //3 columns for each bit & 10 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 3, true);

    //draw signal 
    int j = 3, currentRow = 1;
    graph[currentRow][j++] = graph[currentRow][j++] = '_';    //for first bit
    for (int i = 1; i < len; i++)
    {
        //if bit is 1, invert the signal else let it remain constant
        if (binary[i] == '1')
        {
            //draw a vertical line
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            //change row number
            currentRow = currentRow == 1 ? 5 : 1;
            graph[currentRow][j++] = graph[currentRow][j++] = '_';
        }
        else
            graph[currentRow][j++] = graph[currentRow][j++] = graph[currentRow][j++] = '_';
    }

    printMatrix(graph, rows, cols);
    cout << "\n  ---->Time\n\n";
}

void RZ_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 20 + 6 * len;      //6 columns for each bit & 20 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 6, false);
    
    //draw signal 
    int j = 2;
    for (int i = 0; i < len; i++)
    {
        //if bit is 0, draw pattern below x-axis else above x-axis
        if (binary[i] == '0')
        {
            graph[5][j] = graph[4][j] = '|';
            j++; 
            graph[5][j++] = graph[5][j++] = '_';
            graph[5][j] = graph[4][j] = '|';
            j++;
            graph[3][j++] = graph[3][j++] = '_';
        }
        else
        {
            graph[2][j] = graph[3][j] = '|';
            j++; 
            graph[1][j++] = graph[1][j++] = '_';
            graph[2][j] = graph[3][j] = '|';
            j++;
            graph[3][j++] = graph[3][j++] = '_';
        }
    }

    j = j + 3;
    graph[3][j++] = graph[3][j++] = graph[3][j++] = graph[3][j++] = '-';
    graph[3][j++] = '>';
    graph[3][j++] = 'T'; graph[3][j++] = 'i'; graph[3][j++] = 'm'; graph[3][j++] = 'e';
    printMatrix(graph, rows, cols);
    cout << endl << endl;
}

void ManchesterEncoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 10 + 6 * len;      //6 columns for each bit & 10 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 6, true);

    //draw signal 
    int j = 3;
    for (int i = 0; i < len; i++)
    {
        //check the previous bit, if it is same as current bit then draw a vertical line
        if (i > 0 && binary[i - 1] == binary[i])
           graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
        
        if (i > 0)  //space after each bit to distinguish between bits
            j++;
        
        if (binary[i] == '0')
        {
            graph[1][j++] = graph[1][j++] = '_';
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            graph[5][j++] = graph[5][j++] = '_';
        }
        else
        {
            graph[5][j++] = graph[5][j++] = '_';
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            graph[1][j++] = graph[1][j++] = '_';
        }
    }

    printMatrix(graph, rows, cols);
    cout << "\n  ---->Time\n\n";
}

void DifferentialManchesterEncoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 10 + 6 * len;      //6 columns for each bit & 10 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 6, true);

    //draw signal 
    int j = 2, firstRow = 5, secondRow = 1, temp;
    //for first bit
    if (binary[0] == '0')
        graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '!';
    j++;
    graph[firstRow][j++] = graph[firstRow][j++] = '_';
    graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
    j++;
    graph[secondRow][j++] = graph[secondRow][j++] = '_';

    for (int i = 1; i < len; i++)
    {
        j++;          //space after each bit to distinguish between bits

        //if bit is 1, invert the signal else let it remain constant
        if (binary[i] == '1')
        {
            //change row numbers
            temp = firstRow;
            firstRow = secondRow;
            secondRow = temp;
            //draw pattern
            graph[firstRow][j++] = graph[firstRow][j++] = '_';
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            graph[secondRow][j++] = graph[secondRow][j++] = '_';
        }
        else
        {
            //in case of no inversion, draw a vertical line
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            //draw pattern
            graph[firstRow][j++] = '_';
            graph[5][j] = graph[4][j] = graph[3][j] = graph[2][j] = '|';
            j++;
            graph[secondRow][j++] = graph[secondRow][j++] = '_';
        }

    }

    printMatrix(graph, rows, cols);
    cout << "\n  ---->Time\n\n";
}

void AMI_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 20 + 3 * len;      //3 columns for each bit & 20 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 3, false);

    //draw signal 
    int j = 3, currentRow = 1;
    for (int i = 0; i < len; i++)
    {
        //if bit is 1, draw the signal above/below x-axis else draw it on x-axis
        if (binary[i] == '1')
        {
            if (i > 0 && binary[i - 1] == '1')  //in case of consecutive 1's, move 1 column back to draw a straight vertical line
                j--;
            //draw vertical line
            if (i > 0)      //skip vertical line for 1st bit
            {
                if (currentRow == 1)
                    graph[3][j] = graph[2][j] = '|';
                else
                    graph[5][j] = graph[4][j] = '|';
                j++;
            }
            graph[currentRow][j++] = graph[currentRow][j++] = '_';
            if (currentRow == 1)
                graph[3][j] = graph[2][j] = '|';
            else
                graph[5][j] = graph[4][j] = '|';
            j++;
            currentRow = 6 - currentRow;    //if current row is 1, change it to 5 for next bit and if it's 5, change it to 1
        }
        else
        {
            if (i > 0 && binary[i - 1] == '0')    //space after each 0 bit to distinguish between bits
                j++;    
            graph[3][j++] = graph[3][j++] = '_';
        }
    }

    j = j + 3;
    graph[3][j++] = graph[3][j++] = graph[3][j++] = graph[3][j++] = '-';
    graph[3][j++] = '>';
    graph[3][j++] = 'T'; graph[3][j++] = 'i'; graph[3][j++] = 'm'; graph[3][j++] = 'e';
    printMatrix(graph, rows, cols);
    cout << endl << endl;
}

void Pseudoternary_Encoding(const string binary)
{
    int len = binary.length();
    int rows = 7, cols = 20 + 3 * len;      //3 columns for each bit & 20 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));
    generalGraph(graph, binary, cols, 3, false);

    //draw signal 
    int j = 3, currentRow = 1;
    for (int i = 0; i < len; i++)
    {
        //if bit is 0, draw the signal above/below x-axis else draw it on x-axis
        if (binary[i] == '0')
        {
            if (i > 0 && binary[i - 1] == '0')  //in case of consecutive 0's, move 1 column back to draw a straight vertical line
                j--;
            //draw vertical line
            if (i > 0)      //skip vertical line for 1st bit
            {
                if (currentRow == 1)
                    graph[3][j] = graph[2][j] = '|';
                else
                    graph[5][j] = graph[4][j] = '|';
                j++;
            }
            graph[currentRow][j++] = graph[currentRow][j++] = '_';
            if (currentRow == 1)
                graph[3][j] = graph[2][j] = '|';
            else
                graph[5][j] = graph[4][j] = '|';
            j++;
            currentRow = 6 - currentRow;    //if current row is 1, change it to 5 for next bit and if it's 5, change it to 1
        }
        else
        {
            if (i > 0 && binary[i - 1] == '1')    //space after each 1 bit to distinguish between bits
                j++;
            graph[3][j++] = graph[3][j++] = '_';
        }
    }

    j = j + 3;
    graph[3][j++] = graph[3][j++] = graph[3][j++] = graph[3][j++] = '-';
    graph[3][j++] = '>';
    graph[3][j++] = 'T'; graph[3][j++] = 'i'; graph[3][j++] = 'm'; graph[3][j++] = 'e';
    printMatrix(graph, rows, cols);
    cout << endl << endl;
}

void TwoBOneQ_Encoding(string binary)
{
    if (binary.length() % 2 != 0)   //add 0 at the end of bit pattern if length is not even
        binary += "0";
    int len = binary.length();
    int rows = 7, cols = 10 + 3 * len;      //3 columns for each bit & 10 extra columns for formatting
    vector<vector<char>> graph(rows, vector<char>(cols, ' '));

    cout << "\nAmplitude\n\n";
    graph[0][0] = '^';
    int j = 4;
    //display bit pattern on top
    for (int i = 0; i < len; i++)
    {
        graph[0][j] = binary[i];
        graph[0][++j] = binary[++i];
        j = j + 3;
    }

    //for 2 vertical lines
    graph[4][0] = graph[1][0] = graph[2][0] = graph[3][0] = graph[5][0] = graph[6][0] =
        graph[4][2] = graph[1][2] = graph[2][2] = graph[3][2] = graph[5][2] = graph[6][2] = '|';

    //to draw x-axis at the middle
    for (int j = 3; j < cols; j++)
        graph[3][j] = '_';

    //draw signal 
    j = 3;
    int previousRow, currentRow;
    for (int i = 0; i < len; i += 2)
    {
        if (binary[i] == '0' && binary[i + 1] == '0')
            currentRow = 5;
        else if (binary[i] == '0' && binary[i + 1] == '1')
            currentRow = 4;
        else if (binary[i] == '1' && binary[i + 1] == '1')
            currentRow = 2;
        else
            currentRow = 1;

        if (i > 1)
        {
            //check the previous 2 bits, if they are different from current bits then draw a vertical line
            if (binary[i - 2] != binary[i] || binary[i - 1] != binary[i + 1])
            {
                if (currentRow > previousRow)
                {
                    for (int k = currentRow; k > previousRow; k--)
                        graph[k][j] = '|';
                }
                else
                    for (int k = previousRow; k > currentRow; k--)
                        graph[k][j] = '|';
            }
            j++;
        }

        graph[currentRow][j++] = graph[currentRow][j++] = graph[currentRow][j++] = '_';
        previousRow = currentRow;
    }

    j = j + 3;
    graph[1][j] = graph[2][j] = graph[4][j] = graph[5][j] = '_';
    j++;
    graph[1][j] = graph[2][j] = graph[4][j] = graph[5][j] = '_';
    j++;
    graph[1][j] = graph[2][j] = graph[4][j] = graph[5][j] = '_';
    j++;
    graph[1][j] = graph[2][j] = graph[4][j] = graph[5][j] = '_';
    j += 2;
    graph[1][j] = '+'; graph[2][j] = '+'; graph[4][j] = '-'; graph[5][j] = '-';
    j++;
    graph[1][j] = '3'; graph[2][j] = '1';  graph[4][j] = '1'; graph[5][j] = '3';
    printMatrix(graph, rows, cols);
    cout << "\n  ---->Time\n\n";
}

string inputBitPattern()
{
    cout << "Enter binary to generate signal : ";
    string binary;
    cin >> binary;
    int len = binary.length();

    for (int i = 0; i < len; i++)
    {
        if (binary[i] != '0' && binary[i] != '1')
        {
            cout << "Invalid bit pattern! Please re-enter binary : ";
            cin >> binary;
            len = binary.length();
            i = 0;
        }
    }
    return binary;
}

void displayMenu()
{
    cout << "1- NRZ\n";
    cout << "2- NRZ-L\n";
    cout << "3- NRZ-I\n";
    cout << "4- RZ\n";
    cout << "5- Manchester\n";
    cout << "6- Differential Manchester\n";
    cout << "7- AMI\n";
    cout << "8- Pseudoternary\n";
    cout << "9- 2B1Q\n";
    cout << "Choose line coding scheme : ";
}

int main()
{
    string binary, choice;
    int option;

    while (true)
    {
        binary = inputBitPattern();
        displayMenu();
        cin >> option;
        while (option < 1 || option > 9)
        {
            cout << "Invalid option. Please choose from 1-9 : ";
            cin >> option;
        }

        if (option == 1)
            NRZ_Encoding(binary);
        else if (option == 2)
            NRZ_L_Encoding(binary);
        else if (option == 3)
            NRZ_I_Encoding(binary);
        else if (option == 4)
            RZ_Encoding(binary);
        else if (option == 5)
            ManchesterEncoding(binary);
        else if (option == 6)
            DifferentialManchesterEncoding(binary);
        else if (option == 7)
            AMI_Encoding(binary);
        else if (option == 8)
            Pseudoternary_Encoding(binary);
        else if (option == 9)
            TwoBOneQ_Encoding(binary);

        cout << "Do you want to try another binary? (Y for yes, N for no) : ";
        cin >> choice;
        while (choice != "Y" && choice != "y" && choice != "N" && choice != "n")
        {
            cout << "Invalid input. Please enter Y or N : ";
            cin >> choice;
        }

        if (choice == "n" || choice == "N")
            break;
    }
}
