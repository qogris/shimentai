---
title: Disqus Configuration
date: 2024-09-24T10:25:59Z
lastmod: 2024-09-24T10:25:59Z
draft: false
description: Disqus Configuration
tags:
   - disqus
   - congo
   - hugo
   - patrial
   - template
categories:
   - Reference
summary: To ensure that the Disqus comment system displays correctly, you can follow these steps
slug: disqus-configuration
---

{{<alert "lightbulb">}}
Ref. to [Congo Docs Partials](https://jpanther.github.io/congo/docs/partials/#comments) and  [Hugo Templates Embedded](https://gohugo.io/templates/embedded/#disqus).
{{</alert>}}

### 1. **Get Your Disqus Shortname**

- First, you need to register for a Disqus account and create a site for your Hugo website. The unique identifier for your Disqus site is the **Disqus Shortname**.
- To get this, visit [Disqus](https://disqus.com/) and either sign up or log in. Follow these steps:
     1. After logging in, click on your user icon and select "Add Disqus to Your Site."
     2. Follow the steps to create a new site, and enter a name for your site (e.g., `myblog`).
     3. After the site is created, you'll be given a **Disqus Shortname** (e.g., `myblog`), which is essential for linking your site to Disqus.

   **Note**: The `disqusShortname` is **case-sensitive**, so make sure you enter it exactly as provided by Disqus.

### 2. **Add DisqusShortname to Hugo Configuration**

   In your Hugo project's configuration file (`config.toml` or `config.yaml`), you need to add the Disqus shortname so that Hugo knows which Disqus account to use for comments.

#### If your configuration file is `config.toml`

   Open the `config.toml` file and add the following line:

   ```toml
   disqusShortname = "your-disqus-shortname"
   ```

   Replace `your-disqus-shortname` with the actual shortname you received from Disqus (e.g., `myblog`).

### 3. **Ensure Correct Placement of the Configuration**

   Make sure that the `disqusShortname` is placed in the top-level section of your configuration file. For example, if your `config.toml` file looks like this, the `disqusShortname` should not be inside any specific section or module:

   ```toml
   baseURL = "https://example.com"
   title = "My Hugo Blog"
   languageCode = "en-us"

   # Disqus configuration
   disqusShortname = "myblog"
   ```

   If it's nested incorrectly under a specific block, Hugo might not detect it.

### 4. **Create a Disqus Template**

  In `_default/single.html` of Congo Theme Configuration, there is a default call to `partials/comments.html`, so what we need to do is just creating this `comments.html` partial and include the Hugo embedded template:

   ```toml
  {{ template "_internal/disqus.html" . }}
   ```

### 5. **Confirm the Call to Comments Partial**

You have already added `{{ template "_internal/disqus.html" . }}` to `partials/comments.html`, and make sure you have set the `disqusShortname` in your Hugo project’s `config.toml` (or `config.yaml`) file. This is necessary for the Disqus comment system to work.

### 6. **Test the Configuration**

   To check if the Disqus comments are working, you can run Hugo's local development server:

   ```bash
   hugo server --disableFastRender
   ```

   Then visit any single post page on your local development server to see if the Disqus comment box appears at the bottom of the page. If everything is set up correctly, you should see the Disqus comment section.
