# SSH in Windows

Windows doesn't have SSH built in like Linux or OSX. In order to SSH to an EC2 instance under Windows there are a few more steps involved.

## puTTY

There are two programs required to do SSH in Windows, puTTYgen and puTTY. These can both be obtained from the puTTY [download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Since putty requires a `.ppk` file rather than `.pem` file (they're essentially the same just a different extension to store the `.pem` data) for private key authentication. Fire up `puTTYgen.exe` and load the .pem file you just. `Select file > load private key`. Change the file type filter to all files (*.*), select your `.pem` file and will bring up a dialog that you have successfully imported a foreign key. `Select file > save private key`.

We know have our private key in the right format (`.ppk`). Close puTTYgen and and open puTTY.

Under sessions enter your public DNS of your instance you just created, prefix the address with ubuntu@ so it will automatically use that as your username to login. Make sure port is 22 and SSH is selected in connection type.

In the same window go to `Connection > SSH > Auth`. Click browse for Private key file for authentication file input and select your newly generated `.ppk` file.

To avoid repeating these steps you can save your session details for easier connecting. Jump back to `Sessions` and enter a name under `Saved Sessions` and click `Save`. Now all you do is double click you saved session to connect.

Head back to the [install instructions](INSTALL.md#installsoftware) to continue your setup.