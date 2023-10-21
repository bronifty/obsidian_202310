1) Workflows - attached to repo; contains one or more jobs; triggered by events
2) Jobs - define a runner (execution env); contain one or more steps; can be conditional; executed in parallel by default (can be updated to series)
3) Steps - belong to jobs; either a shell script or an Action (predefined tasks); executed in series; can be conditional
### Example Workflow
```yaml
name: First Workflow
on: workflow_dispatch
jobs:
  first-job:
    runs-on: ubuntu-latest
    steps:
      - name: Print greeting
        run: echo "Hello World!"
      - name: Print goodbye
        run: echo "Done - bye!"
```

> multiline commands
```yaml
run: |
	echo "First output"
	echo "Second output"
```

> example triggers - search github actions events
- eg pull request opened

#### Example to 
```yaml
name: Test workflow
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install nodejs
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install deps
        run: npm ci
      - name: Run tests
        run: npm run test
```

> every job has its own runner
> we can make jobs go in serial with a 'needs' key (like docker compose dependency)
```yaml
name: Test workflow
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install nodejs
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install deps
        run: npm ci
      - name: Run tests
        run: npm run test
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install nodejs
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install deps
        run: npm ci
      - name: Build project
        run: npm run build
      - name: Deploy
        run: echo "deploying"
```

> github context
```yaml
name: Output Information
on: workflow_dispatch
jobs:
  info:
    runs-on: ubuntu-latest
    steps:
      - name: print
        run: echo "${{toJson(github)}}"
```

