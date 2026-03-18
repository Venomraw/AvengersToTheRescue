# Net Track

In this challenge, we'll be using netcat to interact with at server at `net-track.services.cityinthe.cloud:8090`. In order to interact with it you must use this command

```
nc net-track.services.cityinthe.cloud 8090
```

The blank space is normal after connecting. Type `help` to see the list of commands.

## Checking the Version

To check the version type `version` to see it.

## Finding the Flag

Use `list` on the server to see the directory listing.

In order to find the flag, use the `get` commmand on each file on the list

```
get <filename>
```

Go through every file in the list to find the flag

## Finding Largest File Size in Bytes

To find the largest file size, go through each file in the server using the `get` command and than count the letters and spacing in those files.

The easier method is to copy the content in those files and using the command that uses `echo` or `printf` and piping with `wc`

Exit out of the server first before utlizing the command

Command for `schedule` file content:

```
echo -n "Completely free and busy when convenient" | wc -c
```
