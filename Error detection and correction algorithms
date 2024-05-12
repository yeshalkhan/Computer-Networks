using System;
using System.Collections.Generic;
using System.Linq;

namespace main
{
    class Program
    {
        static void Main(string[] args)
        {
            string choice;
            while (true)
            {
                DisplayMenu();
                choice = Console.ReadLine().Trim().ToUpper();

                while (choice != "1" && choice != "2" && choice != "3" && choice != "4" && choice != "5")
                {
                    Console.Write("Invalid option. Please choose from 1-9 : ");
                    choice = Console.ReadLine().Trim().ToUpper();
                }

                Console.WriteLine();
                if (choice == "1")
                    ParityBit();
                else if (choice == "2")
                    _2DParityBits();
                else if (choice == "3")
                    HammingAlgorithm();
                else if (choice == "4")
                    CRC();
                else if (choice == "5")
                    Checksum();

                Console.Write("\nDo you want to try another algorithm? (Y for yes, N for no) : ");
                choice = Console.ReadLine().ToUpper();

                while (choice != "Y" && choice != "N")
                {
                    Console.Write("Invalid input. Please enter Y or N : ");
                    choice = Console.ReadLine().ToUpper();
                }

                if (choice == "N")
                    break;
            }
        }

        static void ParityBit()
        {
            Console.Write("Do you want to even or odd parity? (E for Even, O for Odd) : ");
            string choice = Console.ReadLine().ToUpper();

            while (choice != "E" && choice != "O")
            {
                Console.Write("Invalid input. Please enter E or O : ");
                choice = Console.ReadLine().ToUpper();
            }

            string binary = InputBitPattern("binary");
            int noOfOnes = binary.Count(one => one == '1');
            //number of ones should be even in case of even parity bit
            if (choice == "E" && noOfOnes % 2 == 0)
                Console.WriteLine("\nThe bit pattern is error free");
            //number of ones should be odd in case of odd parity bit
            else if (choice == "O" && noOfOnes % 2 != 0)
                Console.WriteLine("\nThe bit pattern is error free");
            else
                Console.WriteLine("\nThere's an error in the bit pattern");
        }

        static void _2DParityBits()
        {
            Console.Write("Choose sender side or receiver side (S for Sender, R for Receiver) : ");
            string choice = Console.ReadLine().ToUpper();

            while (choice != "S" && choice != "R")
            {
                Console.Write("Invalid input. Please enter S or R : ");
                choice = Console.ReadLine().ToUpper();
            }

            int rows, cols;
            do
            {
                Console.Write("Enter number of rows (> 0) : ");
                int.TryParse(Console.ReadLine(), out rows);
                Console.Write("Enter number of columns (> 0) : ");
                int.TryParse(Console.ReadLine(), out cols);
            } while (rows <= 0 || cols <= 0);

            List<string> binaryMatrix = InputBinaryMatrix(rows, cols);
            if (choice == "S")
                _2DParityBitsSender(binaryMatrix, rows, cols);
            else
                _2DParityBitsReceiver(binaryMatrix, rows, cols);
        }

        static void _2DParityBitsSender(List<string> binaryMatrix, int rows, int cols)
        {
            List<string> outputMatrix = new List<string>();
            string row, column;

            //add parity bits to rows
            int noOfOnes = 0;
            for (int i = 0; i < rows; i++)
            {
                row = binaryMatrix[i];
                noOfOnes = row.Count(one => one == '1');
                row += (noOfOnes % 2 == 0) ? '0' : '1';
                outputMatrix.Add(row);
            }

            row = "";   //for adding last row with parities to output matrix
            //add parity bits to columns
            for (int j = 0; j < cols; j++)
            {
                column = "";
                for (int i = 0; i < rows; i++)
                    column += binaryMatrix[i][j];
                noOfOnes = column.Count(one => one == '1');
                row += (noOfOnes % 2 == 0) ? '0' : '1';
            }
            noOfOnes = row.Count(one => one == '1');    //for last value in the matrix
            row += (noOfOnes % 2 == 0) ? '0' : '1';
            outputMatrix.Add(row);

            Console.WriteLine("\nEntered binary : ");
            PrintMatrix(rows, cols, binaryMatrix);

            Console.WriteLine("Binary to be transmitted : ");
            PrintMatrix(rows + 1, cols + 1, outputMatrix);
        }

