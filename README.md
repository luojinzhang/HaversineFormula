# HaversineFormula
locate the closest Defibrillators by Haversine Formula
using System;
using System.Linq;
using System.IO;
using System.Text;
using System.Collections;
using System.Collections.Generic;

/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/
class Solution
{
    static void Main(string[] args)
    {
       // string LON = Console.ReadLine();
     //   string LAT = Console.ReadLine();
        
        double LON = Convert.ToDouble(Console.ReadLine().Replace(',','.')) *Math.PI/180;
        double LAT = Convert.ToDouble(Console.ReadLine().Replace(',','.')) *Math.PI/180;
        double distance;
        double shortestDistance = new double();
        string currentDEFIB = string.Empty;
        
        int N = int.Parse(Console.ReadLine());
        for (int i = 0; i < N; i++)
        {
            string DEFIB = Console.ReadLine();
            string cord = DEFIB;
            double defLON;
            double defLAT;
            
            for(int j = 0; j < 4; j++)
            {
               
              cord =  cord.Substring(cord.IndexOf(';')+1);
               if (j == 0)
                {
                    DEFIB = cord;
                }
            }
            
            defLON = Convert.ToDouble(cord.Substring(0,cord.IndexOf(';')).Replace(',','.')) *Math.PI/180;
            defLAT = Convert.ToDouble(cord.Substring(cord.IndexOf(';')+1).Replace(',','.')) *Math.PI/180;
            
            distance = Math.Sqrt(Math.Pow((defLON - LON)* Math.Cos((LAT + defLAT)/2) , 2) + Math.Pow((defLAT - LAT) , 2))*6371;
            
            if (i == 0)
            {
                shortestDistance = distance;
                currentDEFIB = DEFIB;
                continue;
            }
            else if ( shortestDistance > distance)
            {
                currentDEFIB = DEFIB;
                shortestDistance = distance;
            }
            else if (shortestDistance < distance)
            {
                continue;
            }
            
            
        }
        Console.WriteLine(currentDEFIB.Substring(0,currentDEFIB.IndexOf(';')));

        // Write an action using Console.WriteLine()
        // To debug: Console.Error.WriteLine("Debug messages...");

        
    }
}
