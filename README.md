# LSRegistry

<div align="center">

![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge)
![Used With](https://img.shields.io/badge/Used_With-LSPotato-orange?style=for-the-badge)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)

**A centralized storage location for registries used with LSPotato and LSCherry**

[Submit Registry](#how-to-register-your-registry) • [Documentation](#registry-structure) • [Examples](#example-structure)

</div>

---

## 📖 Overview

LSRegistry is a public repository that serves as a centralized registry hub for LSPotato and LSCherry. It allows creators to publish and manage their Blender asset registries, making them easily accessible to the community through a standardized namespace system.

## ✨ Features

- 🎯 **Namespace-based Organization** - Clear hierarchical structure for registry identification
- 🔄 **Version Management** - Support for multiple versions with release tracking
- 🔗 **Direct Repository Integration** - Link directly to your GitHub or other platform repositories
- 📦 **Flexible Object Linking** - Map specific Blender objects from your `.blend` files
- 🔐 **Optional Credential Support** - Private repository access when needed

## 🚀 How to Register Your Registry

### Step 1: Fork the Repository

1. Navigate to [LSRegistry](https://github.com/lvoxx/LSRegistry)
2. Click the **Fork** button in the top-right corner
3. Clone your forked repository to your local machine:

```bash
git clone https://github.com/YOUR_USERNAME/LSRegistry.git
cd LSRegistry
```

### Step 2: Register Your Registry

Create your registry entry in LSRegistry with the following structure:

#### 2.1 Create Your Namespace Folder

Create a folder structure matching your desired namespace. For example, if your namespace is `io.user.some-registry`, create:

```
io/
  └── user/
      └── some-registry/
```

#### 2.2 Create `registry.yaml`

Inside your namespace folder, create a `registry.yaml` file with this structure:

```yaml
metadata:
  user: your-github-username
  repository: your-repository-name
  platform: github  # or 'amazon' for other platforms
  credentials: none  # or 'requested' if private repo
  branch: main  # or specify your branch name
```

**Field Descriptions:**
- `user`: Your username on the hosting platform
- `repository`: The name of your repository
- `platform`: Currently supports `github` or `amazon`
- `credentials`: Set to `none` for public repos, `requested` if authentication is needed
- `branch`: The branch containing your registry file (default: `main`)

### Step 3: Configure Your Source Repository

In your **source repository** (not LSRegistry), create a `registry.ls.yaml` file in the root directory of the branch you specified:

```yaml
namespace: io.user.some-registry  # Must match your LSRegistry namespace

linked-objects-in-files:
  "your-model.blend": "ObjectName"
  "another-asset.blend": "AnotherObject"
  # Best practice: link one object per file

versions:
  v1.0.0:
    tag: v1.0.0
    release-file: release-v1.0.0.zip  # Must be a .zip file
  v1.1.0:
    tag: v1.1.0
    release-file: release-v1.1.0.zip
  # Add more versions as needed
```

**Important Notes:**
- `namespace`: Must exactly match the namespace you registered in LSRegistry
- `linked-objects-in-files`: Maps `.blend` files to specific objects. **Best practice**: One object per file
- `versions`: Define your release versions with tags and corresponding `.zip` files
- `release-file`: **Must be a `.zip` file**

### Step 4: Create a Pull Request

1. Commit your changes:

```bash
git add .
git commit -m "Add registry for io.user.some-registry"
git push origin main
```

2. Go to your forked repository on GitHub
3. Click **Pull Request** → **New Pull Request**
4. Set base repository: `lvoxx/LSRegistry` and base: `main`
5. Set head repository: `YOUR_USERNAME/LSRegistry` and compare: `main`
6. Click **Create Pull Request**
7. Fill in the PR description with:
   - Your registry namespace
   - Brief description of your assets
   - Any special notes or requirements

8. Submit and wait for review!

## 📁 Example Structure

Here's a complete example of a registry setup:

### LSRegistry Structure
```
LSRegistry/
├── com/
│   └── example/
│       └── my-assets/
│           └── registry.yaml
```

### `registry.yaml` Example
```yaml
metadata:
  user: johndoe
  repository: blender-awesome-assets
  platform: github
  credentials: none
  branch: main
```

### Source Repository Structure
```
blender-awesome-assets/
├── registry.ls.yaml
├── assets/
│   ├── chair-model.blend
│   └── table-model.blend
└── releases/
    ├── release-v1.0.0.zip
    └── release-v2.0.0.zip
```

### `registry.ls.yaml` Example
```yaml
namespace: com.example.my-assets

linked-objects-in-files:
  "chair-model.blend": "ChairMesh"
  "table-model.blend": "TableMesh"

versions:
  v1.0.0:
    tag: v1.0.0
    release-file: release-v1.0.0.zip
  v2.0.0:
    tag: v2.0.0
    release-file: release-v2.0.0.zip
```

## 🔄 Updating Your Registry

When you have a new release:

1. Update the `registry.ls.yaml` in your **source repository**
2. Add your new version entry:

```yaml
versions:
  v2.1.0:
    tag: v2.1.0
    release-file: release-v2.1.0.zip
```

3. Push the changes to your repository
4. **No need to update LSRegistry** - changes are automatically detected from your source repository!

## 📋 Requirements Checklist

Before submitting your registry, ensure:

- [ ] Namespace folder structure is correct (e.g., `io/user/registry-name/`)
- [ ] `registry.yaml` exists in your namespace folder with all required fields
- [ ] `registry.ls.yaml` exists in your source repository root (on specified branch)
- [ ] Namespace in both files match exactly
- [ ] All release files are `.zip` format
- [ ] Linked objects exist in the specified `.blend` files
- [ ] Repository is accessible (public or credentials provided)

## 🤝 Contributing

We welcome contributions! If you encounter issues or have suggestions:

1. Open an issue describing the problem or feature request
2. For bug fixes or improvements, submit a pull request
3. Follow the existing code structure and naming conventions

## 📄 License

This project is licensed under the Apache License 2.0 - see the LICENSE file in the repository for details.

## 🔗 Related Projects

- [**LSPotato**](https://github.com/lvoxx/LSPotato) - Asset management tool for Blender
- [**LSCherry**](https://github.com/lvoxx/LSCherry) - Toon Shader Framework for Blender

---

<div align="center">

**Made with ❤️ for the Blender community**

If you find this useful, please ⭐ star the repository!

</div>
