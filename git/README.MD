
# Difference between git-submodule and -subtree

## git submodule
With git submodules you typically want to separate a large repository into smaller ones. The way of referencing a submodule is maven-style - you are referencing a single commit from the other (submodule) repository. If you need a change within the submodule you have to make a commit/push within the submodule, then reference the new commit in the main repository and then commit/push the changed reference of the main repository. That way you have to have access to both repositories for the complete build.

## git subtree

With git subtree you integrate another repository in yours, including its history. So after integrating it, the size of your repository is probably bigger (so this is no strategy to keep repositories smaller). After the integration there is no connection to the other repository, and you don't need access to it unless you want to get an update. So this strategy is more for code and history reuse - I personally don't use it.