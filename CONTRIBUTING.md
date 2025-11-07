
# Contributing to Open Integration Engine

Thank you for your interest in contributing to the **Open Integration Engine** project. Contributions are vital to the continued growth and success of the project, and we welcome all forms of participation, whether you are a developer, a documentation contributor, or a user providing feedback.

The contribution process is straightforward and can be completed in a few simple steps:

## How to Contribute

### 1. Open an Issue
Before making any changes, please open an issue in the [GitHub Issues Tracker](https://github.com/OpenIntegrationEngine/engine/issues). This step helps us discuss the problem or feature before work begins, ensuring alignment and reducing redundant efforts.

### 2. Fork the Repository
Start by forking the [Open Integration Engine GitHub repository](https://github.com/OpenIntegrationEngine/engine) to your own GitHub account.

### 3. Clone Your Fork
Clone your fork locally to your development environment:
```bash
git clone git@github.com:OpenIntegrationEngine/engine.git
```

### 4. Make Changes
Create a new branch for your feature or bug fix:
```bash
git checkout -b feature/your-feature-name
```

### 5. Install Tooling
OIE specifies the working versions of Java and Ant in [.sdkmanrc](./.sdkmanrc). To take advantage of this, install [SDKMAN](https://sdkman.io/) and run `sdk env install`
in the project's root directory.

### 6. How To Build

The project uses **Apache Ant** as the build system. All build orchestration is managed from the `server` directory.

#### 6.1 Build Commands

**Full Build (Development)**
```bash
cd server
ant -f mirth-build.xml -DdisableSigning=true
```

> **Note:** This build takes approximately 2 minutes 20 seconds on a MacBook Pro M4 Pro.

This will:
- Build Donkey (message processing engine)
- Build Server extensions
- Build Client
- Build Manager
- Build CLI (Command Line Interface)
- Run all tests
- Create the complete setup in `server/setup/`

**Fast Build (Skip Tests)**
```bash
cd server
ant -f mirth-build.xml -DdisableSigning=true -DdisableTests=true
```

> **Note:** This build takes approximately 10-11 seconds on a MacBook Pro M4 Pro.

Use this for faster builds during development when you don't need to run the full test suite.

**Full Build (Signed - for releases)**
```bash
cd server
ant -f mirth-build.xml
```

**Create Distribution Package**
```bash
cd server
ant -f mirth-build.xml dist
```

#### Packaging

After building, you can create a distribution tarball:

**On Linux (with GNU tar):**
```bash
tar czf openintegrationengine.tar.gz -C server/ setup --transform 's|^setup|openintegrationengine/|'
```

**On macOS (BSD tar - no --transform support):**
```bash
cd server
tar czf ../openintegrationengine.tar.gz setup
```

Or, to rename the directory in the tarball:
```bash
cd server
cp -r setup openintegrationengine
tar czf ../openintegrationengine.tar.gz openintegrationengine
rm -rf openintegrationengine
```

Alternatively, install GNU tar on macOS:
```bash
brew install gnu-tar
gtar czf openintegrationengine.tar.gz -C server/ setup --transform 's|^setup|openintegrationengine/|'
```

#### Build Individual Components

If needed, you can build specific components separately:

```bash
# Build Donkey only
cd donkey
ant build

# Build Server only  
cd server
ant compile

# Build Client only
cd client
ant -f ant-build.xml build

# Build CLI only
cd command
ant build

# Build Manager only
cd manager
ant -f ant-build.xml build
```

#### Build Output

After a successful build, you'll find:
- **`server/setup/`** - Complete application setup ready to run
- **`server/build/`** - Build artifacts
- **`server/dist/`** - Distribution packages (if you ran the `dist` target)

### 7. Implement your changes

Implement the necessary changes, ensuring they align with the project’s coding standards and practices.

### 8. Test Your Changes
Before submitting your changes, please ensure that all tests pass and that your changes work as expected in your local environment.

### 9. Submit a Pull Request
Once your changes are ready, push them to your fork and create a **draft pull request (PR)** from your branch to the `main` branch of the project. Draft PRs help indicate that the work is in progress.  
Mark the PR as **"Ready for review"** only when it is actually complete and ready for feedback. Include a brief description of the changes and reference the related issue.

## Reporting Bugs

If you encounter a bug, please report it using the **GitHub Issues Tracker**:
1. **Search for existing issues** to check if the problem has already been reported.
2. If the issue is not listed, create a new issue with the following information:
   - A clear and descriptive title.
   - Steps to reproduce the issue.
   - The expected vs. actual behavior.
   - Any relevant logs, error messages, or screenshots to help diagnose the issue.

## Suggesting Features

If you would like to suggest a new feature or enhancement:
1. Open a new issue in the **GitHub Issues Tracker**.
2. Label the issue as a **feature request**.
3. Provide a detailed description of the feature and the problem it aims to solve.
4. If applicable, include examples or use cases to demonstrate the value of the feature.

## Community Guidelines

- Be respectful and professional in all interactions.
- Provide constructive feedback and suggestions.
- Engage in discussions around pull requests and issues with an open and collaborative mindset.

## License

By contributing to **Open Integration Engine**, you agree that your contributions will be licensed under the [Mozilla Public License (MPL) 2.0](./LICENSE).

Thank you for your interest in improving **Open Integration Engine**.
