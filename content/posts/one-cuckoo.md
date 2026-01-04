+++
date = '2026-01-04T23:34:28+05:30'
draft = true
title = 'One Cuckoo'
+++

```csharp
using System;
using System.Threading.Tasks;

namespace AsyncBreakfast
{

    class Program
    {

        private static Egg FryEggs(int howMany)
        {
            Console.WriteLine("Warming the egg pan...");
            Task.Delay(3000).Wait();
            Console.WriteLine($"cracking {howMany} eggs");
            Console.WriteLine("cooking the eggs ...");
            Task.Delay(3000).Wait();
            Console.WriteLine("Put eggs on plate");

            return new Egg();
        }

     
    }
}
```