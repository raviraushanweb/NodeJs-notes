Here's a summary of the `fs` module methods we have covered so far:

- **readFile and readFileSync**: Read the entire contents of a file.
  - readFile: Asynchronous, takes a callback.
  - readFileSync: Synchronous, returns the file contents.
- **writeFile and writeFileSync**: Write data to a file, replacing its contents if the file exists.
  - writeFile: Asynchronous, takes a callback.
  - writeFileSync: Synchronous.
- **appendFile and appendFileSync**: Append data to a file, creating the file if it does not exist.
  - appendFile: Asynchronous, takes a callback.
  - appendFileSync: Synchronous.
- **unlink and unlinkSync**: Delete a file.
  - unlink: Asynchronous, takes a callback.
  - unlinkSync: Synchronous.
- **open and openSync**: Open a file and return a file descriptor for further operations.
  - open: Asynchronous, takes a callback.
  - openSync: Synchronous, returns a file descriptor.
- **read and readSync**: Read data from a file using a file descriptor, allowing for operations like random access and reading files in chunks.
  - read: Asynchronous, takes a callback.
  - readSync: Synchronous, returns the number of bytes read.
- **readdir and readdirSync**: Read the contents of a directory.
  - readdir: Asynchronous, takes a callback.
  - readdirSync: Synchronous, returns an array of filenames or fs.Dirent objects.
- **mkdir and mkdirSync**: Create a new directory.
  - mkdir: Asynchronous, takes a callback.
  - mkdirSync: Synchronous.
- **rmdir and rmdirSync**: Remove a directory.
  - rmdir: Asynchronous, takes a callback.
  - rmdirSync: Synchronous.

These methods enable you to perform various file and directory operations, such as reading and writing files, appending data, deleting files, opening files for random access or reading in chunks, listing directory contents, creating and removing directories.

Next, we can explore some additional methods in the `fs` module that are useful for working with files and directories:

1. **fs.stat and fs.statSync**: Get information about a file or directory, such as its size, type (file, directory, symbolic link, etc.), and timestamps (created, modified, accessed).
2. **fs.fstat and fs.fstatSync**: Similar to fs.stat, but works with a file descriptor instead of a path.
3. **fs.access and fs.accessSync**: Check if a file or directory exists and if the current process has the required permissions (read, write, or execute) for it.
4. **fs.rename and fs.renameSync**: Rename a file or directory.
5. **fs.copyFile and fs.copyFileSync**: Copy a file from one location to another.
6. **fs.watch**: Watch for changes in a file or directory and get notified when it's modified, created, or deleted.
7. **fs.symlink and fs.symlinkSync**: Create a symbolic link (also known as a soft link) to a file or directory.
8. **fs.readlink and fs.readlinkSync**: Read the target of a symbolic link.
9. **fs.realpath and fs.realpathSync**: Resolve the actual path of a file or directory, taking into account any symbolic links.
10. **fs.createReadStream and fs.createWriteStream**: Create readable or writable streams for working with files, enabling more efficient and flexible reading and writing operations, especially for large files or streaming data.