        static void _2DParityBitsReceiver(List<string> binaryMatrix, int rows, int cols)
        {
            string row, column;
            int noOfOnes = 0;
            List<bool> RowParities = new List<bool>();
            List<bool> ColumnParities = new List<bool>();

            //detect row wise error
            for (int i = 0; i < rows; i++)
            {
                row = binaryMatrix[i];
                row = row.Remove(row.Length - 1, 1);    //remove the last character (parity bit) to count the number of 1's
                noOfOnes = row.Count(one => one == '1');
                if (noOfOnes % 2 == 0 && binaryMatrix[i][cols - 1] != '0')     //If number of 1's is even, parity bit should be 0
                    RowParities.Add(false);
                else if (noOfOnes % 2 != 0 && binaryMatrix[i][cols - 1] != '1')  //If number of 1's is odd, parity bit should be 1
                    RowParities.Add(false);
                else
                    RowParities.Add(true);
            }

            //detect column wise error
            for (int j = 0; j < cols; j++)
            {
                column = "";
                for (int i = 0; i < rows - 1; i++)
                    column += binaryMatrix[i][j];
                noOfOnes = column.Count(one => one == '1');
                if (noOfOnes % 2 == 0 && binaryMatrix[rows - 1][j] != '0')     //If number of 1's is even, parity bit should be 0
                    ColumnParities.Add(false);
                else if (noOfOnes % 2 != 0 && binaryMatrix[rows - 1][j] != '1')  //If number of 1's is odd, parity bit should be 1
                    ColumnParities.Add(false);
                else
                    ColumnParities.Add(true);
            }

            Console.WriteLine();
            bool isError = false;
            //print out error indexes which are at intersection of corrupted row parity and corrupted column parity 
            for (int i = 0; i < rows; i++)
            {
                for (int j = 0; j < cols; j++)
                {
                    if (RowParities[i] == false && ColumnParities[j] == false)
                    {
                        Console.WriteLine($"There's an error on row {i}, column {j}");
                        isError = true;
                    }
                }
            }
            //for such a case where row parities are corrupted but column parities are not
            if (!ColumnParities.Contains(false))
            {
                for (int i = 0; i < rows; i++)
                {
                    if (RowParities[i] == false)
                    {
                        Console.WriteLine($"There's an error on row {i}");
                        isError = true;
                    }
                }
            }
            //for such a case where row parities are corrupted but column parities are not
            if (!RowParities.Contains(false))
            {
                for (int j = 0; j < cols; j++)
                {
                    if (ColumnParities[j] == false)
                    {
                        Console.WriteLine($"There's an error on column {j}");
                        isError = true;
                    }
                }
            }
            if (!isError)
                Console.WriteLine("The bit pattern is either error free or the algorithm cannot detect the errors");
        }

        static void HammingAlgorithm()
        {
            Console.Write("Choose sender side or receiver side (S for Sender, R for Receiver) : ");
            string choice = Console.ReadLine().ToUpper();

            while (choice != "S" && choice != "R")
            {
                Console.Write("Invalid input. Please enter S or R : ");
                choice = Console.ReadLine().ToUpper();
            }

            string binary = InputBitPattern("binary");
            if (choice == "S")
            {
                AddRedundantBits(ref binary);
                Console.WriteLine("\nBinary to be transmitted : " + binary);
            }
            else
            {
                int index = 0, i = 0;
                string parity, resultant = "";
                binary = binary.Insert(0, "0");     //add a dummy value at start to make indexing easier
                while (true)
                {
                    index = (int)Math.Pow(2, i);
                    if (index > binary.Length)
                        break;
                    parity = GetParityOfRedundantBit(binary, i);
                    if (parity == binary[index].ToString())
                        resultant += '0';
                    else
                        resultant += '1';
                    i++;
                }
                resultant = ReverseStringArray(resultant);
                index = BinaryToDecimal(resultant);
                if (index == 0)
                    Console.WriteLine("\nThe bit pattern is error free");
                else
                    Console.WriteLine($"\nThere's an error on index {index} (Indexes start from 1 here)");
                binary = binary.Remove(0, 1);   //remolve the dummy value
            }
        }