```json
{
  token: ***,
  job: info,
  ref: refs/heads/main,
  sha: 05558d77512506a46da1cd3534764a33545d8759,
  repository: bronifty/delete-me-1,
  repository_owner: bronifty,
  repository_owner_id: 86934366,
  repositoryUrl: git://github.com/bronifty/delete-me-1.git,
  run_id: 6597573893,
  run_number: 1,
  retention_days: 90,
  run_attempt: 1,
  artifact_cache_size_limit: 10,
  repository_visibility: private,
  repo-self-hosted-runners-disabled: false,
  enterprise-managed-business-id: ,
  repository_id: 707894095,
  actor_id: 86934366,
  actor: bronifty,
  triggering_actor: bronifty,
  workflow: Output Information,
  head_ref: ,
  base_ref: ,
  event_name: workflow_dispatch,
  event: {
    inputs: null,
    ref: refs/heads/main,
    repository: {
      allow_forking: true,
      archive_url: https://api.github.com/repos/bronifty/delete-me-1/{archive_format}{/ref},
      archived: false,
      assignees_url: https://api.github.com/repos/bronifty/delete-me-1/assignees{/user},
      blobs_url: https://api.github.com/repos/bronifty/delete-me-1/git/blobs{/sha},
      branches_url: https://api.github.com/repos/bronifty/delete-me-1/branches{/branch},
      clone_url: https://github.com/bronifty/delete-me-1.git,
      collaborators_url: https://api.github.com/repos/bronifty/delete-me-1/collaborators{/collaborator},
      comments_url: https://api.github.com/repos/bronifty/delete-me-1/comments{/number},
      commits_url: https://api.github.com/repos/bronifty/delete-me-1/commits{/sha},
      compare_url: https://api.github.com/repos/bronifty/delete-me-1/compare/{base}...{head},
      contents_url: https://api.github.com/repos/bronifty/delete-me-1/contents/{+path},
      contributors_url: https://api.github.com/repos/bronifty/delete-me-1/contributors,
      created_at: 2023-10-20T23:07:25Z,
      default_branch: main,
      deployments_url: https://api.github.com/repos/bronifty/delete-me-1/deployments,
      description: null,
      disabled: false,
      downloads_url: https://api.github.com/repos/bronifty/delete-me-1/downloads,
      events_url: https://api.github.com/repos/bronifty/delete-me-1/events,
      fork: false,
      forks: 0,
      forks_count: 0,
      forks_url: https://api.github.com/repos/bronifty/delete-me-1/forks,
      full_name: bronifty/delete-me-1,
      git_commits_url: https://api.github.com/repos/bronifty/delete-me-1/git/commits{/sha},
      git_refs_url: https://api.github.com/repos/bronifty/delete-me-1/git/refs{/sha},
      git_tags_url: https://api.github.com/repos/bronifty/delete-me-1/git/tags{/sha},
      git_url: git://github.com/bronifty/delete-me-1.git,
      has_discussions: false,
      has_downloads: true,
      has_issues: true,
      has_pages: false,
      has_projects: true,
      has_wiki: false,
      homepage: null,
      hooks_url: https://api.github.com/repos/bronifty/delete-me-1/hooks,
      html_url: https://github.com/bronifty/delete-me-1,
      id: 707894095,
      is_template: false,
      issue_comment_url: https://api.github.com/repos/bronifty/delete-me-1/issues/comments{/number},
      issue_events_url: https://api.github.com/repos/bronifty/delete-me-1/issues/events{/number},
      issues_url: https://api.github.com/repos/bronifty/delete-me-1/issues{/number},
      keys_url: https://api.github.com/repos/bronifty/delete-me-1/keys{/key_id},
      labels_url: https://api.github.com/repos/bronifty/delete-me-1/labels{/name},
      language: JavaScript,
      languages_url: https://api.github.com/repos/bronifty/delete-me-1/languages,
      license: null,
      merges_url: https://api.github.com/repos/bronifty/delete-me-1/merges,
      milestones_url: https://api.github.com/repos/bronifty/delete-me-1/milestones{/number},
      mirror_url: null,
      name: delete-me-1,
      node_id: R_kgDOKjGbTw,
      notifications_url: https://api.github.com/repos/bronifty/delete-me-1/notifications?since,
      open_issues: 0,
      open_issues_count: 0,
      owner: {
        avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
        events_url: https://api.github.com/users/bronifty/events{/privacy},
        followers_url: https://api.github.com/users/bronifty/followers,
        following_url: https://api.github.com/users/bronifty/following{/other_user},
        gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
        gravatar_id: ,
        html_url: https://github.com/bronifty,
        id: 86934366,
        login: bronifty,
        node_id: MDQ6VXNlcjg2OTM0MzY2,
        organizations_url: https://api.github.com/users/bronifty/orgs,
        received_events_url: https://api.github.com/users/bronifty/received_events,
        repos_url: https://api.github.com/users/bronifty/repos,
        site_admin: false,
        starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
        subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
        type: User,
        url: https://api.github.com/users/bronifty
      },
      private: true,
      pulls_url: https://api.github.com/repos/bronifty/delete-me-1/pulls{/number},
      pushed_at: 2023-10-21T13:08:14Z,
      releases_url: https://api.github.com/repos/bronifty/delete-me-1/releases{/id},
      size: 106,
      ssh_url: git@github.com:bronifty/delete-me-1.git,
      stargazers_count: 0,
      stargazers_url: https://api.github.com/repos/bronifty/delete-me-1/stargazers,
      statuses_url: https://api.github.com/repos/bronifty/delete-me-1/statuses/{sha},
      subscribers_url: https://api.github.com/repos/bronifty/delete-me-1/subscribers,
      subscription_url: https://api.github.com/repos/bronifty/delete-me-1/subscription,
      svn_url: https://github.com/bronifty/delete-me-1,
      tags_url: https://api.github.com/repos/bronifty/delete-me-1/tags,
      teams_url: https://api.github.com/repos/bronifty/delete-me-1/teams,
      topics: [],
      trees_url: https://api.github.com/repos/bronifty/delete-me-1/git/trees{/sha},
      updated_at: 2023-10-20T23:08:01Z,
      url: https://api.github.com/repos/bronifty/delete-me-1,
      visibility: private,
      watchers: 0,
      watchers_count: 0,
      web_commit_signoff_required: false
    },
    sender: {
      avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
      events_url: https://api.github.com/users/bronifty/events{/privacy},
      followers_url: https://api.github.com/users/bronifty/followers,
      following_url: https://api.github.com/users/bronifty/following{/other_user},
      gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
      gravatar_id: ,
      html_url: https://github.com/bronifty,
      id: 86934366,
      login: bronifty,
      node_id: MDQ6VXNlcjg2OTM0MzY2,
      organizations_url: https://api.github.com/users/bronifty/orgs,
      received_events_url: https://api.github.com/users/bronifty/received_events,
      repos_url: https://api.github.com/users/bronifty/repos,
      site_admin: false,
      starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
      subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
      type: User,
      url: https://api.github.com/users/bronifty
    },
    workflow: .github/workflows/output.yml
  },
  server_url: https://github.com,
  api_url: https://api.github.com,
  graphql_url: https://api.github.com/graphql,
  ref_name: main,
  ref_protected: false,
  ref_type: branch,
  secret_source: Actions,
  workflow_ref: bronifty/delete-me-1/.github/workflows/output.yml@refs/heads/main,
  workflow_sha: 05558d77512506a46da1cd3534764a33545d8759,
  workspace: /home/runner/work/delete-me-1/delete-me-1,
  action: __run,
  event_path: /home/runner/work/_temp/_github_workflow/event.json,
  action_repository: ,
  action_ref: ,
  path: /home/runner/work/_temp/_runner_file_commands/add_path_a436c4fb-eab8-433a-af69-4689573fd269,
  env: /home/runner/work/_temp/_runner_file_commands/set_env_a436c4fb-eab8-433a-af69-4689573fd269,
  step_summary: /home/runner/work/_temp/_runner_file_commands/step_summary_a436c4fb-eab8-433a-af69-4689573fd269,
  state: /home/runner/work/_temp/_runner_file_commands/save_state_a436c4fb-eab8-433a-af69-4689573fd269,
  output: /home/runner/work/_temp/_runner_file_commands/set_output_a436c4fb-eab8-433a-af69-4689573fd269
} Information,
  head_ref: ,
  base_ref: ,
  event_name: workflow_dispatch,
  event: {
    inputs: null,
    ref: refs/heads/main,
    repository: {
      allow_forking: true,
      archive_url: https://api.github.com/repos/bronifty/delete-me-1/{archive_format}{/ref},
      archived: false,
      assignees_url: https://api.github.com/repos/bronifty/delete-me-1/assignees{/user},
      blobs_url: https://api.github.com/repos/bronifty/delete-me-1/git/blobs{/sha},
      branches_url: https://api.github.com/repos/bronifty/delete-me-1/branches{/branch},
      clone_url: https://github.com/bronifty/delete-me-1.git,
      collaborators_url: https://api.github.com/repos/bronifty/delete-me-1/collaborators{/collaborator},
      comments_url: https://api.github.com/repos/bronifty/delete-me-1/comments{/number},
      commits_url: https://api.github.com/repos/bronifty/delete-me-1/commits{/sha},
      compare_url: https://api.github.com/repos/bronifty/delete-me-1/compare/{base}...{head},
      contents_url: https://api.github.com/repos/bronifty/delete-me-1/contents/{+path},
      contributors_url: https://api.github.com/repos/bronifty/delete-me-1/contributors,
      created_at: 2023-10-20T23:07:25Z,
      default_branch: main,
      deployments_url: https://api.github.com/repos/bronifty/delete-me-1/deployments,
      description: null,
      disabled: false,
      downloads_url: https://api.github.com/repos/bronifty/delete-me-1/downloads,
      events_url: https://api.github.com/repos/bronifty/delete-me-1/events,
      fork: false,
      forks: 0,
      forks_count: 0,
      forks_url: https://api.github.com/repos/bronifty/delete-me-1/forks,
      full_name: bronifty/delete-me-1,
      git_commits_url: https://api.github.com/repos/bronifty/delete-me-1/git/commits{/sha},
      git_refs_url: https://api.github.com/repos/bronifty/delete-me-1/git/refs{/sha},
      git_tags_url: https://api.github.com/repos/bronifty/delete-me-1/git/tags{/sha},
      git_url: git://github.com/bronifty/delete-me-1.git,
      has_discussions: false,
      has_downloads: true,
      has_issues: true,
      has_pages: false,
      has_projects: true,
      has_wiki: false,
      homepage: null,
      hooks_url: https://api.github.com/repos/bronifty/delete-me-1/hooks,
      html_url: https://github.com/bronifty/delete-me-1,
      id: 707894095,
      is_template: false,
      issue_comment_url: https://api.github.com/repos/bronifty/delete-me-1/issues/comments{/number},
      issue_events_url: https://api.github.com/repos/bronifty/delete-me-1/issues/events{/number},
      issues_url: https://api.github.com/repos/bronifty/delete-me-1/issues{/number},
      keys_url: https://api.github.com/repos/bronifty/delete-me-1/keys{/key_id},
      labels_url: https://api.github.com/repos/bronifty/delete-me-1/labels{/name},
      language: JavaScript,
      languages_url: https://api.github.com/repos/bronifty/delete-me-1/languages,
      license: null,
      merges_url: https://api.github.com/repos/bronifty/delete-me-1/merges,
      milestones_url: https://api.github.com/repos/bronifty/delete-me-1/milestones{/number},
      mirror_url: null,
      name: delete-me-1,
      node_id: R_kgDOKjGbTw,
      notifications_url: https://api.github.com/repos/bronifty/delete-me-1/notificationsall,
      open_issues: 0,
      open_issues_count: 0,
      owner: {
        avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
        events_url: https://api.github.com/users/bronifty/events{/privacy},
        followers_url: https://api.github.com/users/bronifty/followers,
        following_url: https://api.github.com/users/bronifty/following{/other_user},
        gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
        gravatar_id: ,
        html_url: https://github.com/bronifty,
        id: 86934366,
        login: bronifty,
        node_id: MDQ6VXNlcjg2OTM0MzY2,
        organizations_url: https://api.github.com/users/bronifty/orgs,
        received_events_url: https://api.github.com/users/bronifty/received_events,
        repos_url: https://api.github.com/users/bronifty/repos,
        site_admin: false,
        starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
        subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
        type: User,
        url: https://api.github.com/users/bronifty
      },
      private: true,
      pulls_url: https://api.github.com/repos/bronifty/delete-me-1/pulls{/number},
      pushed_at: 2023-10-21T13:08:14Z,
      releases_url: https://api.github.com/repos/bronifty/delete-me-1/releases{/id},
      size: 106,
      ssh_url: git@github.com:bronifty/delete-me-1.git,
      stargazers_count: 0,
      stargazers_url: https://api.github.com/repos/bronifty/delete-me-1/stargazers,
      statuses_url: https://api.github.com/repos/bronifty/delete-me-1/statuses/{sha},
      subscribers_url: https://api.github.com/repos/bronifty/delete-me-1/subscribers,
      subscription_url: https://api.github.com/repos/bronifty/delete-me-1/subscription,
      svn_url: https://github.com/bronifty/delete-me-1,
      tags_url: https://api.github.com/repos/bronifty/delete-me-1/tags,
      teams_url: https://api.github.com/repos/bronifty/delete-me-1/teams,
      topics: [],
      trees_url: https://api.github.com/repos/bronifty/delete-me-1/git/trees{/sha},
      updated_at: 2023-10-20T23:08:01Z,
      url: https://api.github.com/repos/bronifty/delete-me-1,
      visibility: private,
      watchers: 0,
      watchers_count: 0,
      web_commit_signoff_required: false
    },
    sender: {
      avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
      events_url: https://api.github.com/users/bronifty/events{/privacy},
      followers_url: https://api.github.com/users/bronifty/followers,
      following_url: https://api.github.com/users/bronifty/following{/other_user},
      gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
      gravatar_id: ,
      html_url: https://github.com/bronifty,
      id: 86934366,
      login: bronifty,
      node_id: MDQ6VXNlcjg2OTM0MzY2,
      organizations_url: https://api.github.com/users/bronifty/orgs,
      received_events_url: https://api.github.com/users/bronifty/received_events,
      repos_url: https://api.github.com/users/bronifty/repos,
      site_admin: false,
      starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
      subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
      type: User,
      url: https://api.github.com/users/bronifty
    },
    workflow: .github/workflows/output.yml
  },
  server_url: https://github.com,
  api_url: https://api.github.com,
  graphql_url: https://api.github.com/graphql,
  ref_name: main,
  ref_protected: false,
  ref_type: branch,
  secret_source: Actions,
  workflow_ref: bronifty/delete-me-1/.github/workflows/output.yml@refs/heads/main,
  workflow_sha: 05558d77512506a46da1cd3534764a33545d8759,
  workspace: /home/runner/work/delete-me-1/delete-me-1,
  action: __run,
  event_path: /home/runner/work/_temp/_github_workflow/event.json,
  action_repository: ,
  action_ref: ,
  path: /home/runner/work/_temp/_runner_file_commands/add_path_a436c4fb-eab8-433a-af69-4689573fd269,
  env: /home/runner/work/_temp/_runner_file_commands/set_env_a436c4fb-eab8-433a-af69-4689573fd269,
  step_summary: /home/runner/work/_temp/_runner_file_commands/step_summary_a436c4fb-eab8-433a-af69-4689573fd269,
  state: /home/runner/work/_temp/_runner_file_commands/save_state_a436c4fb-eab8-433a-af69-4689573fd269,
  output: /home/runner/work/_temp/_runner_file_commands/set_output_a436c4fb-eab8-433a-af69-4689573fd269
} Information,
  head_ref: ,
  base_ref: ,
  event_name: workflow_dispatch,
  event: {
    inputs: null,
    ref: refs/heads/main,
    repository: {
      allow_forking: true,
      archive_url: https://api.github.com/repos/bronifty/delete-me-1/{archive_format}{/ref},
      archived: false,
      assignees_url: https://api.github.com/repos/bronifty/delete-me-1/assignees{/user},
      blobs_url: https://api.github.com/repos/bronifty/delete-me-1/git/blobs{/sha},
      branches_url: https://api.github.com/repos/bronifty/delete-me-1/branches{/branch},
      clone_url: https://github.com/bronifty/delete-me-1.git,
      collaborators_url: https://api.github.com/repos/bronifty/delete-me-1/collaborators{/collaborator},
      comments_url: https://api.github.com/repos/bronifty/delete-me-1/comments{/number},
      commits_url: https://api.github.com/repos/bronifty/delete-me-1/commits{/sha},
      compare_url: https://api.github.com/repos/bronifty/delete-me-1/compare/{base}...{head},
      contents_url: https://api.github.com/repos/bronifty/delete-me-1/contents/{+path},
      contributors_url: https://api.github.com/repos/bronifty/delete-me-1/contributors,
      created_at: 2023-10-20T23:07:25Z,
      default_branch: main,
      deployments_url: https://api.github.com/repos/bronifty/delete-me-1/deployments,
      description: null,
      disabled: false,
      downloads_url: https://api.github.com/repos/bronifty/delete-me-1/downloads,
      events_url: https://api.github.com/repos/bronifty/delete-me-1/events,
      fork: false,
      forks: 0,
      forks_count: 0,
      forks_url: https://api.github.com/repos/bronifty/delete-me-1/forks,
      full_name: bronifty/delete-me-1,
      git_commits_url: https://api.github.com/repos/bronifty/delete-me-1/git/commits{/sha},
      git_refs_url: https://api.github.com/repos/bronifty/delete-me-1/git/refs{/sha},
      git_tags_url: https://api.github.com/repos/bronifty/delete-me-1/git/tags{/sha},
      git_url: git://github.com/bronifty/delete-me-1.git,
      has_discussions: false,
      has_downloads: true,
      has_issues: true,
      has_pages: false,
      has_projects: true,
      has_wiki: false,
      homepage: null,
      hooks_url: https://api.github.com/repos/bronifty/delete-me-1/hooks,
      html_url: https://github.com/bronifty/delete-me-1,
      id: 707894095,
      is_template: false,
      issue_comment_url: https://api.github.com/repos/bronifty/delete-me-1/issues/comments{/number},
      issue_events_url: https://api.github.com/repos/bronifty/delete-me-1/issues/events{/number},
      issues_url: https://api.github.com/repos/bronifty/delete-me-1/issues{/number},
      keys_url: https://api.github.com/repos/bronifty/delete-me-1/keys{/key_id},
      labels_url: https://api.github.com/repos/bronifty/delete-me-1/labels{/name},
      language: JavaScript,
      languages_url: https://api.github.com/repos/bronifty/delete-me-1/languages,
      license: null,
      merges_url: https://api.github.com/repos/bronifty/delete-me-1/merges,
      milestones_url: https://api.github.com/repos/bronifty/delete-me-1/milestones{/number},
      mirror_url: null,
      name: delete-me-1,
      node_id: R_kgDOKjGbTw,
      notifications_url: https://api.github.com/repos/bronifty/delete-me-1/notificationsparticipating,
      open_issues: 0,
      open_issues_count: 0,
      owner: {
        avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
        events_url: https://api.github.com/users/bronifty/events{/privacy},
        followers_url: https://api.github.com/users/bronifty/followers,
        following_url: https://api.github.com/users/bronifty/following{/other_user},
        gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
        gravatar_id: ,
        html_url: https://github.com/bronifty,
        id: 86934366,
        login: bronifty,
        node_id: MDQ6VXNlcjg2OTM0MzY2,
        organizations_url: https://api.github.com/users/bronifty/orgs,
        received_events_url: https://api.github.com/users/bronifty/received_events,
        repos_url: https://api.github.com/users/bronifty/repos,
        site_admin: false,
        starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
        subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
        type: User,
        url: https://api.github.com/users/bronifty
      },
      private: true,
      pulls_url: https://api.github.com/repos/bronifty/delete-me-1/pulls{/number},
      pushed_at: 2023-10-21T13:08:14Z,
      releases_url: https://api.github.com/repos/bronifty/delete-me-1/releases{/id},
      size: 106,
      ssh_url: git@github.com:bronifty/delete-me-1.git,
      stargazers_count: 0,
      stargazers_url: https://api.github.com/repos/bronifty/delete-me-1/stargazers,
      statuses_url: https://api.github.com/repos/bronifty/delete-me-1/statuses/{sha},
      subscribers_url: https://api.github.com/repos/bronifty/delete-me-1/subscribers,
      subscription_url: https://api.github.com/repos/bronifty/delete-me-1/subscription,
      svn_url: https://github.com/bronifty/delete-me-1,
      tags_url: https://api.github.com/repos/bronifty/delete-me-1/tags,
      teams_url: https://api.github.com/repos/bronifty/delete-me-1/teams,
      topics: [],
      trees_url: https://api.github.com/repos/bronifty/delete-me-1/git/trees{/sha},
      updated_at: 2023-10-20T23:08:01Z,
      url: https://api.github.com/repos/bronifty/delete-me-1,
      visibility: private,
      watchers: 0,
      watchers_count: 0,
      web_commit_signoff_required: false
    },
    sender: {
      avatar_url: https://avatars.githubusercontent.com/u/86934366?v=4,
      events_url: https://api.github.com/users/bronifty/events{/privacy},
      followers_url: https://api.github.com/users/bronifty/followers,
      following_url: https://api.github.com/users/bronifty/following{/other_user},
      gists_url: https://api.github.com/users/bronifty/gists{/gist_id},
      gravatar_id: ,
      html_url: https://github.com/bronifty,
      id: 86934366,
      login: bronifty,
      node_id: MDQ6VXNlcjg2OTM0MzY2,
      organizations_url: https://api.github.com/users/bronifty/orgs,
      received_events_url: https://api.github.com/users/bronifty/received_events,
      repos_url: https://api.github.com/users/bronifty/repos,
      site_admin: false,
      starred_url: https://api.github.com/users/bronifty/starred{/owner}{/repo},
      subscriptions_url: https://api.github.com/users/bronifty/subscriptions,
      type: User,
      url: https://api.github.com/users/bronifty
    },
    workflow: .github/workflows/output.yml
  },
  server_url: https://github.com,
  api_url: https://api.github.com,
  graphql_url: https://api.github.com/graphql,
  ref_name: main,
  ref_protected: false,
  ref_type: branch,
  secret_source: Actions,
  workflow_ref: bronifty/delete-me-1/.github/workflows/output.yml@refs/heads/main,
  workflow_sha: 05558d77512506a46da1cd3534764a33545d8759,
  workspace: /home/runner/work/delete-me-1/delete-me-1,
  action: __run,
  event_path: /home/runner/work/_temp/_github_workflow/event.json,
  action_repository: ,
  action_ref: ,
  path: /home/runner/work/_temp/_runner_file_commands/add_path_a436c4fb-eab8-433a-af69-4689573fd269,
  env: /home/runner/work/_temp/_runner_file_commands/set_env_a436c4fb-eab8-433a-af69-4689573fd269,
  step_summary: /home/runner/work/_temp/_runner_file_commands/step_summary_a436c4fb-eab8-433a-af69-4689573fd269,
  state: /home/runner/work/_temp/_runner_file_commands/save_state_a436c4fb-eab8-433a-af69-4689573fd269,
  output: /home/runner/work/_temp/_runner_file_commands/set_output_a436c4fb-eab8-433a-af69-4689573fd269
}```
