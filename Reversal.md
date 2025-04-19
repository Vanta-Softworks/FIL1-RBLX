# Prologue

- This reversal is nothing short of simple, as many of these programs barely have anything to offer.
- Reversal is made by Vanta CEO - Verel, with assistance from Ash, Intosable

**Scout.GG is not anything to harass, or blame.**

I'm just really gonna be documenting my findings, I don't expect anything interesting. 

# Reversal

At first look we are greeted with a very interesting file layout.

![image](https://github.com/user-attachments/assets/fd768cfd-7123-4f3e-b187-2932c6967a09)

I'm very confused with the developer's competence. Does he know that Internal UIs are **Internal**? Why would I have to run a program to view the UI that is supposed to be running in a thread. Not only that but I later figured out that it is literally compiled with .NET

![image](https://github.com/user-attachments/assets/b5e23093-1761-4d5f-8069-e2c9a5cce26b)

After looking through the program more I found the main source. Here we see many defined functions such as Main, Injection, and some other code for backing the UI components.

![image](https://github.com/user-attachments/assets/066028a5-fa5d-48f9-a392-ac18c7a24f4d)

I was confused as to how they would Inject, so that's exactly what I went for. ~~Excuse me as I changed my ILSpy theme after this.~~

The function worked as just checking if Roblox was currently running, if so it would call `Core.Inject();`, which I assume is part of the API.

<pre>
private static void Inject()
	{
		try
		{
			Process[] roblox = Process.GetProcessesByName("RobloxPlayerBeta"); 
			if (roblox.Length == 0) -- If Roblox is running, continue, else return.
			{
				Console.WriteLine("Roblox not running!");
				return;
			}
			Console.WriteLine("Starting UI...");
			Core.Inject(); -- Calls the Inject function from the API.
			Console.WriteLine("Succesfully Started UI");
			Core.ExecuteScript("loadstring(game:HttpGet(\"https://pastebin.com/raw/xqAL9W36\", true))()"); -- Calling execute from the API.
		}
		catch (Exception ex)
		{
			Console.WriteLine("UI Boot-up failed: " + ex.Message);
		}
	}</pre> 

I further jumped to the API and found these functions:

![image](https://github.com/user-attachments/assets/2c83a436-eaec-462f-864c-3d4faadc4efa)

Turns out this isn't internal at all, and the DLL found in the folder is literally for the UI. Very interesting, Internal UI my ass.

Upon opening these functions, I saw that they were all fucked completely. I assumed these were due to ConfuserEx or other painfully easy to deobfuscate obfuscators.

![image](https://github.com/user-attachments/assets/8c4e2061-9774-49fd-bb01-6f1bb344478d)

Anyway, using simple logic, I decrypted the DLL.

After doing so, I managed to obtain the initilization script, aka where some functions are registered. Now you might say that "Cool, an Init Script, whats so wrong about that?". Well, the Init Script is an abomination.

![image](https://github.com/user-attachments/assets/91dd971e-a9df-4aec-b9ce-cf3185767db5)

Don't even ask me what EuroTruckSimulator2 is, I don't know myself.

After further simple investigation I saw this disturbing piece:

![image](https://github.com/user-attachments/assets/0e8275c9-b1c9-41be-b3d7-34501cda8439)

**What the fuck am I looking at?**

It seems that they literally modify the already defined printidentity function to return a fake level, which is beyond corny and I don't recommend doing.

![image](https://github.com/user-attachments/assets/7b380433-24a7-45a1-b80e-612d236b96dd)

How many sources are they going to skid from? Also Nezur stole Xeno's code, so not surprising.

![image](https://github.com/user-attachments/assets/ec68017f-50e5-4885-9811-7a7ff1692009)

# It's not even worth it at this point

> The epilogue is short. Don't use Scout.GG, please!

**One of the worst executors I've ever seen**. If you want to reverse it go right ahead.

> Resources

- Discord: https://discord.gg/PEPKt8Y4
* Init: https://pastebin.com/RfYSdsVQ

**This is made by Vanta Softworks and any claim of our work will be disputed.**
