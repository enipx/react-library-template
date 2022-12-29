# React library template

Step by Step Instructions to setup a react component library

- First install react & typescript as development dependencies
  - `yarn add -D @types/node @types/react @types/react-dom react react-dom typescript`
  - Add `react` and `react-dom` as peer dependencies, meaning to add as required lib when using the react library

- Add typescript config
  - `npx tsc —init`

- Install & configure Storybook
  - `npx sb init`
  - Update `.storybook/main.js` to indicate the location of your stories files, in my case, it's the src folder.
  - View configuration doc here: [https://storybook.js.org/docs/react/configure/overview#configure-your-storybook-project](https://storybook.js.org/docs/react/configure/overview#configure-your-storybook-project)

- Add Test, I’m using Jest in my project, I guess it’s due to the fact it’s the highly recommended testing library for React and also I find it more easier to use.
  - `yarn add -D jest ts-jest @types/jest @testing-library/react @testing-library/jest-dom jest-environment-jsdom identity-obj-proxy ts-node`
  - add config file `jest.config.ts`
  - create `jest-setup.ts` for the `@testing-library/jest-dom` and add the ``setupFilesAfterEnv`` there. more info here: [https://github.com/testing-library/jest-dom](https://github.com/testing-library/jest-dom)
  - Now to setup mocking for css modules, we will be using the `identify-obj-proxy` so create  `__mocks__/fileMocks.js` and setup accordingly. more info here: [https://jestjs.io/docs/webpack#mocking-css-modules](https://jestjs.io/docs/webpack#mocking-css-modules)

- Setup bundling for production
  - We are going to be using rollup to bundle the library instead of using webpack
  - Install the necessary package `yarn add -D rollup rollup-plugin-typescript2 rollup-plugin-peer-deps-external rollup-plugin-cleaner @rollup/plugin-commonjs @rollup/plugin-node-resolve rollup-plugin-esbuild @rollup/plugin-babel`
  - Setup config file and also script to package.json

- Setup eslint and prettier
  - `yarn add -D eslint prettier eslint-config-prettier eslint-plugin-prettier eslint-config-airbnb`
  - create `.eslintrc.json` , `.prettierrc` , `.eslintignore` and `.prettierignore`
  - Set up vscode settings

- Setup commint linting with `commitlint` and `husky`
  - `yarn add -D @commitlint/cli @commitlint/config-conventional husky` and commit lint config `.commitlintrc` then
  - Install husky to run commitlint as a pre-commit hook `yarn husky install`
  - Add script to package.json file `“prepare”: "husky install"`
  - setup hook to run before code is commit `yarn husky add .husky/commit-msg "yarn commitlint --edit $1"`

- Publishing
  - Setup changeset `yarn add --dev @changesets/cli`
  - Initialize it using `yarn changeset init`
  - Update config and that’s it

Credit: <https://dev.to/denniskortsch/develop-and-test-react-apps-with-react-query-msw-and-react-testing-library-1n7e>
