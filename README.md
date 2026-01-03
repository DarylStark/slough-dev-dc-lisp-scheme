# Slough - Dev Container - Lisp (Scheme dialect)

This is a Dev Container for working on Lisp projects using the Scheme dialect. This container is part of the **Slough project**, a project by Daryl Stark to deliver consistent development tooling like dev containers across various programming languages and environments.

## 📋 Table of Contents

- [About the Slough Project](#about-the-slough-project)
- [What's Inside](#whats-inside)
- [Getting Started](#getting-started)
- [Container Configuration](#container-configuration)
- [Using the Installed Tools](#using-the-installed-tools)
- [Dev Container Tips](#dev-container-tips)
- [License](#license)

## 🎯 About the Slough Project

The Slough project is an initiative by Daryl Stark to provide a consistent and reliable set of development containers across multiple programming languages and toolchains. These containers are designed to:

- Provide pre-configured development environments
- Ensure consistency across different machines and platforms
- Reduce setup time for new projects
- Include commonly-used tools and utilities

This particular container focuses on Lisp development using the Scheme dialect, making it ideal for:
- Learning functional programming concepts
- Studying the Structure and Interpretation of Computer Programs (SICP) book
- Working on Scheme-based projects
- Experimenting with Lisp dialects

## 📦 What's Inside

This dev container includes:

- **MIT Scheme**: A complete Scheme implementation ideal for learning and development
- **Base Development Tools**: Includes common development utilities from the Slough generic base container
- **Starship Prompt**: A modern, fast shell prompt with helpful information
- **Pre-configured Environment**: Ready-to-use setup with no additional configuration needed

## 🚀 Getting Started

### Using this Container as a Dev Container

To use this container in your project, create a `.devcontainer/devcontainer.json` file in your project root:

```json
{
  "name": "Lisp Scheme Development",
  "image": "dast1968/slough-dev-dc-lisp-scheme:1.0.0",
  "customizations": {
    "vscode": {
      "extensions": [
        // Add any VS Code extensions you want
      ]
    }
  }
}
```

**Image Tag Format**: `dast1968/slough-dev-dc-lisp-scheme:1.0.0`

- `dast1968`: Docker Hub username
- `slough-dev-dc-lisp-scheme`: Repository name
- `1.0.0`: Version tag for this release

### Opening in VS Code

1. Install the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VS Code
2. Open your project folder in VS Code
3. Press `F1` and select **Dev Containers: Reopen in Container**
4. VS Code will build/pull the container and open your project inside it

## ⚙️ Container Configuration

### User Information

- **Username**: `developer`
- **Sudo Access**: Available **without password** (use `sudo` freely without authentication)
- **Home Directory**: `/home/developer`
- **Shell**: Bash with Starship prompt

### Important Notes

- The container runs as the `developer` user (non-root) by default
- All development tools are accessible without additional configuration
- The prompt name is set to "Lisp-Scheme" for easy identification

## 🛠️ Using the Installed Tools

### MIT Scheme

MIT Scheme is a complete implementation of the Scheme programming language. Here's how to use it:

#### Interactive REPL (Read-Eval-Print Loop)

Start the interactive Scheme interpreter:

```bash
scheme
```

Once inside the REPL:

```scheme
;; Define a simple function
(define (square x) (* x x))

;; Call the function
(square 5)
;; => 25

;; Exit the REPL
(exit)
```

#### Running Scheme Files

Create a Scheme file (e.g., `hello.scm`):

```scheme
(define (greet name)
  (display "Hello, ")
  (display name)
  (display "!")
  (newline))

(greet "World")
```

Run it:

```bash
scheme --quiet < hello.scm
```

Or load it in the REPL:

```bash
scheme --quiet --load hello.scm
```

#### Useful MIT Scheme Commands

- `(load "filename.scm")`: Load a Scheme file
- `(cd "path")`: Change directory
- `(pwd)`: Print working directory
- `(exit)`: Exit the interpreter
- `(trace procedure)`: Trace procedure calls for debugging
- `(untrace procedure)`: Stop tracing

### Example: SICP Exercises

This container is perfect for working through the Structure and Interpretation of Computer Programs:

```scheme
;; SICP Exercise 1.1 - Basic expressions
10
;; => 10

(+ 5 3 4)
;; => 12

(define (abs x)
  (cond ((< x 0) (- x))
        (else x)))

(abs -5)
;; => 5
```

## 💡 Dev Container Tips

### General Tips

- **Persistence**: Files in your project folder are persistent; files outside may not be
- **Extensions**: Install VS Code extensions in the dev container for a tailored experience
- **Terminal**: Use the integrated terminal in VS Code to run commands inside the container
- **Port Forwarding**: VS Code automatically forwards ports from the container to your host

### Microsoft Windows Specific Tips

#### Prerequisites

1. **Install WSL 2**: Dev Containers work best with WSL 2 on Windows
   ```powershell
   wsl --install
   ```

2. **Install Docker Desktop**: Make sure WSL 2 backend is enabled
   - Open Docker Desktop settings
   - Go to "General" and enable "Use the WSL 2 based engine"

#### Performance Considerations

- **Store Projects in WSL 2**: For best performance, clone repositories inside WSL 2 filesystem (e.g., `~/projects/`), not in Windows filesystem (`/mnt/c/`)
  
  ```bash
  # Good - Fast
  cd ~
  git clone https://github.com/your-username/your-project.git
  
  # Avoid - Slow
  cd /mnt/c/Users/YourName/Projects
  git clone https://github.com/your-username/your-project.git
  ```

- **Open from WSL**: Use `code .` from within WSL to open VS Code with better performance

#### Troubleshooting on Windows

- **Docker not starting**: Ensure WSL 2 is properly installed and set as default
  ```powershell
  wsl --set-default-version 2
  ```

- **Slow file operations**: Move your project to WSL 2 filesystem

- **Port conflicts**: Check if ports are already in use on Windows:
  ```powershell
  netstat -ano | findstr :PORT_NUMBER
  ```

#### Git Configuration

Configure Git inside WSL to avoid line ending issues:

```bash
git config --global core.autocrlf input
git config --global core.eol lf
```

### Working with Multiple Containers

If you're using multiple Slough containers:

1. Each project can use a different container
2. Switch between them by reopening in the appropriate container
3. Containers are isolated - changes in one don't affect others

## 📄 License

This project is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for details.

---

**Part of the Slough Project** by [Daryl Stark](https://github.com/DarylStark)
