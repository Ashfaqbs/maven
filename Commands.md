 how Maven handles dependencies like for eg : Apache POI:

1. **`mvn clean package`**:
   - **What it does**: This will create your application's JAR (with dependencies like Apache POI already included if you're using a fat JAR setup).
   - **Dependencies like Apache POI**: Maven will check if these dependencies (like Apache POI) are already available in your local Maven repository (usually located in `~/.m2/repository`).
     - If the **dependencies are already installed** in your local `.m2` folder, it will just use them during the build process.
     - If the dependencies **are not installed**, Maven will **automatically download** them from the central repository (or another configured repository) and store them in your `.m2` folder.
   - **Key point**: After running `mvn clean package`, your application JAR is created, but the external libraries (like Apache POI) are **not installed** anywhere else. They are just used to package the application.

2. **`mvn clean install`**:
   - **What it does**: This will do everything that `package` does (i.e., compile your code, package it, and manage dependencies like Apache POI), but it also **installs your app's JAR** into the local Maven repository (`~/.m2/repository`).
   - **Dependencies like Apache POI**: As with `package`, Maven will download any required dependencies (like Apache POI) **if they are not already in your local `.m2` folder**. Once downloaded, those dependencies are stored in `.m2` and available for future builds.
   - **Key point**: In addition to creating your application's JAR, Maven will also install this JAR in your local repository so that other projects can reference it as a dependency.

### Key Difference:
- **Both `package` and `install`** will download dependencies like Apache POI if they are not already available in your `.m2` folder.
- **`install`** goes a step further and copies **your own project’s JAR** into the local `.m2` folder, allowing other Maven projects to use it as a dependency.

### Example:
- When you run `mvn clean package`:
   - Apache POI (if not already downloaded) will be downloaded and stored in `.m2` for your build.
   - Your Spring Boot app will be packaged into a JAR in the `target/` folder, but nothing will be installed in `.m2` for your project.

- When you run `mvn clean install`:
   - Apache POI (if not already downloaded) will be downloaded and stored in `.m2`.
   - Your Spring Boot app will be packaged and then **installed in `.m2`**, so other projects can reference your app’s JAR as a dependency.

### Important:
- **Dependencies (like Apache POI)**: These are always downloaded (if not present) by either `package` or `install` and placed in your `.m2` folder.
- **Your Project's JAR**: Only the `install` command installs your own project’s JAR into `.m2` for reuse in other projects.
