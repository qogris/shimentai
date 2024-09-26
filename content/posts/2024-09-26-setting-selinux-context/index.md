---
title: Setting SELinux Context
date: 2024-09-26T08:04:49.187Z
lastmod: 2024-09-26T08:04:49.187Z
draft: false
description: Setting the correct SELinux context to allow Nginx to access and serve content from non-root directories while maintaining SELinux security.
summary: Setting the correct SELinux context to allow Nginx to access and serve content from non-root directories while maintaining SELinux security.
tags:
    - selinux
    - context
    - permissions
    - nginx
categories:
    - Reference
authors: haifeng
isCJKLanguage: false
fmContentType: posts
slug: setting-selinux-context
---
By default, SELinux restricts Nginx from accessing files and directories outside of specific locations (like `/var/www`). To let Nginx access a folder, you'll need to apply the correct SELinux labels.

Here’s a step-by-step guide:

### 0. **Check SELinux Status**

First, check the current status of SELinux to ensure it is enabled:

```bash
sestatus
```

If the status is `enforcing`, configuration will be required.

### 1. **Check the SELinux Context**

First, check the current SELinux context for the folder you want Nginx to access.

```bash
ls -Z /path/to/your/folder
```

This will show the SELinux labels for the folder and its contents.

### 2. **Set the Correct SELinux Context**

To allow Nginx to read and serve files from the folder, you need to label the directory and its contents with the `httpd_sys_content_t` type.

Run the following command:

```bash
sudo semanage fcontext -a -t httpd_sys_content_t "/path/to/your/folder(/.*)?"
```

Explanation:

- `-a`: Add a new rule.
- `-t httpd_sys_content_t`: Sets the SELinux type to allow Nginx access.
- `"/path/to/your/folder(/.*)?"`: This applies the rule to the folder and all files and subdirectories within it.

### 3. **Apply the Context Recursively**

After setting the context, apply it to the folder and its contents:

```bash
sudo restorecon -R -v /path/to/your/folder
```

This command will apply the correct SELinux context (`httpd_sys_content_t`) to the folder and all files within it.

### 4. **Verify the Changes**

To verify that the correct SELinux context has been applied, run:

```bash
ls -Z /path/to/your/folder
```

Make sure that the files and directories have the `httpd_sys_content_t` type.

### 5. **Test Nginx Access**

After applying the SELinux labels, restart Nginx and test whether it can access the folder.

```bash
sudo systemctl restart nginx
```

Then, try accessing the site served by Nginx. If you encounter issues, check the Nginx error logs for additional details:

```bash
sudo tail -f /var/log/nginx/error.log
```

### 6. **Optional: Allow Write Access**

If you need Nginx to write to the directory (for example, if you have a file upload feature), you'll need to apply a different SELinux label: `httpd_sys_rw_content_t`. Here's how:

```bash
sudo semanage fcontext -a -t httpd_sys_rw_content_t "/path/to/your/folder(/.*)?"
sudo restorecon -R -v /path/to/your/folder
```

Now, Nginx will be able to read from and write to this directory.

### **Conclusion**

By setting the correct SELinux context (`httpd_sys_content_t` or `httpd_sys_rw_content_t`), you allow Nginx to access and serve content from non-root directories while maintaining SELinux security.