        static void CRC()
        {
            Console.Write("Choose sender side or receiver side (S for Sender, R for Receiver) : ");
            string choice = Console.ReadLine().ToUpper();

            while (choice != "S" && choice != "R")
            {
                Console.Write("Invalid input. Please enter S or R : ");
                choice = Console.ReadLine().ToUpper();
            }

            string binary = InputBitPattern("binary");
            string divisor = InputBitPattern("divisor");
            while (divisor.Length < 2)
            {
                Console.WriteLine("Divisor's length must be > 2");
                divisor = InputBitPattern("divisor");
            }

            if (choice == "S")
            {
                for (int i = 1; i < divisor.Length; i++)    //add redundant bits equal to the order of divisor
                    binary += '0';
                string remainder = BinaryDivision(binary, divisor);
                //remove redundant 0's from the last and add remainder
                binary = binary.Remove(binary.Length - divisor.Length);
                binary += remainder;
                Console.WriteLine($"\nRemainder : {remainder}");
                if (remainder.Length == (divisor.Length - 1))
                    Console.WriteLine($"Binary to be transmitted : {binary}");
                else
                    Console.WriteLine("This divisor isn't suitable for CRC of this binary");
            }
            else
            {
                string remainder = BinaryDivision(binary, divisor);
                if (remainder == "")
                    Console.WriteLine("\nThe bit pattern is error free");
                else
                    Console.WriteLine("\nThere's an error in the bit pattern");
            }
        }

        static void Checksum()
        {
            Console.Write("Choose sender side or receiver side (S for Sender, R for Receiver) : ");
            string choice = Console.ReadLine().ToUpper();

            while (choice != "S" && choice != "R")
            {
                Console.Write("Invalid input. Please enter S or R : ");
                choice = Console.ReadLine().ToUpper();
            }

            List<string> EightBitGroups = InputEightBitGroups();
            List<int> Decimals = new List<int>();
            //convert bit groups to decimal
            for (int i = 0; i < EightBitGroups.Count; i++)
                Decimals.Add(BinaryToDecimal(EightBitGroups[i]));
            int sum = Decimals.Sum();
            string sumInBinary = DecimalToBinary(sum);
            WrapSum(ref sumInBinary);
            OnesComplement(ref sumInBinary);

            if (choice == "S")
            {
                EightBitGroups.Add(sumInBinary);
                Console.Write("\nBinary to be transmitted : ");
                foreach (string s in EightBitGroups)
                    Console.Write(s + " ");
                Console.WriteLine();
            }
            else
            {
                //an error free checksum's complement will contain all zeros
                if (sumInBinary.Contains('1'))
                    Console.WriteLine("\nThere's an error in the bit pattern");
                else
                    Console.WriteLine("\nThe bit pattern is error free");

            }
        }

        //HELPER FUNCTIONS

        static void DisplayMenu()
        {
            Console.WriteLine("1- Parity Bit");
            Console.WriteLine("2- 2D Parity Bits");
            Console.WriteLine("3- Hamming Algorithm");
            Console.WriteLine("4- CRC");
            Console.WriteLine("5- Checksum");
            Console.Write("Choose error detection algorithm : ");
        }

        static string InputBitPattern(string input)
        {
            Console.Write($"Enter {input} : ");
            string binary = Console.ReadLine();
            int len = binary.Length;

            for (int i = 0; i < len; i++)
            {
                if (binary[i] != '0' && binary[i] != '1')
                {
                    Console.Write($"Invalid bit pattern! Please re-enter {input} : ");
                    binary = Console.ReadLine();
                    len = binary.Length;
                    i = 0;
                }
            }
            return binary;
        }

