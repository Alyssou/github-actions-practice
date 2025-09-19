# Lab 2 GitHub Actions


## Exercise 1: Hello GitHub Actions

**Goal:** Create your first workflow that prints "Hello GitHub Actions" when you push code.

### Steps:
1. Create a new repository on GitHub (name it `github-actions-practice`).
2. Clone it locally:
```bash
   git clone https://github.com/<your-username>/github-actions-practice.git
   cd github-actions-practice
```
3. Inside the repo, create a folder .github/workflows/.

4. Inside that folder, create a file named hello.yml with the following content:
```yaml
name: Hello Actions

on: [push]

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Print Hello
        run: echo "Hello GitHub Actions 👋"
```
5. Commit and push:
6. Go to your GitHub repo → Actions tab → Watch the workflow run!

## Exercise 2: Running Tests

**Goal:** Automate tests for a Node.js project.

### Steps:

1. Add a simple Node.js project in your repo:

```sh
npm init -y
npm install jest --save-dev
```
2. Add a file sum.js:

```js
function sum(a, b) {
  return a + b;
}

module.exports = { sum };
```
3. Add a test file sum.test.js:

```js
const { sum } = require('./sum');

describe('sum function', () => {
  it('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
  });
});
```

4. Update package.json to include a test command:

```json
"scripts": {
  "test": "jest"
},
"type": "module"
```

5. Create a new workflow .github/workflows/tests.yml:

```yaml
name: Node.js Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js 22
        uses: actions/setup-node@v3
        with:
          node-version: 22
          cache: 'npm'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
```

6. Commit and push your changes.

7. Check the Actions tab → Confirm that tests are running.

## Exercise 3: 

- Try do run the workflow with multiple versiosn of node, for example 21, 22. **hint**, try to use matrix
- Imagine and create an actions that use sequential and also parallel jobs
 