| S.No | Function       | Signature                                              | Description                                                                                             |
|------|----------------|--------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| 1    | readFile       | fs.readFile(path[, options], callback)                 | Asynchronously reads the entire contents of a file.                                                     |
| 2    | readFileSync   | fs.readFileSync(path[, options])                       | Synchronously reads the entire contents of a file.                                                      |
| 3    | writeFile      | fs.writeFile(file, data[, options], callback)          | Asynchronously writes data to a file, replacing the file if it already exists.                          |
| 4    | writeFileSync  | fs.writeFileSync(file, data[, options])                | Synchronously writes data to a file, replacing the file if it already exists.                           |
| 5    | appendFile     | fs.appendFile(file, data[, options], callback)         | Asynchronously appends data to a file, creating the file if it does not yet exist.                      |
| 6    | appendFileSync | fs.appendFileSync(file, data[, options])               | Synchronously appends data to a file, creating the file if it does not yet exist.                       |
| 7    | unlink         | fs.unlink(path, callback)                              | Asynchronously removes a file or symbolic link.                                                         |
| 8    | unlinkSync     | fs.unlinkSync(path)                                    | Synchronously removes a file or symbolic link.                                                          |
| 9    | open           | fs.open(path[, flags[, mode]], callback)               | Asynchronously opens a file and returns a file descriptor.                                              |
| 10   | openSync       | fs.openSync(path[, flags[, mode]])                     | Synchronously opens a file and returns a file descriptor.                                               |
| 11   | close          | fs.close(fd, callback)                                 | Asynchronously closes a file descriptor.                                                                |
| 12   | closeSync      | fs.closeSync(fd)                                       | Synchronously closes a file descriptor.                                                                 |
| 13   | readDir        | fs.readdir(path[, options], callback)                 | Asynchronously reads the contents of a directory.                                                       |
| 14   | readDirSync    | fs.readdirSync(path[, options])                        | Synchronously reads the contents of a directory.                                                        |
| 15   | mkdir          | fs.mkdir(path[, options], callback)                    | Asynchronously creates a new directory.                                                                 |
| 16   | mkdirSync      | fs.mkdirSync(path[, options])                          | Synchronously creates a new directory.                                                                  |
| 17   | rmdir          | fs.rmdir(path[, options], callback)                    | Asynchronously removes an empty directory.                                                              |
| 18   | rmdirSync      | fs.rmdirSync(path[, options])                          | Synchronously removes an empty directory.                                                               |
| 19   | read           | fs.read(fd, buffer, offset, length, position, callback)| Asynchronously reads data from a file.                                                                  |
| 20   | stat           | fs.stat(path[, options], callback)                     | Asynchronously retrieves file or directory information.                                                 |
| 21   | statSync       | fs.statSync(path[, options])                           | Synchronously retrieves file or directory information.                                                  |
| 22   | fstat          | fs.fstat(fd[, options], callback)                      | Asynchronously retrieves information for an open file.                                                  |
| 23   | fstatSync      | fs.fstatSync(fd[, options])                            | Synchronously retrieves information for an open file.                                                   |
| 24   | access         | fs.access(path[, mode], callback)                      | Asynchronously tests a user's permissions for a file or directory.                                      |
| 25   | accessSync     | fs.accessSync(path[, mode])                            | Synchronously tests a user's permissions for a file or directory.                                       |
| 26   | rename         | fs.rename(oldPath, newPath, callback)                  | Asynchronously renames a file or directory.                                                             |
| 27   | renameSync     | fs.renameSync(oldPath, newPath)                        | Synchronously renames a file or directory.                                                              |
| 28   | copyFile       | fs.copyFile(src, dest[, flags], callback)              | Asynchronously copies a file.                                                                           |
| 29   | copyFileSync   | fs.copyFileSync(src, dest[, flags])                    | Synchronously copies a file.                                                                            |
| 30   | watch          | fs.watch(filename[, options][, listener])              | Watches for changes on a file or directory.                                                             |
| 31   | symlink        | fs.symlink(target, path[, type], callback)             | Asynchronously creates a new symbolic link.                                                             |
| 32   | symlinkSync    | fs.symlinkSync(target, path[, type])                   | Synchronously creates a new symbolic link.                                                              |
| 33   | readlink       | fs.readlink(path[, options], callback)                 | Asynchronously reads the value of a symbolic link.                                                      |
| 34   | readlinkSync   | fs.readlinkSync(path[, options])                       | Synchronously reads the value of a symbolic link.                                                       |
| 35   | realpath       | fs.realpath(path[, options], callback)                 | Asynchronously resolves a pathname to its absolute path.                                                |
| 36   | realpathSync   | fs.realpathSync(path[, options])                       | Synchronously resolves a pathname to its absolute path.                                                 |
| 37   | ftruncate      | fs.ftruncate(fd, len, callback)                        | Asynchronously truncates a file to a specified length.                                                  |
| 38   | ftruncateSync  | fs.ftruncateSync(fd, len)                              | Synchronously truncates a file to a specified length.                                                   |
| 39   | truncate       | fs.truncate(path, len, callback)                       | Asynchronously truncates a file to a specified length without opening it.                               |
| 40   | truncateSync   | fs.truncateSync(path, len)                             | Synchronously truncates a file to a specified length without opening it.                                |
| 41   | chmod          | fs.chmod(path, mode, callback)                         | Asynchronously changes the permissions of a file.                                                       |
| 42   | chmodSync      | fs.chmodSync(path, mode)                               | Synchronously changes the permissions of a file.                                                        |
| 43   | chown          | fs.chown(path, uid, gid, callback)                     | Asynchronously changes the owner and group of a file.                                                   |
| 44   | chownSync      | fs.chownSync(path, uid, gid)                           | Synchronously changes the owner and group of a file.                                                    |
| 45   | utimes         | fs.utimes(path, atime, mtime, callback)                | Asynchronously changes the file timestamps of a file. 
| 46   | utimesSync     | fs.utimesSync(path, atime, mtime)                      | Synchronously changes the file timestamps of a file.                                                    |
| 47   | fsync          | fs.fsync(fd, callback)                                 | Asynchronously synchronizes a file's in-core state with the underlying storage device.                  |
| 48   | fsyncSync      | fs.fsyncSync(fd)                                       | Synchronously synchronizes a file's in-core state with the underlying storage device.                   |
| 49   | fdatasync      | fs.fdatasync(fd, callback)                             | Asynchronously synchronizes a file's data with the underlying storage device.                           |
| 50   | fdatasyncSync  | fs.fdatasyncSync(fd)                                   | Synchronously synchronizes a file's data with the underlying storage device.                            |
| 51   | readv          | fs.readv(fd, buffers, position, callback)              | Asynchronously reads data from a file into an array of Buffer objects.                                  |
| 52   | writev         | fs.writev(fd, buffers[, position], callback)           | Asynchronously writes an array of Buffer objects to a file.                                             |
| 53   | watchFile      | fs.watchFile(filename[, options], listener)            | Starts watching for changes on a file, invoking the listener when the file has changed.                 |
| 54   | unwatchFile    | fs.unwatchFile(filename[, listener])                   | Stops watching for changes on a file that was being watched by `fs.watchFile`.                          |

