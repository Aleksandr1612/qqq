using System;

class Program
{
    static void Main(string[] args)
    {
        Random random = new Random();

        int[,] array1 = GenerateRandomArray("Первый случайный массив:", random);
        int[,] array2 = GenerateRandomArray("Второй случайный массив:", random);

        CheckArrays(array1);
        CheckArrays(array2);
    }

    static int[,] GenerateRandomArray(string prompt, Random random)
    {
        Console.WriteLine(prompt);
        int rows = random.Next(1, 11); 
        int cols = random.Next(1, 11); 
        int[,] array = new int[rows, cols];

        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < cols; j++)
            {
                array[i, j] = random.Next(0, 100); 
            }
        }

        Console.WriteLine($"Сгенерированный массив {rows}x{cols}:");
        PrintArray(array);
        return array;
    }

    static void PrintArray(int[,] array)
    {
        int rowCount = array.GetLength(0);
        int colCount = array.GetLength(1);
        for (int i = 0; i < rowCount; i++)
        {
            for (int j = 0; j < colCount; j++)
            {
                Console.Write(array[i, j] + "\t");
            }
            Console.WriteLine();
        }
    }

    static void CheckArrays(int[,] array)
    {
        int rowCount = array.GetLength(0);
        int colCount = array.GetLength(1);
        int alternatingRowsCount = 0;
        int evenRowsWithOddSecondElementCount = 0;

        for (int i = 0; i < rowCount; i++)
        {
            if (CheckRow(array, i, colCount))
            {
                alternatingRowsCount++;
            }

            if (CheckEvenRowWithOddSecondElement(array, i))
            {
                evenRowsWithOddSecondElementCount++;
            }
        }

        if (alternatingRowsCount > 0)
        {
            Console.WriteLine($"Количество строк с чередующимися четными и нечетными элементами: {alternatingRowsCount}");
        }
        else
        {
            Console.WriteLine("Нет строк с чередующимися четными и нечетными элементами.");
        }

        if (evenRowsWithOddSecondElementCount > 0)
        {
            Console.WriteLine($"Количество четных строк, где второй элемент нечетный: {evenRowsWithOddSecondElementCount}");
        }
        else
        {
            Console.WriteLine("Нет четных строк, где второй элемент нечетный.");
        }
    }

    static bool CheckRow(int[,] array, int rowIndex, int colCount)
    {
        for (int j = 1; j < colCount; j++)
        {
            if ((array[rowIndex, j] % 2) == (array[rowIndex, j - 1] % 2))
            {
                return false; 
            }
        }
        return true; 
    }

    static bool CheckEvenRowWithOddSecondElement(int[,] array, int rowIndex)
    {
        if (rowIndex % 2 == 0) 
        {
            return (array[rowIndex, 1] % 2 != 0); 
        }
        return false; 
    }
}
