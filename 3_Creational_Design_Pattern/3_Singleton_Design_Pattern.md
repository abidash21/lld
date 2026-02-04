SINGLETON DESIGN PATTERN
- Creates only one instance of a class throughout the entire applicaiton irrespective the number of threads or classes use the class, they refer to the same object

 If we use new instance everytime then, 
- Mutliple instances would consume unnecessary resources - Increased memory usage
- Inconsistent logging - If different parts of the system use different loggers, logs could be written in different places or out of order

```java
class Logger {

    public Log() {
        System.out.println("Logging in ");
    }
}

public class Main {
    public static void main(String[] args) {

        Logger l1 = new Logger();
        Logger l2 = new Logger();
    }
}

disadvantages:
- If logging to a file, each logger might try to access and write at the same time , leading to potential conflicts and overhead
- Inconsistent output in the same logfile, log messages scattered across different log files
- If the logger maintains state related data, each logger instance could have different settings, No single source of truth.



public class Logger {
    private static Logger logger = null;
    private Logger() {}

    public static Logger getLogger(){
        if(logger == null){
            logger = new Logger()
        }
        return logger;
    } // This is not thread safe


    public void log(){
        System.out.println("Log: " + message);
    }
}

public class Application {
    public void run {
        Logger logger = Logger.getLogger();
        logger.log("Application started");
    }
}


- This is fine for single thread application, but for multithreading there may be problems:
1. Thread A checks if the Logger instance is null
2. Thread B does the same thing at the exact same time, unaware that Thread A is also checking 
3. Both thread creates a new logger instance, suddenly we have two instances instead of one


disadvantages:
- Mutliple instances created, two or more logger leading to inefficiency, debugging becomes difficult
- Race conditions, Threads compete to create the Singleton instance, leading to unpredictable behaviour. Some logs might get lost

solution:
- Use synchronized block, this ensures that only one thread can create the logger instance at a time.
- The synchronized keyword is used to control access to critical section of code, ensuring that only one thread executes 
the block at any given time.

 public static synchronized Logger getLogger(){
        if(logger == null){
            logger = new Logger()
        }
        return logger;
    }

problem:
- WIth the current implementation we are making every thread wait. But in reality we should stop other threads only when an instance is getting created. If an instance is already created then all other threds should access the logger

- When all threds wait for longer it increase overhead.

solution:
- The Double Checked Locking Technique:
Instead of synchronizing every call, we only synchronize when the instance is null and needs to be created.
- This minimizes synchronization overhead, making the singleton faster and more efficient
- First check outside synchronized block, the instance already exists, we return it without synchronization
- Second check inside synchronized block, if the instance is still nulll, we then synchronize and create the instance.


 public static Logger getInstance() {
    if (instance == null) { // First check (no synchronization needed here)
      synchronized (Logger.class) { // Synchronize only when creating the instance
        if (instance == null) { // Second check (inside synchronized block)
          instance = new Logger(); // Create the instance if it's still null
        }
      }
    }
    return instance; // Return the single instance
  }

‍




