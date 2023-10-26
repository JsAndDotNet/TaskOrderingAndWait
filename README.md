# Task Ordering And Wait
Simple Task Wait


````
public class Thing
{
	public int Id { get; set; }
	public string Nm { get; set; }

	public async Task<string> DoSomething()
	{
		Random random = new Random();
		var waitTime = random.Next(0, 20);

		await Task.Delay(waitTime);
		string detail = $"{Id} - Done";
		Console.WriteLine(detail);
		return detail;
	}
}



Console.WriteLine("*************************************************************");
Console.WriteLine("Kick Off Tasks - Order Will Be Random");

List<Task<string>> tasks = new List<Task<string>>();

for (int i = 0; i < 10; i++)
{
	var thisCar = new Thing() { Id = i, Nm = $"Thing {i}" };
	tasks.Add(thisCar.DoSomething());
}

var results = await Task.WhenAll(tasks);

Console.WriteLine("*************************************************************");
Console.WriteLine("Get Task Results - Results Will Be Ordered");

foreach (var taskResponse in results)
{
	Console.WriteLine($"Final: {taskResponse}");
}

Console.WriteLine("ALL COMPLETE");

Console.WriteLine("*************************************************************");

return;

````
