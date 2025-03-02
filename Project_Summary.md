The following is a review of what I did to review set up JMX Monitoring on Fedora :

1. Project Setup:
    - Created a Java file containing the `SimpleJVMForMonitoring` class and the `SimpleStatsMBean` interface.
    - Set up a directory structure for your project:
    - Created a main project folder: `JMX Monitoring Project`
    - Inside the main folder, created an `output` directory for compiled classes
    - Placed the Java source file (`SimpleJVMForMonitoring.java`) in the main project folder
    - Fixed code issues:
    - Renamed the file to match the public class name (`SimpleJVMForMonitoring.java`).
    - Made the `SimpleStatsMBean` interface public.
    - Possibly made the `SimpleStats` class public as well.

### Folder Structure

JMX Monitoring Project/
├── SimpleJVMForMonitoring.java
└── output/
└── (compiled .class files will go here)

2. Java and JMC Installation:
   - Installed Java 11 OpenJDK: `sudo dnf install java-11-openjdk`
   - Since JMC is a Redhat native package, and the Fedora option was sunsetted. COPR was needed to install.
     Luckily Almac has helped make it available! - https://copr.fedorainfracloud.org/coprs/almac/
   - Used COPR (Cool Other Package Repo) to install JMC from Almac's repo:
     ```
     sudo dnf copr enable almac/jmc8
     sudo dnf install jmc
     ```

3. Compiling the Java Application:
   ```
   javac -d '/run/media/mims/QVO/New Docs/Learning/Linux/JMX Monitoring Project/output' SimpleJVMForMonitoring.java
   ```

4. Running the JVM with JMX enabled:
   ```
   java -Dcom.sun.management.jmxremote.port=9010 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false SimpleJVMForMonitoring
   ```

5. Attempting to run JMC:
   You tried various commands to run JMC and point it to your JVM, including:
   ```
   jmc filename='run/media/mims/QVO/New Docs/Learning/Linux/JMX Monitoring Project/output'
   ```

6. Additional Setup:
   - Installed htop for system monitoring: `sudo dnf install htop`
   - Edited your .bashrc file, possibly to set up aliases or environment variables for easier access to your project directory.

7. Connecting JMC to JVM:
   To correctly connect JMC to your running JVM, you should launch JMC and then use its interface to connect to the JVM running on localhost:9010, as that's the port you specified when launching your Java application with JMX enabled.

