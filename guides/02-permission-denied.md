# Permission Denied When Saving a File

*Tested in an Ubuntu virtual machine.*

## Symptom

A "Permission denied" message appears when the customer tries to save a file.

## Cause

The user does not have write permission on the file.

## Steps to fix

1. Open the Terminal. Press **Ctrl + Alt + T**, or click the dots icon at the bottom-left of the dock and search for "terminal".
2. Ask the customer which file failed to save.
3. Go to the file's folder and run `ls -l` to see its permissions and owner.
4. Read the permissions. If the owner's part shows only `r--` and not `rw-`, the file is read-only.
5. If the customer owns the file, run `chmod 644 <file name>`. This gives the owner read and write access, and gives everyone else read-only access.
6. Ask the customer to save the file again.

## Expected result

The file saves without any error.

## If it still doesn't work

Run `ls -l` again and check the owner. If another user owns the file, or the error continues, escalate the ticket and include the `ls -l` output.
