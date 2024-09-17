<p align="center">
    <i>🚀 <a href="https://keycloakify.dev">Keycloakify</a> v10 starter 🚀</i>
    <br/>
    <br/>
</p>

This starter is based on Vite. There is also [a Webpack based starter](https://github.com/keycloakify/keycloakify-starter-webpack).

# Quick start

```bash
git clone https://github.com/Royce-Geospatial-Consultants/rg-keycloakify-starter.git
cd rg-keycloakify-starter
yarn install # Or use an other package manager, just be sure to delete the yarn.lock if you use another package manager.
```

# Testing the theme locally

[Documentation](https://docs.keycloakify.dev/v/v10/testing-your-theme) (Recommended: Running in a Keycloak Docker Container)

# How to customize the theme

[Documentation](https://docs.keycloakify.dev/v/v10/customization-strategies)

# Building the theme

You need to have [Maven](https://maven.apache.org/) installed to build the theme (Maven >= 3.1.1, Java >= 7).  
The `mvn` command must be in the $PATH.  

-   On macOS: `brew install maven`
-   On Debian/Ubuntu: `sudo apt-get install maven`
-   On Windows: `choco install openjdk` and `choco install maven` (Or download from [here](https://maven.apache.org/download.cgi))

```bash
npm run build-keycloak-theme
```

Note that by default Keycloakify generates multiple .jar files for different versions of Keycloak.  
You can customize this behavior, see documentation [here](https://docs.keycloakify.dev/targeting-specific-keycloak-versions).

# Deploying the theme

[Documentation](https://docs.keycloakify.dev/importing-your-theme-in-keycloak) (Use the Bare Metal option)

Once you have the .jar file for the correct version of Keycloak, drop it into the currently running GCP Keycloak VM instance you want to apply the theme to.

-   Make sure you have permissions to SSH into the VM and are able to use sudo
-   Upload the .jar, then move it into `/mnt/{keycloak-directory}/providers`
-   From the keycloak directory:
    -   `sudo bin/kc.sh build`
    -   `sudo systemctl restart keycloak`
-   In a web browser, head to the Keycloak domain you applied this theme to
-   Log in, select "Realm Settings" and head to "Themes"
-   Under "Login theme" you should find the corresponding theme name specified in `vite.config.ts`
-   Select it to apply the theme, then log out to see the theme in effect on the Login page


# Initializing the account theme (Optional)

```bash
npx keycloakify initialize-account-theme
```

# Initializing the email theme (Optional)

```bash
npx keycloakify initialize-email-theme
```

# GitHub Actions

The starter comes with a generic GitHub Actions workflow that builds the theme and publishes
the jars [as GitHub releases artifacts](https://github.com/keycloakify/keycloakify-starter/releases/tag/v10.0.0).  
To release a new version **just update the `package.json` version and push**.

To enable the workflow go to your fork of this repository on GitHub then navigate to:
`Settings` > `Actions` > `Workflow permissions`, select `Read and write permissions`.
