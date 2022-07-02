(Visual Studio Code Setup Install)[https://code.visualstudio.com/docs/setup/linux]<br />

# Setup Repo and Key
* `sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc`
* `sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'`

# Update Package cache
* `sudo dnf check-update`

# Install Visual Studio Code
* `sudo dnf install code`