        static List<string> InputBinaryMatrix(int rows, int cols)
        {
            int size = rows * cols;
            string row, binary = InputBitPattern("binary");
            while (binary.Length != size)
            {
                Console.Write($"Binary must be of length {rows} * {cols}! ");
                binary = InputBitPattern("binary");
            }

            List<string> binaryMatrix = new List<string>();
            int nextStartingIndex = 0;
            for (int i = 0; i < rows; i++)
            {
                //Extract each row as a substring
                row = binary.Substring(nextStartingIndex, cols);
                binaryMatrix.Add(row);
                nextStartingIndex += cols;
            }
            return binaryMatrix;
        }

        static void PrintMatrix(int rows, int cols, List<string> matrix)
        {
            for (int i = 0; i < rows; i++)
            {
                for (int j = 0; j < cols; j++)
                    Console.Write(matrix[i][j] + " ");
                Console.WriteLine();
            }
        }

        static string GetParityOfRedundantBit(string binary, int i)
        {
            //starting index is the binary value in which 2nd 1 will appear on the (1+i)th index 
            int startingIndex = (int)Math.Pow(2, i);
            //range defines how many values to take starting from the starting index
            int range = (int)Math.Pow(2, i);
            int j, noOfOnes = 0, count;

            //check the parities at these indexes and set the parity of redundant bits accordingly
            do
            {
                count = 0;
                for (j = startingIndex; count < range && j < binary.Length; j++, count++)
                {
                    if (j == (int)Math.Pow(2, i)) //skip first 1 because that's the index of redundant but itself
                        continue;
                    if (binary[j] == '1')
                        noOfOnes++;
                }
                startingIndex += (int)Math.Pow(2, i + 1);
            }
            while (j < binary.Length);
            return noOfOnes % 2 == 0 ? "0" : "1";

            /*
             1st Parity bit : i=0, Starting value=2^0, Range=2^0 i.e., 1, 3, 5, 7, 9, 11,... here st value=1, range=1, next st value=1+2^1=3
             2nd Parity bit : i=1, Starting value=2^1, Range=2^1 i.e., 2,3, 6,7, 10,11,...  here st value=2, range=2, next st value=2+2^2=6
             3rd Parity bit : i=2, Starting value=2^2, Range=2^2 i.e., 4,5,6,7, 12,13,14,15...  here st value=4, range=4, next st value=4+2^3=12
             ...
             */
        }

        static void AddRedundantBits(ref string binary)
        {
            int n = binary.Length, index;
            string parity;
            int r = 0;
            while ((n + 1 + r) > Math.Pow(2, r))
                r++;

            binary = binary.Insert(0, "0");     //add a dummy value at start to make indexing easier
            for (int i = 0; i < r; i++)
            {
                index = (int)Math.Pow(2, i);          //insert redundant bits at indexes which are at powers of 2
                binary = binary.Insert(index, "2");       //initially set the parity of redundant bits 2
            }

            for (int i = 0; i < r; i++)
            {
                index = (int)Math.Pow(2, i);
                parity = GetParityOfRedundantBit(binary, i);
                binary = binary.Remove(index, 1);   //remove the initial parity and set the actual parity
                binary = binary.Insert(index, parity);
            }

            binary = binary.Remove(0, 1);   //remolve the dummy value
        }

        static int BinaryToDecimal(string binary)
        {
            int digit, result = 0, count = 0;
            for (int i = binary.Length - 1; i >= 0; i--)
            {
                digit = (int)binary[i] - 48;
                result += (digit * (int)Math.Pow(2, count++));
            }
            return result;
        }

        static string ReverseStringArray(string input)
        {
            char[] charArray = input.ToCharArray();
            Array.Reverse(charArray);
            return new string(charArray);
        }

