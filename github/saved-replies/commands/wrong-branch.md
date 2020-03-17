@github-actions run

<details>
<summary>⛔ Wrong branch</summary>

```js
(async () => {
  // Get issue/PR number
  const number = context.issue.number;

  // Change base to "develop"
  await githubClient.pulls.update({
    owner: context.repo.owner,
    repo: context.repo.repo,
    pull_number: number,
    base: 'develop'
  });

  // Comment body
  const commentBody = 'This pull request has been made to the wrong branch. As per our'
    + ' [Contribution Guide](https://github.com/octobercms/october/blob/master/.github/CONTRIBUTING.md#making-a-pull-request)'
    + ', all pull requests must be made to the `develop` branch.'
    + '\n\n'
    + 'We have automatically changed your pull request to be merged to the `develop` branch for you. Please ensure that'
    + ' any future pull requests are made to the develop branch.';

  // Add comment
  await postComment(commentBody);
})();
