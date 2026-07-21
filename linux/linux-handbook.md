# Linux Handbook

## 1. Linux Filesystem

What is the linux file system?
- Everything is a file
- Hierarchical structure
- Root directory

### Linux Directory Structure

| Directory | Purpose |
|-----------|---------|
| `/` | Root filesystem |
| `/home` | User home directories |
| `/etc` | Configuration files |
| `/var` | Logs and variable data |
| `/usr` | Applications and binaries |
| `/opt` | Optional software |
| `/tmp` | Temporary files |
| `/proc` | Process information |
| `/dev` | Device files |

### Absolute vs Relative Paths

| Absolute Path | Relative Path |
|---------------|---------------|
| Starts with `/` | Does not start with `/` |
| Works from any location | Depends on the current working directory |
| Longer but explicit | Shorter and more convenient |
| Common in scripts and configuration | Common in day-to-day terminal usage |

---

#### Best Practices

- Use **absolute paths** in scripts, automation, and configuration files where consistency is important.
- Use **relative paths** for interactive terminal work and when navigating within a project directory.
- Use `pwd` to confirm your current location before relying on relative paths.

### Common Navigation Commands

---

### `pwd`

#### Purpose

Displays the absolute path of the current working directory.

#### Syntax

```bash
pwd
```

#### Common Options

This command is commonly used without any options.

#### When I Use It

- To confirm my current location before executing commands.
- While navigating deeply nested directories.
- During shell scripting when verifying the working directory.

#### Tips

If you ever get lost while navigating the filesystem, `pwd` should be one of the first commands you run.

---

### `cd`

#### Purpose

Changes the current working directory.

#### Syntax

```bash
cd [directory]
```

#### Common Options

`cd` typically doesn't require options, but it accepts several useful path shortcuts.

#### When I Use It

- Navigating project directories.
- Accessing configuration files.
- Moving between application folders while troubleshooting.

#### Tips

Use `cd -` to quickly switch between two frequently used directories.

---

### `ls`

#### Purpose

Lists the contents of a directory.

#### Syntax

```bash
ls [options] [directory]
```

#### Common Options

| Option | Description |
|---------|-------------|
| `-l` | Long listing format |
| `-a` | Show hidden files |
| `-h` | Human-readable file sizes |
| `-R` | List directories recursively |
| `-t` | Sort by modification time |

#### When I Use It

- Viewing directory contents.
- Checking file permissions.
- Confirming ownership.
- Verifying file sizes.
- Identifying hidden files.

#### Tips

`ls -lah` is one of the most useful combinations and is worth memorizing.

---

### `tree`

#### Purpose

Displays the directory structure as a tree.

#### Syntax

```bash
tree [directory]
```

#### Common Options

| Option | Description |
|---------|-------------|
| `-L <n>` | Limit the depth of the tree |
| `-a` | Include hidden files |
| `-d` | Show directories only |

#### When I Use It

- Understanding project structures.
- Documenting repositories.
- Exploring unfamiliar codebases.

#### Tips

The `tree` command may not be installed by default. Install it using your distribution's package manager if necessary.

---

### Navigation Shortcuts

| Shortcut | Description |
|----------|-------------|
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Home directory |
| `-` | Previous working directory |
| `/` | Root directory |

---

### Best Practices

- Use `pwd` whenever you're unsure of your current location.
- Prefer `ls -lah` when inspecting files and permissions.
- Use `tree` to understand unfamiliar directory structures.
- Learn directory shortcuts (`~`, `.`, `..`, and `-`) to navigate more efficiently.
- Tab completion can save time and reduce typing errors when entering file and directory names.

---

### Key Takeaways

- `pwd` tells you where you are.
- `cd` moves you between directories.
- `ls` lets you inspect the contents of directories.
- `tree` provides a visual representation of the filesystem hierarchy.
- Efficient navigation is a foundational Linux skill and essential for cloud engineering, system administration, and DevOps workflows.
### Finding Files

#### `find`

**Purpose:** Searches for files and directories within a specified path based on various search criteria.

**Syntax**

```bash
find [path] [expression]
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-name` | Search by file or directory name (case-sensitive) |
| `-iname` | Search by file or directory name (case-insensitive) |
| `-type` | Filter by file type (e.g., file or directory) |
| `-size` | Filter by file size |
| `-mtime` | Filter by last modification time |
| `-user` | Filter by file owner |

