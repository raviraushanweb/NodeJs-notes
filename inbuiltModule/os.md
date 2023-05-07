| S.No. | Function Name      | Function Signature         | Description                                                  | Example                                       | Expected Output                  |
|-------|--------------------|-----------------------------|--------------------------------------------------------------|-----------------------------------------------|----------------------------------|
| 1     | arch               | os.arch()                   | Returns the processor architecture.                          | console.log(os.arch());                       | "x64"                            |
| 2     | cpus               | os.cpus()                   | Returns an array of objects with information about each CPU. | console.log(os.cpus());                       | [Array of CPU core objects]      |
| 3     | endianness         | os.endianness()             | Returns the endianness of the CPU.                           | console.log(os.endianness());                 | "LE"                             |
| 4     | freemem            | os.freemem()                | Returns the amount of free system memory in bytes.           | console.log(os.freemem());                    | 1234567890 (example value)       |
| 5     | totalmem           | os.totalmem()               | Returns the total amount of system memory in bytes.          | console.log(os.totalmem());                   | 9876543210 (example value)       |
| 6     | homedir            | os.homedir()                | Returns the current user's home directory.                   | console.log(os.homedir());                    | "/Users/johndoe" (example value) |
| 7     | loadavg            | os.loadavg()                | Returns an array with the 1, 5, and 15-minute load averages. | console.log(os.loadavg());                    | [0.5, 0.6, 0.7] (example values)  |
| 8     | platform           | os.platform()               | Returns the operating system platform.                       | console.log(os.platform());                   | "darwin" (example value)         |
| 9     | release            | os.release()                | Returns the operating system release.                        | console.log(os.release());                    | "20.6.0" (example value)         |
| 10    | type               | os.type()                   | Returns the operating system type.                           | console.log(os.type());                       | "Darwin" (example value)         |
| 11    | uptime             | os.uptime()                 | Returns the system uptime in seconds.                        | console.log(os.uptime());                     | 12345 (example value)            |
| 12    | userInfo           | os.userInfo([options])      | Returns an object with information about the current user.   | console.log(os.userInfo());                   | {username: "johndoe", ...}       |
| 13    | networkInterfaces  | os.networkInterfaces()      | Returns an object containing network interfaces.             | console.log(os.networkInterfaces());           | {en0: [{...}], en1: [{...}], ...}|
| 14    | tmpdir             | os.tmpdir()                 | Returns the default directory for temporary files.           | console.log(os.tmpdir());                     | "/tmp" (example value)           |
| 15    | constants          | os.constants                | Returns an object containing various error codes, etc.       | console.log(os.constants.signals.SIGINT);      | 2                                |
| 16    | getPriority        | os.getPriority([pid])       | Returns the scheduling priority of the process.              | console.log(os.getPriority(process.pid));      | 0 (example value)                |
| 17    | setPriority        | os.setPriority([pid,] priority)  | Sets the scheduling priority of the process with the given PID.| os.setPriority(process.pid, 10);                | (No output, priority is set)     |
| 18    | hostname           | os.hostname()                    | Returns the hostname of the operating system.                  | console.log(os.hostname());                      | "johndoe-pc" (example value)     |

Please note that the function signature for `os.setPriority()` includes an optional `pid` parameter. If `pid` is not provided, the function sets the priority of the current process.


The os module provides several utility functions that can be helpful in various scenarios when working with Node.js applications. Here are 10 use-cases that justify learning and spending time on the os module:

1. Resource Monitoring: Use os module functions like os.freemem(), os.totalmem(), and os.loadavg() to monitor system resources, enabling you to create a custom dashboard or trigger alerts when resources are running low.

2. Platform-Agnostic Code: Utilize os.platform() and os.type() to write platform-agnostic code, ensuring that your Node.js application runs smoothly across different operating systems.

3. Diagnostics and Debugging: Use os.hostname(), os.release(), os.cpus(), and os.networkInterfaces() to retrieve information about the system your application is running on. This information can be useful for diagnostics and debugging purposes.

4. User Management: Leverage os.homedir() and os.userInfo() to manage user-specific data, such as saving user-specific configuration files or logs in the user's home directory.

5. Temporary Files: Use os.tmpdir() to create, store, and manage temporary files, such as cache or intermediate data files, in a platform-independent manner.

6. Process Management: Utilize os.getPriority() and os.setPriority() to manage process priorities, allowing you to optimize system performance by adjusting the priority of resource-intensive tasks or background processes.

7. System Profiling: Collect information about the system's hardware, including CPU architecture (os.arch()), endianness (os.endianness()), and CPU core information (os.cpus()), to create a system profile that can be used for performance optimization, benchmarking, or analytics.

8. Application Analytics: Track system-level metrics like os.uptime() to monitor the overall stability and performance of your application and identify potential bottlenecks or issues.

9. Cross-Platform Deployment: Retrieve system information using os.type(), os.release(), and os.platform() to ensure that your application is compatible with the target environment during deployment.

10. Dynamic Feature Availability: Use the os module functions to determine the availability of certain features on the host system. For example, you can use os.cpus() to check the number of CPU cores and decide whether to enable parallel processing for certain tasks.

By mastering the os module, you can create more robust and versatile Node.js applications that adapt to their environment and perform optimally across different platforms and system configurations.

