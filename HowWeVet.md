# How We Vet

Still trying to sort this out. These are the 3 competing ideas.

## 1. 🔍 Simple Vetting: Verify the Commit is on the Main Branch

This is the most common and easiest automated check. It assumes that the official, approved code for a plugin resides on the plugin author's main branch (`main` or `master`).

- **Logic:** Your CI/CD script (or a manual reviewer) checks if the submitted `commit_hash` is a **direct ancestor** of the external repository's current `main` branch HEAD.
    
- **How it works (in Git terms):** You would use a command like `git merge-base --is-ancestor [commit_hash] [main_branch_head]`.
    
    - If it returns true, the commit is a recognized, merged, and published part of the plugin's official history. **(Approved)**
        
    - If it returns false, the commit is either from an unmerged feature branch, a rejected PR, or a private branch. **(Unapproved/Unverified)**
        
- **Limitation:** This assumes the developer **always** merges approved PRs into their `main` branch. If they use tags for releases on side branches, this check would fail.
    

---

## 2. 🏷️ Strict Vetting: Mandate a Signed Tag

This is the strongest assurance of author intent, ensuring the specific code has been explicitly marked as a "Release" by the plugin author.

- **Logic:** **Require the developer to submit a specific Git Tag** (e.g., `v1.2.0`) instead of a raw commit hash.
    
- **How it works:**
    
    1. The developer creates a **Signed Tag** on their plugin repository (e.g., `git tag -s v1.2.0`). This cryptographic signature proves the tag was created by their verified private key.
        
    2. Your CI/CD script clones the external repo, checks out the tag, and **verifies the GPG signature** on that tag against the developer's known public key.
        
- **Benefit:** This confirms that the plugin author **deliberately created a release point** for this version. You are only building code that the original developer has officially blessed.
    
- **Drawback:** This is complex, as it requires you to manage a list of GPG public keys for all plugin authors and integrate GPG verification into your CI/CD pipeline.
    

---

## 3. 🎯 GitHub-Specific Vetting: Rely on the `Release` API

If the external plugin repository is on GitHub, you can use the GitHub API to check if the commit is associated with an official **GitHub Release**.

- **Logic:** Your CI/CD script queries the plugin repository's **Releases API** and checks if the submitted `commit_hash` is the **target commit** for any of the repository's official GitHub Releases.
    
- **Benefit:** This is easier to automate than GPG tags and confirms the code was deemed stable enough for a release build by the original author.
    
- **Limitation:** It only works for GitHub-hosted plugins, and it doesn't prevent an author from creating a "release" from an unapproved feature branch.
    

---

## 4. 📝 Manual Vetting: Review the Plugin's PR History

This is the necessary fallback, especially for the first submission of a new plugin.

- **Logic:** The human reviewer (you) must click the submitted `source_url` and look at the repository's **Pull Request** and **Issues** history.
    
- **Verification Steps:**
    
    1. Search the Issues/PRs for discussions related to the version you are about to merge.
        
    2. Check if the provided `commit_hash` is part of a large, well-documented feature PR that was recently merged into the main branch.
        
    3. If the plugin is open-source, verify that the code change in the commit is minor and logically consistent with the claimed purpose of the release.
        

For maximum security in your **Notepad#** environment, you should implement the **Simple Vetting (Method 1)** as an automated CI check and use **Manual Vetting (Method 4)** for every new plugin submission and any submission that fails the automated check.