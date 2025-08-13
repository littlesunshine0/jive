---
title: Xcode Templates
date: 2025-08-13
draft: false
slug: xcode-templates
---
# Xcode Templates

Creating Project Templates for Bash

### **Introduction**

This guide will walk you through creating an Xcode project template for organizing and running shell scripts. Instead of compiling code, this template uses Xcode's "External Build System" project type. When you build the project, it will execute a script of your choice.

### **Directions & Important Paths**

This template will create a project that, when built (?B), executes a main build.sh script. This script's job is to call other initialization scripts in the project. By default, it only runs init_server.sh, which scaffolds a local Vapor server.

**Key Paths Used (Defaults):**

- **Project Root (ROOT):** ~/Projects

- **Server Source Code (SERVER_DIR):** ~/Projects/LocalAPIServer

- **Database Directory (DB_DIR):** ~/Library/Application Support/LocalAPIServer

- **Database File (DB_PATH):** ~/Library/Application Support/LocalAPIServer/db.sqlite

You can override these paths by setting environment variables before running the build, for example: ROOT=/path/to/my/dev ./build.sh.

### **Step 1: Create the Directory Structure**

First, we'll create a new folder for our template in the custom project templates directory.

Create the path where Xcode looks for custom project templates
- **File Location:** ~/Library/Developer/Xcode/Templates/Project Templates/Custom/Bash Script Project.xctemplate

### **Step 2: Create the Template Information File**

The TemplateInfo.plist must be updated to include all the scripts that are part of the project.

Create the plist file and add its content
### **Step 3: Create the Source Scripts**

Now we create all four scripts. build.sh is the main entry point, and the others are separate files.

#### **Create build.sh (The Orchestrator)**

Create the main build.sh file
#### **Create init_server.sh (The Scaffolding Script)**

Create the init_server.sh file
#### **Create init_browser-app.sh**

This script now contains the full logic for scaffolding the Vite/React frontend.

Create init_browser-app.sh
#### **Create init_swift-app.sh (Placeholder)**

Create init_swift-app.sh
### **Step 4: Make the Scripts Executable**

This is a crucial step to ensure all scripts can be run.

chmod +x build.sh \
chmod +x init_server.sh \
chmod +x init_browser-app.sh \
chmod +x init_swift-app.sh

### **Step 5: Restart Xcode**

For Xcode to find your new template, you must **completely quit and restart it**.

Once restarted, go to **File > New > Project...**. Under the "Custom" section, you'll find your "Bash Script Project". When you create a project from it and press **Build** (?B), it will run the build.sh script, which in turn runs the server initialization.
