@github-actions run

<details>
<summary>✔ Ready for testing</summary>

```js
(async () => {
  // Get issue/PR number
  const number = context.issue.number;

  // Add Testing Needed label
  await githubClient.issues.addLabels({
    owner: context.repo.owner,
    repo: context.repo.repo,
    issue_number: number,
    labels: ['Testing Needed'],
  });

  // Comment body
  const commentBody = 'This pull request has been marked as **Ready for Testing**. To expedite this pull request being'
    + ' merged, we encourage members of the community to test the changes and confirm they are working. You may view our'
    + ' [Testing a Pull Request](https://github.com/octobercms/october/blob/develop/.github/CONTRIBUTING.md#testing-a-pull-request)'
    + ' section in the Contibution Guide to access the changes in your own copy of October CMS.'
    + '\n\n'
    + 'If you have [Docker](https://www.docker.com/), you can quickly run a copy of October CMS with this pull request\'s'
    + ' changes in place via the following command:'
    + '\n\n'
    + '```\n'
    + 'docker run --rm -p 80:80 -e GIT_MERGE_PR=' + number + ' aspendigital/octobercms:develop\n'
    + '```';

  // Add comment
  await postComment(commentBody);
})();
```
