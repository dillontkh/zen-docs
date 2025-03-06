---
title: Building Zen Browser 📦
lastmod: 2025-03-06
---

We've taken the time to make building Zen Browser as easy as possible, independent of your operating system or technical knowledge. 

> [!failure]
> We cannot provide support if a build fails. Please understand this before proceeding with the following steps.

## Step 1: Clone the Project

First, you need to clone the Zen Browser repository to your local machine. This will create a local copy of the project that you can work on.

```bash
git clone https://github.com/zen-browser/desktop.git --recurse-submodules
cd desktop
```

- **`--recurse-submodules`**: This flag ensures that all submodules are cloned along with the main project. Zen Browser relies on several submodules, so this step is essential.

## Step 2: Install Dependencies

Once you have cloned the project, navigate to the project directory and install the necessary dependencies using npm:

```bash
pnpm i
```

This command will install all the packages listed in the `package.json` file, which are required for building and running Zen Browser.

If you see this error message:

<div align="center">
	<img src="/assets/building/ignored-builds-warning.png" width="80%">
</div>

Run `pnpm approve-builds` and approve them.

## Step 3: Download and Bootstrap the Browser

To set up the browser, you need to download additional files and prepare the environment:

```bash
pnpm run init
```

This command handles all the necessary bootstrapping tasks, such as setting up configuration files and downloading essential resources.

## Step 4: Update Language Packs 

Before building the browser, it’s recommended to update the American English language packs to ensure that all localization files are up-to-date:

```bash
python3 ./scripts/update_en_US_packs.py
```

This script updates the "en-US" localization files, which are necessary for proper language support in Zen Browser. Running this step ensures that your build includes the latest translations and language resources.

## Step 5: Build the Browser

Now that everything is set up, you can build the browser:

```bash
pnpm build
```

This command compiles the source code and creates the necessary files for running Zen Browser.

## Step 6: Run the Browser

After building the browser, you can start it using:

```bash
pnpm start
```

This command launches the browser, allowing you to see your changes in action.

# Troubleshooting

<details>
<summary>[Windows] Error: ccache not found</summary>

Add `C:\Users\<your_user>\.mozbuild\sccache` to your PATH.

</details>

<details>
<summary>[Windows] Error: 7z not found</summary>

Download <a href="https://www.7-zip.org/download.html">7-zip</a> and add it to your PATH.

</details>

<details>
<summary>[All OS] My code changes are not being reflected even after building</summary>

If you are changing files in the `src/` directory:

```bash
pnpm run import
pnpm run build:ui
```

</details>

<details>
<summary>[All OS] Something went wrong installing the "sharp" module</summary>

You likely did not approve builds in [Step 2](#step-2-install-dependencies).

</details>
