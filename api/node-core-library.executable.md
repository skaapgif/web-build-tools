[Home](./index) &gt; [@microsoft/node-core-library](./node-core-library.md) &gt; [Executable](./node-core-library.executable.md)

## Executable class

The Executable class provides a safe, portable, recommended solution for tools that need to launch child processes.

<b>Signature:</b>

```typescript
export declare class Executable 
```

## Methods

|  Method | Modifiers | Description |
|  --- | --- | --- |
|  [spawnSync(filename, args, options)](./node-core-library.executable.spawnsync.md) | `static` | Synchronously create a child process and optionally capture its output. |
|  [tryResolve(filename, options)](./node-core-library.executable.tryresolve.md) | `static` | Given a filename, this determines the absolute path of the executable file that would be executed by a shell:<!-- -->- If the filename is missing a path, then the shell's default PATH will be searched. - If the filename is missing a file extension, then Windows default file extensions will be searched. |

## Remarks

The NodeJS child\_process API provides a solution for launching child processes, however its design encourages reliance on the operating system shell for certain features. Invoking the OS shell is not safe, not portable, and generally not recommended:

- Different shells have different behavior and command-line syntax, and which shell you will get with NodeJS is unpredictable. There is no universal shell guaranteed to be available on all platforms.

- If a command parameter contains symbol characters, a shell may interpret them, which can introduce a security vulnerability

- Each shell has different rules for escaping these symbols. On Windows, the default shell is incapable of escaping certain character sequences.

The Executable API provides a pure JavaScript implementation of primitive shell-like functionality for searching the default PATH, appending default file extensions on Windows, and executing a file that may contain a POSIX shebang. This primitive functionality is sufficient (and recommended) for most tooling scenarios.

If you need additional shell features such as wildcard globbing, environment variable expansion, piping, or built-in commands, then we recommend to use the `@microsoft/rushell` library instead. Rushell is a pure JavaScript shell with a standard syntax that is guaranteed to work consistently across all platforms.