**Notes**

- Searches the filesystem in real time.
- Highly flexible and suitable for complex searches.
- Can also execute commands on matching files.

---

#### `locate`

**Purpose:** Quickly searches for files using a pre-built database.

**Syntax**

```bash
locate [pattern]
```

**Notes**

- Much faster than `find` because it searches an indexed database.
- Results may be outdated if the database has not been refreshed.
- Database updates are typically handled automatically or manually using `updatedb`.

---

#### `which`

**Purpose:** Displays the location of an executable command in the system's `PATH`.

**Syntax**

```bash
which [command]
```

**Notes**

- Useful for determining which executable will run when a command is invoked.
- Only searches directories listed in the `PATH` environment variable.

---

#### `whereis`

**Purpose:** Locates the binary, source files, and manual pages for a command.

**Syntax**

```bash
whereis [command]
```

**Notes**

- Searches standard system locations.
- Helpful when looking for related files associated with a command.

---

#### `type`

**Purpose:** Identifies how the shell interprets a command.

**Syntax**

```bash
type [command]
```

**Notes**

- Indicates whether a command is an alias, shell builtin, function, or executable.
- Useful for understanding command behavior and troubleshooting shell environments.

---

### Summary

| Command | Best Used For |
|---------|---------------|
| `find` | Real-time file and directory searches |
| `locate` | Fast filename searches using an indexed database |
| `which` | Finding the executable path of a command |
| `whereis` | Locating binaries, source files, and man pages |
| `type` | Determining how the shell resolves a command |


### Manipulating Files and Directories

---

#### `cp`

**Purpose:** Copies files and directories from one location to another.

**Syntax**

```bash
cp [options] source destination
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-r` | Copy directories recursively |
| `-i` | Prompt before overwriting existing files |
| `-u` | Copy only when the source is newer |
| `-v` | Display files as they are copied |

**Notes**

- Preserves the original file by creating a duplicate.
- Use `-r` when copying directories.

---

#### `mv`

**Purpose:** Moves or renames files and directories.

**Syntax**

```bash
mv [options] source destination
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-i` | Prompt before overwriting |
| `-u` | Move only if the source is newer |
| `-v` | Display files as they are moved |

**Notes**

- Can be used to rename files and directories.
- Moving within the same filesystem is generally faster than copying.

---

#### `rm`

**Purpose:** Removes files and directories.

**Syntax**

```bash
rm [options] file
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-r` | Remove directories and their contents recursively |
| `-f` | Force removal without prompting |
| `-i` | Prompt before deleting each file |
| `-v` | Display files as they are removed |

**Notes**

- Deleted files cannot be recovered through `rm`.
- Exercise caution when using `-r` and `-f`, especially together.

---

#### `mkdir`

**Purpose:** Creates new directories.

**Syntax**

```bash
mkdir [options] directory
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-p` | Create parent directories if they do not exist |
| `-v` | Display directories as they are created |

**Notes**

- `-p` is useful for creating nested directory structures.

---

#### `rmdir`

**Purpose:** Removes empty directories.

**Syntax**

```bash
rmdir [directory]
```

**Notes**

- Only works on empty directories.
- Use `rm -r` to remove directories containing files.

---

#### `touch`

**Purpose:** Creates an empty file or updates the timestamp of an existing file.

**Syntax**

```bash
touch [options] file
```

**Common Options**

| Option | Description |
|--------|-------------|
| `-a` | Update only the access time |
| `-m` | Update only the modification time |
| `-c` | Do not create the file if it does not exist |

**Notes**

- Commonly used to create placeholder files.
- Frequently used when testing scripts or applications.

---

### Summary

| Command | Primary Use |
|---------|-------------|
| `cp` | Copy files and directories |
| `mv` | Move or rename files and directories |
| `rm` | Delete files and directories |
| `mkdir` | Create directories |
| `rmdir` | Remove empty directories |
| `touch` | Create empty files or update timestamps |


---

## 2. File Permissions

---

## 3. Users & Groups

---

## 4. Processes

---

## 5. Services

---

## 6. Networking

---

## 7. Log Management

---

## 8. Text Processing

---

## 9. Shell Scripting

---

## References