        static string BinaryDivision(string binary, string divisor)
        {
            string dividend, remainder;
            int len = divisor.Length, indexOf1stOne, extraBits = len;
            //extract group of bits equal to the length of divisor
            dividend = binary.Substring(0, extraBits);
            while (true)
            {
                remainder = "";
                binary = binary.Remove(0, extraBits);

                for (int i = 0; i < len; i++)   //perform XOR addition
                    remainder += (dividend[i] == divisor[i]) ? '0' : '1';

                //remove extra 0's from left side of remainder
                indexOf1stOne = remainder.IndexOf('1');
                if (indexOf1stOne >= 0)
                    remainder = remainder.Substring(indexOf1stOne);
                else
                {
                    //if there are no 1's in remainder
                    remainder = "";
                    while (binary.Length != 0 && binary[0] != '1')   //next extra bits from binary must have 1 at front
                        binary = binary.Remove(0, 1);
                }

                //next dividend would be remainder + extra bits from binary
                extraBits = len - remainder.Length;
                if (binary.Length == 0)     //if no more bits are left
                    break;
                if (extraBits > binary.Length)      //if no of bits in binary is less than the bits needed for the dividend
                {
                    remainder = remainder + binary.Substring(0);
                    break;
                }
                dividend = remainder + binary.Substring(0, extraBits);
            }
            return remainder;
        }

        static List<string> InputEightBitGroups()
        {
            string binary = InputBitPattern("binary"), group;
            while (binary.Length % 8 != 0)
            {
                Console.Write("The number of bits must be a multiple of 8!");
                binary = InputBitPattern("binary");
            }

            List<string> EightBitGroups = new List<string>();
            int nextStartingIndex = 0, size = binary.Length / 8;
            for (int i = 0; i < size; i++)
            {
                //Extract each group as a substring
                group = binary.Substring(nextStartingIndex, 8);
                EightBitGroups.Add(group);
                nextStartingIndex += 8;
            }
            return EightBitGroups;
        }

        static string DecimalToBinary(int dec)
        {
            string result = "";
            while (dec >= 1)
            {
                result += (dec % 2).ToString();
                dec /= 2;
            }
            result = ReverseStringArray(result);
            return result;
        }

        static void WrapSum(ref string sum)
        {
            if (sum.Length < 8)
            {
                //pad extra 0's on left to make length 8
                int difference = 8 - sum.Length;
                for (int i = 0; i < difference; i++)
                    sum = sum.Insert(0, "0");
            }
            else if (sum.Length > 8)
            {
                int noOfEightBitGroups = sum.Length / 8;
                List<string> EightBitGroups = new List<string>();
                string rightmostBits;
                for (int i = 0; i < noOfEightBitGroups; i++)
                {
                    //extract eight bit groups and put them into an array
                    rightmostBits = sum.Substring(sum.Length - 8);
                    sum = sum.Remove(sum.Length - 8);
                    EightBitGroups.Add(rightmostBits);
                }

                string result = EightBitGroups[0], addition;
                for (int i = 1; i < noOfEightBitGroups; i++)
                {
                    addition = "";
                    //repetitively perform XOR addition on array's contents to reduce sum's length to 8
                    for (int j = 0; j < 8; j++)
                        addition += (EightBitGroups[i][j] == result[j]) ? '0' : '1';
                    result = addition;
                }

                //for extra bits e.g., if sum's length was 20, there are 20/8=2 groups in array (total 16 bits). the extra 4 bits are left
                if (sum.Length % 8 != 0)
                {
                    addition = "";
                    for (int i = sum.Length - 1, j = result.Length - 1; i >= 0; i--, j--)
                        addition += (sum[i] == result[j]) ? '0' : '1';
                    result = result.Remove(result.Length - sum.Length);
                    addition = ReverseStringArray(addition);
                    result += addition;    //concatenate addition of extra bits at the end
                }
                sum = result;
            }
        }

        static void OnesComplement(ref string binary)
        {
            string result = "";
            for (int i = 0; i < binary.Length; i++)
                result += binary[i] == '1' ? '0' : '1';
            binary = result;
        }

    }
}


