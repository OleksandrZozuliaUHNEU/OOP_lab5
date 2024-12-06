using System;

public class StandardCalculator
{
    public double Operand1 { get; set; }
    public double Operand2 { get; set; }

    public StandardCalculator() { }

    public double Add() => Operand1 + Operand2;
    public double Subtract() => Operand1 - Operand2;
    public double Multiply() => Operand1 * Operand2;
    public double Divide()
    {
        if (Operand2 == 0)
            throw new DivideByZeroException("Division by zero is not allowed.");
        return Operand1 / Operand2;
    }
}

public class EngineeringCalculator : StandardCalculator
{
    public double Sin(double angleInDegrees)
    {
        if (angleInDegrees < 0 || angleInDegrees > 360)
            throw new ArgumentOutOfRangeException("Angle must be between 0 and 360 degrees.");
        double radians = angleInDegrees * Math.PI / 180;
        return Math.Sin(radians);
    }
}

class Program
{
    static void Main()
    {
        Console.WriteLine("Choose mode: 1 - Standard, 2 - Engineering");
        int mode = int.Parse(Console.ReadLine());

        if (mode == 1)
        {
            StandardCalculator calc = new StandardCalculator();
            Console.WriteLine("Enter two numbers:");
            calc.Operand1 = double.Parse(Console.ReadLine());
            calc.Operand2 = double.Parse(Console.ReadLine());

            Console.WriteLine("Choose operation: +, -, *, /");
            string op = Console.ReadLine();

            try
            {
                double result = op switch
                {
                    "+" => calc.Add(),
                    "-" => calc.Subtract(),
                    "*" => calc.Multiply(),
                    "/" => calc.Divide(),
                    _ => throw new InvalidOperationException("Invalid operation.")
                };
                Console.WriteLine($"Result: {result}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
        else if (mode == 2)
        {
            EngineeringCalculator engCalc = new EngineeringCalculator();
            Console.WriteLine("Enter an angle in degrees (0 to 360):");
            double angle = double.Parse(Console.ReadLine());

            try
            {
                double sinValue = engCalc.Sin(angle);
                Console.WriteLine($"Sin({angle}) = {sinValue}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
        else
        {
            Console.WriteLine("Invalid mode selected.");
        }
    }
}

