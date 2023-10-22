- git log to check commit history
- git checkout commit-hash to return to a commit 
- get checkout branch-name to return HEAD to the last commit in the branch

```sh
git log
git checkout f3ac63ffc8336079dc0a732c948bffdb846c753f
git log # does not show cany commits except for the ones before this
git checkout main
git log # shows call commits (we are back on main at the last commit)
```



commit f3ac63ffc8336079dc0a732c948bffdb846c753f
Author: bronifty <bronifty@gmail.com>
Date:   Wed Sep 27 05:53:36 2023 -0400

    updated gitignore

commit 05d1681678412864fbe6461f438252629419d250
Merge: 05b48ab4 380c161a
Author: bronifty <bronifty@gmail.com>
Date:   Tue Sep 26 15:22:26 2023 -0400

    Merge branch 'main' of https://github.com/bronifty/wing

commit 05b48ab41aec1d3257d346035cb5ee0a89e2b029
Author: bronifty <bronifty@gmail.com>
Date:   Tue Sep 26 15:19:59 2023 -0400

    updated wing compiler to use cjs

commit 380c161a2996efe1f481e6efc86e768bf05cdb6d
Author: TATSUNO “Taz” Yasuhiro <ytatsuno.jp@gmail.com>
Date:   Tue Sep 26 23:41:08 2023 +0900

    fix(sdk): better error message on unsupported compile target (#4282)
    
    closes https://github.com/winglang/wing/issues/4172
    
    The new error message tells that the resource still needs to be implemented for the 
target.
    It also includes a link to the roadmap with a filter, so user can find the ticket fo
r the implementation
    
    Before | After
    ---|---
    Unable to create an instance of abstract type "@winglang/sdk.cloud.Api" for this tar
get | Resource "@winglang/sdk.cloud.Api" is not yet implemented for "awscdk" target. Ple
ase refer to the roadmap https://github.com/orgs/winglang/projects/3/views/1?filterQuery
=cloud.Api
    
    ## Checklist
    
    - [x] Title matches [Winglang's style guide](https://www.winglang.io/contributing/st
art-here/pull_requests#how-are-pull-request-titles-formatted)
    - [x] Description explains motivation and solution
    - [x] Tests added (always)
    - [x] Docs updated (only required for features)
    - [ ] Added `pr/e2e-full` label if this feature requires end-to-end testing
    
    *By submitting this pull request, I confirm that my contribution is made under the t
erms of the [Wing Cloud Contribution License](https://github.com/winglang/wing/blob/main
/CONTRIBUTION_LICENSE.md)*.