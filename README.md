# maven-python-project

# Clone this Project
```
git clone https://github.com/atulkamble/maven-python-project.git
cd maven-python-project
```
# Prerequisite
```
sudo yum install python -y
sudo yum install maven -y
sudo yum install java -y
sudo yum install tree -y
```
Maven is primarily used for Java projects, but you can use it to manage and build projects in other languages, including Python, using plugins such as the `exec-maven-plugin`. Here's a basic guide on how to set up a Maven project to run Python code.

### 1. **Install Maven**

Ensure you have Maven installed on your system. You can check this by running:

```sh
mvn -version
```

If Maven is not installed, you can download and install it from the [official Maven website](https://maven.apache.org/install.html).

### 2. **Create a Maven Project**

Open your terminal and create a new Maven project using the following command:

```sh
mvn archetype:generate -DgroupId=com.example -DartifactId=my-python-project -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This will generate a basic Maven project structure.

### 3. **Project Structure**

Your project directory should look something like this:

```
my-python-project
│
├── pom.xml
├── src
│   ├── main
│   └── test
└── python
    └── script.py
```

### 4. **Add Python Script**

Create a directory named `python` in your project root and add your Python script, e.g., `script.py`:

```python
# script.py
print("Hello, Maven with Python!")
```

### 5. **Modify `pom.xml`**

Open the `pom.xml` file in the root directory and configure the `exec-maven-plugin` to run the Python script:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-python-project</artifactId>
    <version>1.0-SNAPSHOT</version>
    <build>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.0.0</version>
                <executions>
                    <execution>
                        <phase>compile</phase>
                        <goals>
                            <goal>exec</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <executable>python</executable>
                    <arguments>
                        <argument>${project.basedir}/python/script.py</argument>
                    </arguments>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### 6. **Run the Maven Project**

Execute the Maven build process to run your Python script:

```sh
mvn compile
```

You should see the output of your Python script in the terminal:

```sh
[INFO] --- exec-maven-plugin:3.0.0:exec (default) @ my-python-project ---
Hello, Maven with Python!
```

### Explanation:

1. **Project Setup**: The Maven project is created using a standard archetype.
2. **Directory Structure**: A `python` directory is added to store the Python script.
3. **POM Configuration**: The `exec-maven-plugin` is configured in the `pom.xml` file to execute the Python script during the compile phase.
4. **Execution**: Running `mvn compile` triggers the Maven lifecycle, which in turn executes the Python script.

This setup allows you to integrate Python scripts into your Maven build process, enabling you to manage multi-language projects effectively.
