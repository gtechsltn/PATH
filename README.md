# PATH

```
using System;
using System.Text;

public class EnvironmentVariableReader
{
    public static void ShowEnvironmentVariable()
    {
        // Get the value of the DOTNETBACKEND_PORT environment variable
        string? dotnetBackendPort = Environment.GetEnvironmentVariable("DOTNETBACKEND_PORT");
        Console.WriteLine($"DOTNETBACKEND_PORT: {dotnetBackendPort ?? "Not set"}");

        // Get the value of the JAVA_HOME environment variable
        string? javaHome = Environment.GetEnvironmentVariable("JAVA_HOME");
        Console.WriteLine($"JAVA_HOME: {javaHome ?? "Not set"}");

        // Get the value of the SPARK_HOME environment variable
        string? sparkHome = Environment.GetEnvironmentVariable("SPARK_HOME");
        Console.WriteLine($"SPARK_HOME: {sparkHome ?? "Not set"}");

        // Get the value of the NODE_JS environment variable
        // Note: The standard variable is typically just 'PATH' or other specific
        // variables, not NODE_JS. This is an example.
        string? nodeJs = Environment.GetEnvironmentVariable("NODE_JS");
        Console.WriteLine($"NODE_JS: {nodeJs ?? "Not set"}");

        // Get the value of the NVM environment variable
        // Note: The standard variable is typically NVM_HOME or similar.
        string? nvm = Environment.GetEnvironmentVariable("NVM");
        Console.WriteLine($"NVM: {nvm ?? "Not set"}");
    }

    /// <summary>
    /// Save a new path to the PATH environment variable in C#
    /// </summary>
    /// <param name="newPath">The new directory you want to add to the PATH</param>
    public static void AddNewPath(string newPath)
    {
        // Check if the directory exists before attempting to add it
        if (!Directory.Exists(newPath))
        {
            Console.WriteLine($"Error: The directory '{newPath}' does not exist.");
            return;
        }

        // Get the current PATH value
        string? currentPath = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.Machine);

        // Check if the new path is already in the existing PATH to avoid duplicates
        if (currentPath == null || !currentPath.Contains(newPath))
        {
            // The separator for PATH is ';' on Windows and ':' on Linux/macOS
            char separator = Path.PathSeparator;

            // Construct the new PATH value
            string updatedPath = $"{currentPath}{separator}{newPath}";

            // Set the new PATH for the machine
            Environment.SetEnvironmentVariable("PATH", updatedPath, EnvironmentVariableTarget.Machine);

            Console.WriteLine($"Successfully added '{newPath}' to the system PATH.");
        }
        else
        {
            Console.WriteLine($"'{newPath}' is already in the system PATH.");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.OutputEncoding = Encoding.UTF8;

        Console.WriteLine("---------- Environment.GetEnvironmentVariable(\"PATH\") ----------");
        string[]? pathValues = Environment.GetEnvironmentVariable("PATH")?.Split([Path.PathSeparator], StringSplitOptions.RemoveEmptyEntries) ?? [];

        foreach (string pathValue in pathValues)
        {
            Console.WriteLine($"PATH: {pathValue ?? "Not set"}");
        }

        Console.WriteLine("---------- Environment.GetEnvironmentVariable(\"PATH\", \"Process\") ----------");
        string[]? pathProcessValues = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.Process)?.Split([Path.PathSeparator], StringSplitOptions.RemoveEmptyEntries) ?? [];

        foreach (string pathValue in pathProcessValues)
        {
            Console.WriteLine($"PATH: {pathValue ?? "Not set"}");
        }

        Console.WriteLine("---------- Environment.GetEnvironmentVariable(\"PATH\", \"Machine\") ----------");
        string[]? pathMachineValues = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.Machine)?.Split([Path.PathSeparator], StringSplitOptions.RemoveEmptyEntries) ?? [];

        foreach (string pathValue in pathMachineValues)
        {
            Console.WriteLine($"PATH: {pathValue ?? "Not set"}");
        }

        Console.WriteLine("---------- Environment.GetEnvironmentVariable(\"PATH\", \"User\") ----------");
        string[]? pathUserValues = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.User)?.Split([Path.PathSeparator], StringSplitOptions.RemoveEmptyEntries) ?? [];

        foreach (string pathValue in pathUserValues)
        {
            Console.WriteLine($"PATH: {pathValue ?? "Not set"}");
        }

        Console.WriteLine("---------- ShowEnvironmentVariable ----------");
        EnvironmentVariableReader.ShowEnvironmentVariable();
    }
}
```
